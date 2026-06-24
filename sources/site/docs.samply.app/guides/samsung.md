# Source: https://docs.samply.app/guides/samsung.html

# Audio stops on Samsung devices [​](https://docs.samply.app/#audio-stops-on-samsung-devices)

Samply users on Samsung mobile devices may notice that audio playback stops once the phone screen is locked. This issue is due to battery life optimizations that conserve energy by preventing network access to certain apps when they are not directly in-use.

## Solution for newer devices [​](https://docs.samply.app/#solution-for-newer-devices)

On updated Samsung devices, each app should have their own battery settings. You can find these settings at the following location:

```
Settings > Apps > Battery
```

There, you will need to make the following changes to Chrome (or your preferred browser) and Samply (if the app is installed):

```
Chrome: Unrestricted

Samply: Unrestricted
```

Once these changes are made and you restart Samply, you should notice that audio continues to play once the screen is locked.

## Solution for older devices [​](https://docs.samply.app/#solution-for-older-devices)

On older Samsung devices, there is a global setting called **"Keep WiFi on During Sleep"**. Enabling this setting may allow audio to continue to play after the screen is locked.