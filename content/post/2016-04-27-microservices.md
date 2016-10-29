+++
date = "2016-04-27T14:21:40+08:00"
description = "Someone was going to do it eventually..."
title = "A trading platform in Go"
tags = ["code"]
+++

I've been obsessing over Go lately. I won't go into it much since pretty much everyone else on the internet has at some point or another. And all of the people I know have probably heard me raving about it. The quality of the language itself remains divisive, but I am going to soldier on and just try and build something.

<!--more-->

## The project

I've been looking at playing with [go-micro](https://github.com/micro/go-micro) and building microservices. Really, I only needed an excuse to build something. I've come across some decent trading platforms and frameworks online but nothing really built in Go. So that's my project.

The first step will be to write a client that subscribes to the Interactive Brokers API and publishes the ticker data onto a [NATS](http://nats.io/) message bus, which will then be consumed by [InfluxData's](https://influxdata.com/) Telegraf NATS connector. This will give me a bunch of data to play with, with helpful time series crunching tools that come for free with InfluxDB (`min`, `max`, even an `SMA`!).

Everything will be docker-ised into a swarm. NATS and Influx provide docker containers so that's easy. The single microservices will contain static binaries so (in theory) that will be easy as well.

## The snippet

Here is a code snippet that subscribes to the IB API (also docker-ised) and (for now) just logs the values to STDOUT.

```go
func exec(pair string, currency string) {
	log.Infoln("Starting connection to IB gateway...", "Pair:", pair, ", Currency:", currency)
	options := &ib.EngineOptions{
		Client:           0,
		Gateway:          "192.168.99.100:4003",
		DumpConversation: false,
	}

	var err error
	e, err = ib.NewEngine(*options)

	defer e.Stop()

	if err != nil {
		log.Fatalln("ERROR!", err)
		return
	}
	defer e.Stop()
	log.Infoln("Done.")
	log.Infoln("Setting up contract for subscription...")
	contract := &ib.Contract{
		Symbol:       pair,
		SecurityType: "CASH",
		Exchange:     "IDEALPRO",
		Currency:     currency,
	}

	im, err := ib.NewInstrumentManager(e, *contract)
	defer im.Close()
	ctm, err := ib.NewCurrentTimeManager(e)
	defer ctm.Close()

	if err != nil {
		log.Fatalln(err)
	}

	for {
		select {
		case <-im.Refresh():
			if err := im.FatalError(); err != nil {
				log.Fatalln(err)
			}
			log.Infoln("Time:", ctm.Time().UnixNano())
			log.Infoln("Bid:", im.Bid())
			log.Infoln("Ask:", im.Ask())
			log.Infoln("Last:", im.Last())
		}

	}
}
```

At the moment CPU usage jumps up to 50% as soon as you connect to the IB Gateway. No idea why but I'm just going to assume its a library issue for the time being.

The repo can be located on [Github](https://github.com/nii236/nii-finance).
