Title: Humble Beginnings
Date: 2015-03-15 20:29
Category: dev
Tags: pi, pelican, lighttpd, markdown

So here we are! My new blog is up and running, all hosted on my Raspberry Pi sitting back at home. I'm sitting at Whole Foods, mooching off my third hour of free Wi-Fi. I had no idea that a laggy-SSH hell existed but damn, I wish upon nobody this several-minutes keyboard input delay.

##Bloging Infrastructure

The setup was quite simple. Pelican installs via pip and comes with a quickstart command which makes everything super easy and streamlined. I'm also writing this blog with markdown which makes typing everything up in terminal Emacs over ssh not a terrible experience. (Technically, I could also mount my Pi's filesystem and use a local text editor too. I don't know why I'm not doing that.) lala

```
sudo apt-get install python-pip  
sudo pip install pelican  
sudo pip install markdown  
```

Blahblahblah type up some markdown.md files into the pelican/content directory, use the pelican command, generate some html, and then bam the blog is up and running. Cool.

```
cd ~/pelican/content
emacs hello_world.md  
cd ~/pelican ; pelican  
# output html files located in ~/pelican/html
```

##Markdown

I found this awesome 10 minute tutorial on how to learn Markdown [here](http://markdowntutorial.com/). I'm already using most of the basic functions in this first post! Woohoo!

##Lighttpd

And finally, my webpage is hosted on Lighttpd, a super lightweight web server. Super easy to set up as well. Standard install:

```
sudo apt-get install lighttpd
```

... then edit the configuration file to point to Pelican's output files:

```
sudo emacs /etc/lighttpd/lighttpd.conf
```

Make this line point to the pelican/output folder:
```
server.document-root        = "/var/www/html"
```

Reset the server:
```
sudo /etc/init.d/lighttpd restart
```

Fun Linux facts that I didn't know prior to my current Co-op work term:

* All configuration files are in /etc
* All processes that automatically run on startup have runners in /etc/init.d

Cool to see work coming into my play haha.

##Todo
I'm feeling tempted to naively open my blog and webserver up by forwarding my home router's Port 80 to my Pi. For now, I'll pick a different port to be safe. I was also looking into some chroot jailing for lighttpd and got that set up as well, even though I'm not using any PHP or SQL right now. Always more security stuff to look into.

Also, I only have a single blog post and it's taking Pelican **_10.7 seconds_** on average to generate the entire webpage. This might be a problem down the road when this entire blog gets bigger. I might need to look into the HTML generation on a more powerful computer and then copying the files over via Git or something. Or buy a Raspberry Pi 2. The latter is much more tempting.