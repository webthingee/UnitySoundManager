# UnitySoundManager
A Sound Manager for use in Unity

# Overview
As a new indy game developer and avid GameJam participant, this is a project I was inspired to create after I experienced a major time crunch at the end of a GameJam. It was the last few hours of the GameJam, and I still needed to do a ton of work with the audio. 

In addition to creating the actual sounds I wanted to use, I still needed to decide how and where to place and manage Audio Sources. A lot of time, effort and thought was still needed to figure out how to manage and pass in the audio clips, manage stops and starts, and test to ensure there were no conflicts with Audio Sources. It was time I didn't have at the end of a GameJam, and if you're still reading this, you may have found yourself in the same boat at some point.

One of the specific challenges I experienced was managing sound effects when a GameObject was destroyed. Since I usually create first, add sound later, there were many times where ```OnDestroy()``` would not work for me to play a sound because the script and Audio Source were attached to the object that was being destroyed. Which meant I was going to have to either change the GameObjects or Prefabs, or move the code and Audio Sources to other GameObjects.

Well, all this inspired me to create this Sound Manager. My goal was to have one GameObject that I could rely on, send audio clips to, have them play, and then just forget about them.

I decided to think along the lines of object pooling. This led me down the thought path of spinning up and destroying Audio Sources on the fly. The concept was to have an Audio Source ready to play a clip, then play the clip, and then if the Audio Source was no longer needed, clean up after itself (e.g. destroy itself if it was not needed in the near future). Again, my top priority was set it, forget it, and use it over and over and over again.

After some advice from Steel_Dev (a fellow Unity developer that also hangs out on [GamesPlusJames](https://www.twitch.tv/gamesplusjames)), I ended up with this Sound Manager that is a quasi Audio Source pooling system that can do all the things I wanted. It can spin up Audio Sources as needed, destroy Audio Sources when not needed, and even hold a buffer of Audio Sources that are ready for usage if speed or performance become an issue.

So here we have it. My first Unitypackage that I think others might find value in. While I know there are many other ways to solve this problem, this is the approach I decided to start with, and I hope to use this in my next GameJam, perhaps making improvements to this UnityPackage along the way.

# Created with
* Unity 2017.3.1f1
* Audio Files created at https://www.bfxr.net/

# Examples

Use as you would `AudioSource.Play()`, pass the clip and an optional volume.
```Csharp
SoundManager.Instance.SMPlay(sound, 0.5f);
```

Use as you would `AudioSource.Play()`, pass the clip, volume, and optional looping.
```Csharp
SoundManager.Instance.SMPlay(sound, 0.5f, true);
```

Use as you would `AudioSource.PlayOneShot()`, pass the clip and an optional volume.
```Csharp
SoundManager.Instance.SMPlayOneShot(sound, 0.5f);
```

