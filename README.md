# podcastgen

generate itunes-compatible podcasts from cson or json

## example

`example/jsdfpodcast.cson`:
```coffee
title: "jsdf podcast",
author: "john p. cast",
subtitle: "john's fab podcast subtitle",
description: "john's fab podcast description",
summary: "john's fab podcast summary",
baseUrl: "http://files.ktfr.net/podcast/",
podcastUrl: "http://files.ktfr.net/podcast/podcast.xml",
imageUrl: "http://lorempixel.com/500/500/abstract/",
language: "en-us",
items: [
  {
    title: "cashmere cat mix",
    author: "cashmere cat",
    path: "cashmere.mp3", # relative from baseUrl
    duration: "6:43",
    date: "Mon, 3 Mar 2014 00:00:00 +1100", # RFC 2822 formatted date
    imageUrl: "http://lorempixel.com/500/500/animals/"
  },
  {
    title: "jacques greene mix",
    author: "jacques greene",
    path: "LWEPodcast198JacquesGreene.mp3",
    duration: 4660,
    date: "Mon, 14 Apr 2014 00:00:00 +1100",
    imageUrl: "http://lorempixel.com/500/500/technics/"
  }
]
```

run it:
```bash
podcastgen example/jsdfpodcast.cson > podcast.xml
```

`podcast.xml`:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rss xmlns:itunes="http://www.itunes.com/dtds/podcast-1.0.dtd" xmlns:atom="http://www.w3.org/2005/Atom" xmlns:media="http://search.yahoo.com/mrss/" version="2.0">
<channel>
  <atom:link href="http://files.ktfr.net/podcast/podcast.xml" rel="self" type="application/xml"/>
  <title>jsdf podcast</title>
  <item>
    <title>cashmere cat mix</title>
    <media:content url="http://files.ktfr.net/podcast/cashmere.mp3" type="audio/mpeg" medium="audio" expression="full"/>
    <enclosure url="http://files.ktfr.net/podcast/cashmere.mp3" type="audio/mpeg"/>
    <pubDate>Mon, 3 Mar 2014 00:00:00 +1100</pubDate>
    <guid isPermaLink="true">http://files.ktfr.net/podcast/cashmere.mp3</guid>
  </item>
  <item>
    <title>jacques greene mix</title>
    <media:content url="http://files.ktfr.net/podcast/LWEPodcast198JacquesGreene.mp3" type="audio/mpeg" medium="audio" expression="full"/>
    <enclosure url="http://files.ktfr.net/podcast/LWEPodcast198JacquesGreene.mp3" type="audio/mpeg"/>
    <pubDate>Mon, 14 Apr 2014 00:00:00 +1100</pubDate>
    <guid isPermaLink="true">http://files.ktfr.net/podcast/LWEPodcast198JacquesGreene.mp3</guid>
  </item>
</channel>
</rss>
```

### api usage
```coffee
fs = require 'fs'
podcastgen = require 'podcastgen'

rssdata = podcastgen({
  title: "my podcast",
  baseUrl: "http://example.com/podcast/",
  ...
})

rssfile = fs.createWriteStream 'mypodcast.rss'
rssfile.write rssdata
```

### install

```bash
npm install -g podcastgen
```
