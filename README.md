**General**

As a big fan of radio streams/broadcasts I made some repositories about radio streaming. There are some basic principles I adhere to during making these repositories:

- Usage ofcheap and possibly old radio streamers and PC's.
- Mostly usage of opensource software.
- No subscriptions.
- No dependance on companies.
- Software mostly written in Python.
- Multi room (but not synchronized on the second)
- Reasonable large selection of radio stations.
- Also DAB radio stations.

I accomplished this with Philips radio streamers (SLA5520), raspberries (with MPD) and an old PC (with Debian). 

When you want to listen to a radio stream the most obvious ways to do that are:

- Buy a radio streamer box that works as an old radio (with FM or AM)
- Use a phone with a radio app and earphones or bluetooth amplifier.
- Use a PC running a radio-program or a webbrowser.

I concentrate on the last option because, combined with old streamers, that's the cheapest option. It is also extendable to a multi room system.

The disadvantage of this option is that the radio program used normally does not integrate with other streamers (listeners with an amplifier). I will discuss this problem in the next chapter.

**Integration with your streamers**

Using a program or webbrowser for discovering and playing a readio stream has the problem that the actual stream URL is often not shown. That gives you, as only option for integration, rerouting the audio output of your PC to an other program like icecast. I discuss that in the repositories   .......

The program streamtuner2 and streamtuner-ng give you the possibility to use the currently playing station's URL and process that for further use. Streamtuner2 can deliver PLS files, streamtuner-ng has a bookmarks.json file with the URL's of your "favorites".

**Extend the usage of streamtuner2**

Streanmtuner2 is no longer maintained. I revived it a bit by improving some plugins (for querying radio databases). The program stll has a few problems but it is quite usable again.
 
**Extend the usage of streamtuner-ng**

I made two extra plugins for streamtuner-ng. One for easier access to all the radio stations of one specific country or language. One for access to your, already saved, URL's in PLS files.  

**Delivering URL's in PLS files in streamtuner2**

Streamtuner2 has an option to save a radio station in a playlist file somewhere on your system, preferrable on your NAS mounted on your PC.

**Delivering URL's in PLS files in streamtuner-ng**

Streamtuner-ng gives you the opportunity to mark a radio station as a favorite. On the OS level you can find that in a bookmarks.json file. I made a very small service program to sync these favorites to your NAS as pls files in a favorites directory. You can copy or move those PLS files further in your "radio tree" on your NAS. Not so easy as in streamtuner2 but still usable.

**What to do with these PLS files?**

Some streamers (like MPD) might be able to simply call these PLS files. My cheap Philips streamers are UPnP devices so you have to serve these files. I used to use "Ushare" (a simple UPnP server reachable for all UPnP devices in your network). That program is no longer maintained and not available on newer Linux versions. So I made my own Ushare (in Python) with the same properties.


**Summary**

To summerize the "normal" use of the programs and plugins:

Use a webbrowser to find your radio station or play your older radio stations and play that on your PC. If you want you can stream the speaker output to icecast and let streamers connect to icecast.

Use streamtuner2 the same way and/or save the current radio
station as a PLS file in your network. 
Use streamtuner-ng the same way and/or mark the current radio station as favorite . A few moments later that station will appear in the favorites directory on your network. (if you want move that file to a better place)
In both cases let the PLS files be used as input for a streamer that can read these files or let an UPnP device use this file presented by an UPnP server.

Your saved PLS files are usable by streamtuner2 or streamtuner-ng or any player that can stream PLS files (like audacious)

**Problems with the Philips SLA5520**

These devices are, by now, 20 years old. (that's why they are cheap). Originally they were supposed to use a radio database (I think Vtuner). That was always very cumbersome but the fact that they are UPnP devices makes them still usable. The main problem with these devices is that they don't seem to support https (or TLS?). Fortunately they support a proxy server. To overcome this problem I made a small proxy server: this proxy tries the http stream requested, if not change to https , depending on the result that comes back from the radio site it follows redirects, unpacks pls's unpacks https streams and delivers back a http audio stream.

An other problem with these devices is that they only play wma and mp3 streams or music files. Maybe I will try some transcoding but don't count on that.

An other problem is that they are wifi b & g based with wpa encryption. Not all modern routers support that so find somewhere your old router.

 


