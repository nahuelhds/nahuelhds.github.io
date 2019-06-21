---
lang: es
title: Debugging React Native + Expo with Nuclide on Windows
description: The experience that couldn’t be
date: '2017-07-24T11:48:42.504Z'
categories: []
keywords: []
slug: /@nahuelhds/debugging-react-native-expo-with-nuclide-on-windows-fb47be0b36ad
---

### TL;DR

Don’t waste your time. For a better dev performance with React Native on Windows, I strongly recommend using [VS Code](https://code.visualstudio.com/). With it I happened to debug React Native whether with Android under Genymotion or **with iOS with my real device through remote debugging (this is what I wanted so far).**

### My experience

Nuclide maybe is the a jump for web debugging with React. I’m sure of it. Specially if you were using Atom till now. But when it’s about mobile development and debugging-and specially trying to do so onto an iPhone device being a Windows user- it lacks of some features. If you’re on Windows, Nuclide lets you know that they don’t fully support it. Well, this is it.

I fought literally a couple weeks to reach a good IDE configuration till I did make it and I started coding React Native with the help of ESLint and Flow. It worked like a charm if we focus on the actual coding activity -especially the code intelligence and the autocomplete features. I was very enthusiastic.

#### The debugging issue

A little days after, I had the need to debug my app, see some values in order to optimize some functions, etc, etc. **There’s where I started suffering the absence of official support as a Windows user.** Facebook’s Nuclide experience is based on Mac env. They don’t bother on the Linux/Windows. _It’s up to the community._

Anyway, I’ve found some debugging solutions. As they’re not the same as debugging on web -where you can set breakpoints and change the code locally through Chrome DevTools- it’s a step forward.

My dev env is:

*   Windows 10 64 bits
*   Atom + [Nuclide](https://nuclide.io/)
*   [React Native](https://facebook.github.io/react-native/)
*   [Expo.io](https://expo.io/)

The tricky was finding mixed references between [CRNA (React Native Create App)](https://github.com/react-community/create-react-native-app), Expo and [React Native Cli](https://www.npmjs.com/package/react-native-cli). In every use case, the thing with [Nuclide Inspector](https://nuclide.io/docs/platforms/react-native/#element-inspector) is:

1.  The packager differs from what Expo uses for its app launches.
2.  When connecting to the packager, **the inspector looks for a fixed port** (8097 if I remember correctly) and that cannot be configured in any way _but touching the files inside node\_modules_ (ugly)

Besides, almost every success case of remote debugging on iOS devices were from Mac devs. So, while moving forward in my research my frustration grew.

The only way for debugging I had was:

1.  “Start remote JS debugging”.
2.  Use the Chrome Dev Tools from the debugger-ui page that Expo launches automatically.
3.  Write “debugger;” where I wish to set a breakpoint.

Forget about doing local modifications on the files while in a breakpoint: I had to go to the Atom window, go back to the Chrome page, once and again.

### Conclusion

Don’t waste your time: Nuclide is an advance for Windows users but as they advice in their website “Windows is not fully supported” and **this sentence is real if you’re trying to remote debug React Native in your iOS device**.

¿My solution? Using [VS Code](https://code.visualstudio.com/).
