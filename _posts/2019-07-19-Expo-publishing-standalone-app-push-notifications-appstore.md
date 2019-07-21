---
lang: en
title: "Publishing your Expo Standalone App with push notifications into the App Store. The easy way... 😅"
excerpt: >-
  The notifications doesn't work with TestFlight? Don't worry, I have you covered
categories:
  - react-native
keywords:
  - expo
  - standalone
  - push-notifications
  - production-certificate
  - testflight
---

![Did you receive this email?](img/expo-standalone-push-notification.png)

Did you receive this email?
{: .img-caption }

Let's do a simple check.

- Did you receive a **undetermined** status from the push notifications permission? ✅
- Did you receive an email saying something about **ITMS-90078: Missing Push Notification Entitlement** after delivering your app through the Application Loader? ✅

## Making the push notifications work 📱

It took my two days and several hours to find out... 😡

The answers are on several Github issues and some threads in the Expo forums. I'm just gathering some of the info together. Basically you need to do two things.

1. Enable push notification for your app identifier. ☝️
1. Rebuild with Expo clear provisioning file parameter. ✌️

### Enable push notifications on your App ID's Identifier

[As it's mentioned in this GitHub issue](https://github.com/expo/turtle/issues/62#issuecomment-469528206):

> In order to fix this, you need to enable "Push notifications" for your app on the app store.
>
> 1. Login to [https://developer.apple.com/](https://developer.apple.com/)
> 1. Go to the "Certificates, Identifiers and Profiles" section
> 1. Select "App IDs" in the Identifiers section on the left column
> 1. Choose your app ID, edit it and check "Push Notifications". Save changes
> 1. Generate a certificate for the production push service: go to the "Certificates" section, and follow the assistant to add a "Apple Push Notification service SSL (Sandbox & Production)" certificate for your app. Acute readers will notice that expo does not need this certificate since it uses a key to talk to Apple directly
>
> TL;DR: Expo needs to enable the "Push Notification" service when creating the app in the Apple Developer Portal

### Rebuild your Expo app

Second, I'm sure you already has published you app, so what you need to do is change the `expo.ios.buildNumber` in your **app.json** file and then rebuild the app **clearing the provisioning profile** like this. 👨‍💻👩‍💻

```bash
expo build:ios --clear-provisioning-profile
```

In that way Expo will generate the build with the Push Notifications that are now activated in your App ID Identifier.

Finally, upload it again from the Application Loader. You should be fine.

**IMPORTANT!** If clearing the provisioning profile doesn't work, try *clearing all* with the command:

```bash
expo build:ios -c
```
