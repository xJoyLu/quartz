author:: null
source:: [Web Scraping via Javascript Runtime Heap Snapshots - Adrian Cooney's Blog](https://www.adriancooney.ie/blog/web-scraping-via-javascript-heap-snapshots)
clipped:: [[2022-07-09]]
published:: 

In recent years, the web has gotten very hostile to the lowly web scraper. It's a result of the natural progression of web technologies away from statically rendered pages to dynamic apps built with frameworks like React and CSS-in-JS. Developers no longer need to label their data with class-names or ids - it's only a courtesy to screen readers now.

There's also been a concerted effort by large companies to protect their public data. Facebook, for example, employs a [team of over 100 people](https://about.fb.com/news/2021/04/how-we-combat-scraping/) to make sure it is as difficult as possible for any data to escape the black hole. Granted, some of these large companies do offer APIs for their data but rarely is this unrestricted. You're usually at the whim of their app review process or granted access only to a partial view of the data. Data that would be otherwise public if you were to do a Google search and click through to their website manually.

![How HTML looks nowadays](https://www.adriancooney.ie/_next/image?url=https%3A%2F%2Fimages.ctfassets.net%2Fnpzloj4jufpj%2F6fDxT3Yshk7RQNidx1tDA8%2F07eecdbd9539d44a60e8f1da6b00ef5d%2FScreenshot_2022-04-26_at_23.25.09.png&w=1920&q=75)

How HTML looks nowadays

This can be frustrating if you're like me - somebody who wanted to build a small, local, non-profit app that uses data hosted on a closed platform. The data is public but completely inaccessible to machines because of aggressive anti-web-scraping measures. That gave me two options - input the data manually or play the web-scraping game. Of course, I chose the latter.

### `puppeteer-heap-snapshot` is born.

After a couple of attempts at extracting the data using the usual CSS selector method of web-scraping - that is, fetching the raw HTML or booting up a browser via something like [Puppeteer](https://github.com/puppeteer/puppeteer) and trying to pick the data embedded in the HTML structure - I was close to admitting defeat. It wasn't until I had an epiphany: the data is *inside* the web page.

I plucked out a unique string from the data visible on the web page and took a heap snapshot of the browser's Javascript runtime via Chrome's Dev Tools. A heap snapshot is a raw dump of everything in the web app's memory (or heap). Using the Dev Tools' search function and my unique string, I managed to find a nice, well-structured object containing my string and, adjacently, all the data that my app needed. It was from this point that I focused my energy on automating this process to find and extract the data from the heap snapshot. `puppeteer-heap-snapshot` is born.

![Chrome Dev Tools' Memory Profiler](https://www.adriancooney.ie/_next/image?url=https%3A%2F%2Fimages.ctfassets.net%2Fnpzloj4jufpj%2F1VPKptaSPuNl8kbCWS4t4g%2F36963d9d0b96d268b8a7b9c3b88bb052%2FScreenshot_2022-04-26_at_23.44.10.png&w=1920&q=75)

Chrome Dev Tools' Memory Profiler

[`puppeteer-heap-snapshot`](https://github.com/adriancooney/puppeteer-heap-snapshot) is a Node.js module that, given a [Puppeteer](https://github.com/puppeteer/puppeteer) browser page, can capture and parse a heap snapshot and deserialize objects that contain a set of properties. It comes with a nifty CLI tool too so we can quickly prototype scrapers from our terminal.

For example, let's fetch the metadata from the above video:

`$ puppeteer-heap-snapshot query \
 --url https://www.youtube.com/watch\?v\=L_o_O7v1ews \  --properties channelId,viewCount,keywords --no-headless 
>> Opening Puppeteer page at: https://www.youtube.com/watch?v=L_o_O7v1ews >> Taking heap snapshot..
[  {  "videoId": "L_o_O7v1ews",  "title": "Zoolander - The Files are IN the Computer!",  "lengthSeconds": "21",  "keywords": [  "Zoolander",  "Movie Quotes",  "2000s",  "Humor",  "Files",  "IN the Computer",  "Hansel"  ],  "channelId": "UCGQ6kU3NRI3WDxvTGIsaVjA",  "isOwnerViewing": false,  "shortDescription": "",  "isCrawlable": true,  "thumbnail": {  "thumbnails": [  {  "url": "https://i.ytimg.com/vi/L_o_O7v1ews/hqdefault.jpg?sqp=-oaymwEbCKgBEF5IVfKriqkDDggBFQAAiEIYAXABwAEG&rs=AOn4CLCRXqKq4f3pDXFysaLwvaK7zokbcA",  "width": 168,  "height": 94  },  {  "url": "https://i.ytimg.com/vi/L_o_O7v1ews/hqdefault.jpg?sqp=-oaymwEbCMQBEG5IVfKriqkDDggBFQAAiEIYAXABwAEG&rs=AOn4CLAUYKiFQE7AsuwoLrJZldUQRzjZig",  "width": 196,  "height": 110  },  {  "url": "https://i.ytimg.com/vi/L_o_O7v1ews/hqdefault.jpg?sqp=-oaymwEcCPYBEIoBSFXyq4qpAw4IARUAAIhCGAFwAcABBg==&rs=AOn4CLB_nQ2Un8uDxAAYOYB_E4fMaxCt2g",  "width": 246,  "height": 138  },  {  "url": "https://i.ytimg.com/vi/L_o_O7v1ews/hqdefault.jpg?sqp=-oaymwEcCNACELwBSFXyq4qpAw4IARUAAIhCGAFwAcABBg==&rs=AOn4CLB7uDAGHDaTSAe3xy5q3H2JqekbAw",  "width": 336,  "height": 188  }  ]  },  "allowRatings": true,  "viewCount": "140687",  "author": "James",  "isPrivate": false,  "isUnpluggedCorpus": false,  "isLiveContent": false  } ]`

In that command, `puppeteer-heap-snapshot` booted up an instance of Chrome, navigated to the video on Youtube and took a heap snapshot of the page (58Mb in total, they can get large!). It then parsed that heap snapshot, found the object with the properties `channelId`, `viewCount`, `keywords`, and deserialized it back to us. These properties were chosen manually by working backward from the visible data on the web page to the data structure containing said data (I'll dive into that process in another blog post). We use the `--no-headless` argument to boot a windowed Chrome instance (i.e. not headless) because Google can detect and thwart headless Chrome - but that's a story for another time.

We can see the response is JSON! A clean, well-formed data structure extracted magically from the webpage. On top of that, the definition of the scraper is just 3 strings: `channelId`, `viewCount` and `keywords`! We no longer have to maintain a complex web scraper tightly coupled to the semantics of an ever-changing webpage. Instead, we can target objects that do not change often like API response objects or well-defined entities.

### Future proof web-scraping?

You can imagine the grin on my face when I managed to circumvent the aforementioned closed-platform aggressive anti-web-scraping measures using this method. I experimented with other platforms like Facebook, Instagram, and Twitter and they're all susceptible to the technique after tweaking a few parameters. I've been using `puppeteer-heap-snapshot` in production for quite some time now and it's working surprisingly well.

![Me not fixing a broken web scraper and having more fun](https://www.adriancooney.ie/_next/image?url=https%3A%2F%2Fimages.ctfassets.net%2Fnpzloj4jufpj%2F1rxzUBV0ImX5FUOWhqYvFQ%2F07221f3d6d437958df4c9d5c037fd05b%2Fantonino-visalli-RNiBLy7aHck-unsplash__2_.jpg&w=1920&q=75)

Me not fixing a broken web scraper and having more fun

This method still comes with the same caveats that web-scraping always had - the public data could be here today, gone tomorrow and there is nothing you can do about it. The benefit of this technique though is the maintenance cost of the web scraper is greatly reduced and I'd even wager they will break *far less* than the current standard pattern.

It's costly for systems like web apps to change their underlying data structures because they're usually tightly coupled to the server meaning property names of objects are unlikely to change over time. On top of that, attempting to break the technique by obfuscating the data structure would be a large and costly undertaking because it would require obfuscating the entire stack - a mighty feat. Is this possibly a future-proof web-scraping technique? Maybe .. Web Assembly might be the final nail in the coffin.

### Get started heap snapshot scraping.

Hop on over to [`puppeteer-heap-snapshot`'s Github Page](https://github.com/adriancooney/puppeteer-heap-snapshot) to get started using it (now that it's [officially legal](https://techcrunch.com/2022/04/18/web-scraping-legal-court/)!). It's still in an experimental/beta phase so proceed with caution when deploying. It's also incredibly slow - I didn't put any effort into optimizing the algorithms that query the (huge) heap snapshot data structures because I had more pressing features to build so please don't kill me for the CPU spikes (your orchestrator might kill your containers though, a lesson learned).