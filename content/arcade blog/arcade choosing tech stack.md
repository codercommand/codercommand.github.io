+++
title = 'Arcade: Choosing Tech Stack'
date = 2024-04-27
draft = false
+++

# Background

The original intention was to make Arcade in Unreal Engine 5 just like in the original demo [Demise]({{< ref "demise" >}}). This changed because after using Unreal Engine 5.1 for 2 years at Falmouth University I came to dislike the engine as a programmer. For designers and artists the engine is great, but the programming experience is terrible and Unreal Engine doesn't play nicely with Git version contol either.

When people complain about Unreal C++ it's normally the naming convention, lack of documentation, or Unreal's own versions of things from the C++ standard library. Those things are not that big of a problem. These are the problems:
1. Slow build times made it really hard to iterate and test code, same with the editor taking to long to open.
2. Functions took parameters that weren't used, examples of this are ShouldSkip from UMovementComponent and the Blueprint JSON plugin.
3. With each new feature Unreal adds, the engine gets more complicated. I don't mean in terms of more options to choose from, I mean you have to know how to write certain bits of code in a certain order which you can only learn by example or from a tutorial. Two examples are Enhanced Input and Mover 2.0.
4. Most of the big bugs in [Swamp Fell]({{< ref "swamp fell" >}}) had nothing to do with the games C++ or Blueprint code. The problems were with Unreal Engine itself. I had to make custom versions of SetInputMode (based on this tutorial [Problem with Set Input Mode Game Only node](https://superyateam.com/2019/10/01/problem-with-set-input-mode-game-only-node/)) because the default implementation has a bug that hasn't been fixed in over 5 years. Learning about the problem also took a few months because Google searching for the bug wasn't easy. I also had to make my own version of SpawnActor that allowed deferred spawning because of a UI bug with world space UI visibilty.

Because of these reasons I decided I wanted to use a different game engine. What I wanted was:
1. 3D Support.
2. Great programmer experience.
3. Engine API that's simple, doesn't have weird bugs, and doesn't force me to work with an overcomplicated framework. (If that means I must implement some things myself, I'm happy with that.)

After searching, [Bevy](https://bevyengine.org/) and [Unigine](https://unigine.com/) were the engines I belived matched what I wanted. I ignored [Unity](https://unity.com/) because I have never liked working in the engine and they had just tried doing the runtime fees. Considered [Godot](https://godotengine.org/) because I have enjoyed using it in the past, but I'm not a fan of the UI, the lack of multimonitor support, and I want to make the game in something more impessive for my portfolio to improve my employability.

I was planning on using Bevy since it appeared to cater to what I needed. Unigine wasn't viable because it lacks support for other platforms besides Linux and Windows.

# Changing to Heaps

On 26th April 2024 before I started coding the game I saw this tweet:

{{< twitter_simple user="LogLogGames" id="1783906189459202319" >}}

The [article](https://loglog.games/blog/leaving-rust-gamedev/) was very insightful, and some of the problems they had working in Rust were the same as the problems I had when using Unreal. Because of this I decided I hadn't found the right engine and I should look again. That night I found [Heaps](https://heaps.io/index.html) which ticked all the boxes for what I needed.

Over the next day I read what people were saying in response to the article ([Leaving Rust gamedev after 3 years](https://news.ycombinator.com/item?id=40172033)) and reflected on my own experience with Rust and Bevy though limited.

I decided the game client will be made in Heaps, and the server will be made using Rust with almost no dependencies.

Benefits of Heaps:
1. Windows, Linux, and console support.
2. Simple engine API.
3. Game engine is so simple you could read the source code and extend it yourself.
4. MIT licenced.
5. During development you can use a virtual machine instead of compiling, making it easy to test and iterate on changes.
6. Multiple successful 2D and 3D games released proving the engine can be used commercially and isn't a toy.

Benefit of server in Rust:
1. Unlikely to crash.
2. The server will be secure.
3. Efficient & fast.
4. Lower server costs.
