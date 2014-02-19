---
layout: post
title: "Compile pov-ray on debian jessie"
date: 2014-02-18 20:08:43 -0500
comments: true
categories: 
---
Man I'm terrible at keeping this blog up to date. Anyway - I've decided to play
around with <a href="http://www.povray.org">the Persistence of Vision</a>
raytracer again (aka "pov-ray"). It's a pretty old but capable raytracer.
It's got a fairly easy to understand scene description language that gives you
some major power, and I'd like to think I'll be able to auto-generate some
interesting stuff via ruby - we'll see.

Unfortunately, it's been removed from the debian repos, so you're left to get
it installed yourself. Here's how I did it on debian testing (currently
"jessie"):

    sudo aptitude install build-essential libboost-dev libboost-thread-dev zlib1g-dev libpng12-dev libjpeg8-dev libtiff5-dev libopenexr-dev
    git clone https://github.com/POV-Ray/povray
    cd povray
    git co 3.7-stable
    # Now we follow the unix/install.txt instructions, sorta.
    cd unix
    #Need to fix prebuild.sh for the newer version of automake in jessie
    sed 's/automake --w/automake --add-missing --w/g' -i prebuild.sh
    cd ..
    ./configure --prefix ~/bin/povray COMPILED_BY='dan@collispuro.cnet' LIBS="-lboost_system -lboost_thread"
    make
    make check
    make install

and it'll install into `~/bin/povray/`.

Thanks to <a href="http://news.povray.org/povray.unix/thread/%3Cweb.52810591323e085d7a3e03fe0@news.povray.org%3E/">this post</a> for getting me over the automake incompatibility confusion, where an empty `Makefile.in` was being generated while trying to `./configure`.
