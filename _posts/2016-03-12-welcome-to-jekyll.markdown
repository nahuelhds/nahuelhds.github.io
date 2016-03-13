---
layout: post
title:  "Installing Supersonic"
date:   2016-03-13 02:21:00 -0300
categories: supersonic
---

After following all the Supersonic instructions for the initial installation, you'll run with some npm dependencies issues. Well, the problem is fixed by installing those dependencies.
1. After `steroids create myProject` and `cd myProject` it'll throw some errors. To fix it just install the npm dependencies that fails.
1. Long story short: `npm install grunt grunt-extend-config grunt-contrib-clean grunt-contrib-coffee grunt-contrib-sass grunt-contrib-concat grunt-contrib-copy`
1. Wait for it.
1. Good. Now just run `steroids connect` and you're done.
