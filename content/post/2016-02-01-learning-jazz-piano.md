+++
date = "2016-02-01T10:06:25+08:00"
title = "Experiments in learning jazz piano"
tags = ["piano", "jazz", "music"]
+++

So I have been learning music on and off for years, and have never really gotten to a __fully sick__ level of proficiency. The problem here is usually that I don't put in enough hours, which is true. The other problem is paralysis analysis, and the filthy need to optimise my learning. I have suffered this same problem in my Japanese studies but I'll leave that for another post.

# Jazz

My background is classical piano, where I learnt enough in high school that a constant level of proficiency just sticks with me for the rest of my life. My interest in the past five years, however, has been jazz piano. I have had various teachers, learning methods and styles, but have never really seemed to stick. My poor sight reading ability coupled with my adult responsibilities (harhar) make it difficult to keep a steady practice routine going.

I am about to embark on a new method, combining everything that I have attempted so far.

# Synthesia

The game [Synthesia](http://www.synthesiagame.com) is something that has been around for a long long time. I bought a license back in 2011 I think, and its still been going strong. I opened up the latest version just last night and it seems that it now supports:

- Custom hand splitting
- Looping
- Sweet sweet UI

Definitely worth the price.

## Finding high quality MIDI

Most of the songs in Synthesia kind of suck to be honest. Not to mention irrelevant to jazz piano. Or classical piano. Or anything decent really. And I refuse to pay for lame-o Adele piano covers.

So I went hunting around for decent jazz piano MIDI. It needs to ideally have backing tracks, quantized beats and split tracks for each hand. Its not easy. Here it is.

[Douglas McKenzie](http://www.bushgrafts.com) (I bought his DVD!) is a great jazz pianist in Australia. He has a website with excellently formatted MIDI files. Its actually to time! And he even releases sheet music transcriptions of each of his solos. The MIDI files even have his annotations of each improvisation idea dammit! Its amazing.

I am also lazy. So run the following code in the folder of your choice to download all the MIDI files on his page.

```
wget -A mid -m -p -E -k -K -np http://www.bushgrafts.com/jazz/midi.htm
```

Stage 2 (actually stage 999) will be to look at these [Bill Evans transcriptions](http://www.billevans.nl/midipage.htm). Pull them thus:

```
wget -A mid -m -p -E -k -K -np http://www.billevans.nl/midipage.htm
```

## Using the MIDI

So just feed these into Synthesia, have a listen, play what you can, then check against the Synthesia falling notes, official sheet music or the generated ones from the game.

Feed the MIDI output into a virtual MIDI device into Reaper, and listen to that [sweet sweet piano VST](https://www.pianoteq.com/) that you no doubt own.

Practice the ear, export to MP3, run it through [Transcribe](http://www.seventhstring.com/) (or just slow it down through Synthesia)!
