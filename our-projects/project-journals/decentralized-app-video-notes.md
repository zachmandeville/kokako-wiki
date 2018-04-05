<!-- Title: Notes from watching 'Making Decentralized Apps with Alexander Cobleigh -->

# Why make decentralized apps
- When you are using a service, you are at the whims of the creators of that platform.  Like twitter moving from favs to hearts and favorites to likes, then introducing the likes into your timeline.
- The platform holders will control our own experience, but this is unneccessary.
- What brings decentralized designers together: a want to control their own information and how it's shared.  It's an unexplored space, largely, where you can try things again.  Make the future exciting again.

# What is a decentralized App
Good to look in context:
- Centralized is a central server or provider, which presents a central weakness too.
- Decentralized has different nodes that sometimes talk to one another.  When one node goes down, the rest are still there.  But you can still centralized pouplarity into a single node, which provides weakness.
- Distributed is really what he's talking about, but it's a newer term. Here, everyone is connected to everyone else through some basic social connection.  There isn't any central point of weakness, and the power is in the peer and not the platform owner.
- Take back control of the _idea_ of the web.
Properties:
- Works Offline
- No servers!  No domain names! No cost!
- you can change anything!
- extremely cool and underground

# How?
- Dat: a beautiful combo of torrents and github repos.
- Basic unit is a dat archive, represented by a hash.
- works essentially like a webpage.
- You can code and work in node.js (the entire ecosystem is done in node).

# Buffet of demos
- First one was just an html page with links to the other demos.
- Second was reading and writing to dat. You can adjust the color of a page for example and it saves, because you are writing through api to the json file of the site.
  - It's done by writing a function that loads the initial color, then a function that, through the api, reads the json file for what color is set and then applies that value to the page.
- The third demo was showing how you can keep your business logic server separate from the local css.  in other words, you can make the app run the way you intended while letting the local user fashion their v. of the site any way they want.
- Last one was datradio.  Where you share links to music by uploading a folder to dat and then sharing that folder.  That action is super simple!

