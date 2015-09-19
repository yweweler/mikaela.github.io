---
layout: post
comments: true
title: "Quickstart with Atheme IRC Services (& forks) for end users"
category: [english]
tags: [english, irc, atheme]
---

Atheme IRC Services is the most used IRC service package. However many
 people have difficulties with registering a channel and then managing
 it, which I attempt to help with here. I start by explaining NickServ
 registration (and as a bonus HostServ) and then move to channel
 management and you just cannot talk about that without mentioning
 GroupServ too...

## NickServ

You won't be able to do anything unless you register your nick. This is
as easy as `/msg nickserv register PASSWORD someone@example.net`.

Depending on Atheme configuration on the IRC network you are using, you
must verify your email by checking it and copy-pasting the command which
starts with `/msg NickServ verify register` to NickServ.

In case you wish to have multiple nicks in the same account, that is also
easy, just `/nick AltNick` and `/msg nickserv group`. You can see nicks
you have by using `/msg nickserv info yournick` (other people (except IRC
operators) cannot see that part).

Now you should be successfully identified and should configure automatic
identification, I cannot help with it so much, but I can point you to
beginning:

* [freenode's SASL instructions](https://freenode.net/sasl)
* [My instructions for SASL with WeeChat]({% post_url 2015-03-26-weechat-sasl-simply %})
* [DuckDuckGo YOURCLIENTHERE SASL](https://duckduckgo.com/?q=YOURCLIENTHERE%20SASL)
* IRCCloud: edit network and go to advanced settings and you will see box
  for NickServ password.
* KiwiIRC: Check "I have a password" and type your passsword there. Ensure
  that you specified a nick that is grouped to your account.

## HostServ

In case the network you are on has HostServ, you can get vhosts with it.
Vhosts appear in place of your real host/cloaked host, but
[won't hide your IP](https://gist.github.com/maxteufel/1e2cf7ada079c271bd3c).

There are two ways to get a vhost, take one that is offered to everyone or
request something.

* Check `/msg hostserv offerlist` and if you see something you like, you
  can enable it with e.g. `/msg hostserv take $user.irc.example.net` and
  running `/msg hostserv on`.
* Use `/msg nickserv request blah` and when you receive message telling you
  that your requested vhost has been approved use `/msg hostserv on`.

## ChanServ

And finally to the topic which seems to be the most difficult, channel
(access) management.

First register the channel with `/msg ChanServ register #channel` while
you are opped. Now you are free to setup the channel as you wish.

I use the following templates, so I can e.g.
`/msg chanserv flags someone op` instead of
`/msg chanserv flags someone +vVhHoOirtAe`. You can also use the network
defaults that you can see with `/msg chanserv template`.

*This is a bash scripts which is ran like `./cstemplate #channel` and
copy-pasted to ChanServ. It basically allows ops to do everything they
could do anyway by being opped using services and "trusted users" have
became regulars on channels I am on. If a flag doesn't exist on the network
you are on, Atheme will just silently ignore it.*

**You should see my cstemplate script here, but the embedding isn't
working, to see it [please click here to go to the GitHub instance of it](https://github.com/Mikaela/gist/blob/master/irc/atheme/cstemplate).**

Another example using my templates would be `/msg ChanServ flags #channel !channel-ops` which would give op permissions above to users in the
!channel-ops group.


## GroupServ

I mentioned groups a little earlier and now I am returning to them. They
are a way to manage flags of group of users very easily by having
all users in the group and just setting flags to the group instead of
invidual users.

*GroupServ is undervalued service and it might not be surprising if it's
missing from your network :(*

Start by creating your group `/msg groupserv register !blah` (you might
want to register a more descriptive name).

Next, as in this example this group is going to be op #somewhere we close
the group: `/msg groupserv set !group open off`.

Now there are only two tasks left, making the group op and adding ops
there:

* `/msg chanserv flags #channel !blah op`
    * where `op` can still be replaced with `aop` if you are following
      Atheme defaults or some other template you created or your own
      set of flags.
* `/msg groupserv flags !blah user +c`
    * Repeat as many times as you have ops, to remove ops you simply remove
      their `-c` flag or all flags (`-*`). You will also want to read
      `/msg groupserv help flags` as there is more than I said here.

## Futher reading

* [Always add opers to access list (this is the $oper in my templates)]({% post_url 2015-01-10-channels-hostmask-groups-a-basic-howto %})
    * oops, did I just repeat previous post :smile:
* `/msg NickServ help`
    * `/msg NickServ help set`
        * especially worth taking a look at: `emailmemos` & `enforce`
* `/msg ChanServ help`
    * `/msg ChanServ help set`
        * especially worth taking a look at: `guard`, `keeptopic`,
          `verbose`
* `/msg GroupServ help`
    * `/msg GroupServ help flags`
    * `/msg GroupServ help set`