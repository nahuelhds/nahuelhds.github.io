---
lang: en
title: Setup Dark Mode in Slack on MacOS
description: You only have to follow these two steps
date: "2018-11-22T13:29:06.953Z"
categories:
  - slack
keywords:
  - dark-mode
  - dark-theme
  - macos
  - highsierra
  - mojave
---

![This is what you get after following these simple instructions](img/1__NVjk4Iy__c6ZSkfpxuQAkNA.png)
This is what you get after following these simple instructions
{: .img-caption }

### June 2019 update 💁‍

- Added a bonus step at the end of the post, for automating the dark theme implementation with a simple double-click. 😁
- Dark mode has arrived for mobile apps. [Read it in the Slack blog itself.](https://get.slack.help/hc/en-us/articles/360019434914-Dark-mode-for-Slack-s-mobile-apps) Desktop dark mode still in progress. Hopefully we can use this little hack here.
- Uddated the rawgit.com links to jsdelivr.com. (Thanks [Israel Tiomno](https://medium.com/u/7dc15be05be) 🤗)

_Credits to_ [_this Gist_](https://gist.github.com/a7madgamal/c2ce04dde8520f426005e5ed28da8608)_._

### First, configure the general theme 👨‍💻

1. Close Slack
1. Open this file `/Applications/Slack.app/Contents/Resources/app.asar.unpacked/src/static/ssb-interop.js`
1. Append this at the very bottom

```js
document.addEventListener("DOMContentLoaded", function() {
  let tt__customCss =
    ".menu ul li a:not(.inline_menu_link) {color: #fff !important;}";
  $.ajax({
    url:
      "https://cdn.jsdelivr.net/gh/laCour/slack-night-mode@master/css/raw/black.css",
    success: function(css) {
      $("<style></style>")
        .appendTo("head")
        .html(css + tt__customCss);
    }
  });
});
```

### Second, choose a proper sidebar theme 💅

1. Go to Preferences / Sidebar
1. At the end of that page, choose to set a custom color
1. Paste this custom theme:

```bash
#171717,#404245,#424242,#ECF0F1,#4A4A4A,#FAFAFA,#2ECC71,#00A362
```

You can see other sidebar themes at [Slack Theme](https://slackthemes.net). The one I chose is [Green Lantern](https://slackthemes.net/#/green_lantern).

### Enjoy the darkness 😈

That’s it. You can now open Slack and see the results!

### ¡Bonus step! Automatize this 🤓

Every time Slack makes a little update, you’ll need to manually add that little script again and again.

Well, not anymore.

First, create a bash script with the following content.

```sh
#/bin/sh

FILE=/Applications/Slack.app/Contents/Resources/app.asar.unpacked/src/static/ssb-interop.js
CSS_SOURCE=https://cdn.jsdelivr.net/gh/laCour/slack-night-mode@master/css/raw/black.css

cat >>$FILE <<EOL

document.addEventListener('DOMContentLoaded', function() {
    let tt__customCss = '.menu ul li a:not(.inline_menu_link) {color: #fff !important;}'
    $.ajax({
        url: '$CSS_SOURCE',
        success: function(css) {
            \$('<style></style>').appendTo('head').html(css + tt__customCss);
        }
   });
});
EOL

```

Save it to file “slack-apply-dark-theme.sh.command”. [The **.command** extension makes the file double-clickable from the Finder](https://stackoverflow.com/a/29710607/1588525).

Finally, set permissions 700 for it. So you’re the only that can use it.

```sh
chmod 700 slack-apply-dark-theme.sh.command
```

Now, every time you need to apply the dark theme, just double click your brand new file.
