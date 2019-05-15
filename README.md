# Share channels between Slack accounts!

## How's this work

In an ideal world you'd point an outbound webhook from your team's slack directly to an inbound webhook of your friend's slack team. Since that doesn't work, point your outbound webhook to this project which will re-format the data and forward it along to the inbound webhook of your friend's team. Now messages in your channel will show up in your friend's channel. Once your friend does the same with her team, you have bi-directional communication.

Slackline requires no configuration on the server. Everything is handled via URL parameters.

## Why did we develop Slackline?

We are big fans of [Slack][slack] and have been using it for a while
now. Our friends at [Vizzuality][vizzuality] started using it recently
and we missed not being able to speak with them. We started with a light
integration with Slack using 4 webhooks and this project.

This gave way to better way to share channels across between slack teams: [slackline.io](http://slackline.io)

**You can try it for free joining our [#slackline shared channel](http://slackline.io/shared_channels/slackline)**

## ~What is the difference between the free and paid Slackline?~

Slackline.io has closed.

~The free version is a light integration with the Slack API just using incoming and outgoing webhooks.~

~[slackline.io](http://slackline.io) allows you to~:
 - ~See the avatars from the users in the other team.~
 - ~Easier to setup: create your shared channel, share the URL to the shared channel with somebody in the other team and they can connect their team by themselves. No need to exchange tokens or manually craft URLs.~
 - ~Support for more than two teams connected to the same shared channel.~
 - ~Any team can change the channel they are using with no need to change anything in the other teams.~

~[slackline.io](http://slackline.io) is still under development, but you can try it for free connecting to our [#slackline shared channel](http://slackline.io/shared_channels/slackline) and we'll notify you as soon as it's available.~

## How do I use slackline for free?

~We would obviously recommend you use [slackline.io](http://slackline.io) since it's easier to setup and seeing avatars from those on the other side really rocks. But, if you want to use this version, that's cool with us too! :)~

You just need to follow the following steps to setup a channel.

 0. Host this project somewhere. A free heroku app will go pretty far, just note that the first message will be delayed while your instance boots up.
 1. Create a channel you want to share with another team.
 2. Create an Incoming WebHook integration and select the channel you created.
 3. Copy the Incoming WebHook token from the URL Slack provides for the WebHook. The token is the last element of 
 the URL, ie: ```https://hooks.slack.com/services/[...]/[...]/[TOKEN]```
 4. Create a URL with the following format: ```http://slackline.herokuapp.com/bridge/?token=[TOKEN]&domain=[YOUR_SLACK_DOMAIN]``` send it to the person setting up the other team.
 5. The person setting up the other team will send you a similar
    URL with their domain and token, create an Outgoing WebHook with
    that URL and the channel you created in step 1.

Once you have done this in both teams, you will have a chat-room shared by both teams.

Here you have an example of a Outgoing WebHook URL:

```
http://slackline.herokuapp.com/bridge/?token=bcaa5867b1d42142b74eDVA4&domain=avengers.slack.com
```

## Bridging 3 or more channels

The above 5 steps will work for bridging 2 channels together. If you want to bridge 3 channels, simply add the outgoing URLs
for each of the other two teams into your Outgoing WebHooks (1 URL per line). Have the other 2 teams do the same. There's no
limit to how many teams you can combine this way.

Optionally you can add "from=[identifier]" to the outgoing URLs you enter in step 5. This will
append the identifier to the end of the user name so people know where that user came from. 

Ex: If your username is "Jeffery" from taskmasters.slack.com, then setting a url of:
```
http://slackline.herokuapp.com/bridge/?token=bcaa5867b1d42142b74eDVA4&domain=avengers.slack.com&from=Taskmasters
```
will cause messages you chat to show up in the avenger's team as
```
Jeffery Taskmasters [bot]
hey guys
```

instead of the usual
```
Jeffery [bot]
hey guys
```

Everything YOUR team says is sent out via the outgoing hooks, so by adding &from= you make things nicer for the other teams. Ask them to do the same!

## How does it work?

We are just bridging hooks, we don't store any messages going through
the bridge.

## DISCLAIMER

This project is not officially supported by [Slack][slack] and they are
not responsible for the use you make of this and won't give you any
support related to this integration.

Now that we are talking disclaimers... I'm not responsible either for
any use of the software. Use at your own risk and to be safe it might be
good if you deploy this yourself rather than using my Heroku deployment ;)

## MIT LICENSE

Copyright (C) <2014> Ernesto Jimenez <erjica@gmail.com>


Permission is hereby granted, free of charge, to any person obtaining a
copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be included
in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS
OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


[slack]: http://slack.com
[vizzuality]: http://vizzuality.com
