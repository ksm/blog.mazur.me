---
layout: post
title:  "How to get Playground Driven Development working with Carthage"
---

I introduced [Playground Driven Development](https://www.pointfree.co/episodes/ep21-playground-driven-development) on the last project I worked on. It sped up my development and forced me to write view controllers in a decoupled way. But before I was able to reap the benefits of PDD I hit a roadblock: Xcode Playgrounds kept throwing a `Couldn't look up symbols` error, because it couldn't see [Carthage](https://www.github.com/Carthage/Carthage)-built dependencies. Here's how to fix this issue.

## Identifying the problem

Initially I wasn't sure what the source of my Playgrounds problem was, so I made a [sample PDD project](https://github.com/ksm/Habits) without Carthage. Next I installed Carthage and added a single dependency[^1]. This reproduced the problem:

![Screenshot of Xcode Playgrounds with the couldn't lookup symbols error](/assets/2019-02-09-playground-driven-development-and-carthage-001.png)

## Fixing the *couldn't look up symbols* issue

I knew Playgrounds were missing some symbols, and I knew this was Carthage related. It became clear that Carthage supplied dependencies weren't being seen by Playgrounds. What wasn't so obvious to me is how to fix this issue in a way that wouldn't require any kind of Xcode project restructuring.

I reached out to the iOS community with the sample project that reproduced the problem, and it turned out that [Logan Moseley](https://github.com/loganmoseley) was having the same problem. Within a day Logan figured out the [simple fix](/assets/2019-02-09-playground-driven-development-and-carthage-logan-fix.png) I was searching for. Thank you Logan! Here are the steps:

1. Select Xcode → Project Settings → Targets → your main AppFramework target
2. Click on the Build Phases tab
3. Add a Copy Files phase
4. Select Products Directory as the Destination
5. Drag all Carthage-supplied frameworks in from the project navigator's frameworks group
6. Clean and re-build the project, open the project playground and start playing

Here's how the new Copy Files phase should look:

![Screenshot of Xcode project target settings that fix the Carthage Playground Driven Development issue](/assets/2019-02-09-playground-driven-development-and-carthage-003.png)

We're done. Playground Driven Development with Xcode and Carthage should now work. 💫

![Screenshot of Xcode Playgrounds working with Carthage after applying the fix](/assets/2019-02-09-playground-driven-development-and-carthage-002.png)

[^1]: The [master](https://github.com/ksm/Habits/tree/master) branch has a self-contained Xcode project with working PDD. The [carthage](https://github.com/ksm/Habits/tree/carthage) branch installs Carthage and shows the problem (you still have to run `carthage bootstrap`). The fix is on [carthage-fix](https://github.com/ksm/Habits/tree/carthage-fix).

*[PDD]: Playground Driven Development
