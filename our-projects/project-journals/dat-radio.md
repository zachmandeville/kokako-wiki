<!-- Title: Dat Radio Pull Request -->
<!-- Subtitle: Learning a cool thing well enough to improve upon it! -->

# Background
Dat Radio is a decentralized playlist collector/player.  It has the promise of offering a sort of "decentralized bandcamp", where someone could upload their album for others to hear without requiring any central service or server.  If this was accessible to artists, then they can hold more power in the means of distribution and it would help lead towards my ideal solarpunk, punk2punk future.

Dat Radio is currently in Alpha, there is one version of it on dat and also a youtube video.  In talking to the creator, I know there are other elements they'd love to add like cover photos and descriptions.  There is ample room for improvement on this app, and it offers a way for me to learn decentralized dat sites.

#Intentions
- Better understand how a decentralized dat:// app works
- Be able to _use_ the app well enough to share my own mixtape.
- Be able to add an improvement to it that is accepted by the repo owner.
- Document my own Process around this.

# The Stages of this Project
- Get to know the app and the creator
- Replicate and use the app
- Reflect on process so far and plan improvement.
- Implement and test improvement on my fork.
- Fashion a pull request to the central repo.
# Steps I took
## Watched the Introduction to decentralized apps.
The creator of dat radio, [Alexander Cobleigh](https://cblgh.org/) gave a 30 minute talk on building decentralized apps.  At the end he gave a demo of dat radio.
The talk can be found here: https://www.youtube.com/watch?v=-0cgl6okmUs&feature=youtu.be&t=1670
Here are my notes from watching the talk: [notes on making decentralized apps](decentralized-app-video-notes)

## Made a basic Beaker app
I want to better understand how beaker (and dat) works, before I try to figure out the datradio code.  There are a number of tutorials on the beaker homepage i can use to learn more.  

First off: a beaker blog
I am following the tutorial here: 
https://beakerbrowser.com/docs/tutorials/create-a-blog.html

I am realizing that it requires using jekyll, and presumes an understanding of this.  This works for me, but would not work for someone who never used the command line, or ruby, or ruby gems, or jekyll.  There are so many new concepts constantly!

The point of this is showing how you can move an entire folder over to beaker and it still works.  so you do your work offline and get it looking good, and then dat from that point forward will publish that blog to the rest of the world.

Done and done!

## Got Buffet of Demos and DatRadio working on local machine.

@clbgh made up an intro to dat apps, which I forked here:  https://github.com/zachmandeville/decent-dat-intro

This is a great repo/talk as it provides the source for each of the sites he mentioned.  So I can get them working on my own browser (and so essentially be serving them up myself), and then study how exactly they work.  

The easiest one to follow, most likely, is the read/write site.  I forked the site here:
<dat://4b9b475826314432f930122835130f298c4e333ad104a237e6ff38195334ffd1/>

Here is my study on how it works!
[exploring how read/write on dat](dat-read-write-exploration)

## Add a function to a simple site like read/write

One of the demo sites let you change the background based on whatever you input.  I realized that the code was simple enough that I could try an experiment on it.

Currently, the font is a file located in the archive, and then set in the CSS file.  Since you can change the body background color easily, i imagine you could change the font too.  

[How I made a feature to chang ethe font on a site](font-changing-feature)

# Necessary Resources
