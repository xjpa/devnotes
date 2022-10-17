---
layout: post
title: Building a high performance financial web application with JavaScript - JS Monthly
description: A short summary of one team's journey to run a real-time financial calculation engine in the browser using JavaScript. Buffet style (as in food, not Warren) presentation with something for everyone - React & Redux, V8 optimisations, monads and evolving simple design.
summary: A short summary of one team's journey to run a real-time financial calculation engine in the browser using JavaScript. Buffet style (as in food, not Warren) presentation with something for everyone - React & Redux, V8 optimisations, monads and evolving simple design.
comments: true
tags: [javascript, webdev, finance]
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/EPhArG3It18" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

note: still havent finished watching it yet, i stopped at 15:42

- talk link: [https://youtu.be/EPhArG3It18](https://youtu.be/EPhArG3It18)

- Google's lighthouse test shouldnt have you bothered: [https://developers.google.com/web/tools/lighthouse](https://developers.google.com/web/tools/lighthouse)

- Understand if it's a CPU bounded problem or not. Ask yourself: "what is bounding your problem?" Most performance optimisation begins with this

- CPU bounded problem can be given to web worker, especially in NodeJS it is single threaded. With that, we move it into a separate thread and that separate thread is in the web worker

- What is CPU bounded problem?

"your program will only go faster if you get more CPUs"

or if you make that program run faster on CPUs you have

meaning that you can buy a lot more RAM but your program will still perform the same because the problem is in the CPU, rather than in other resources like for example besides more RAM it could be a faster network/faster speed to download/render webpage resources, but that still wouldnt solve your problem if it's CPU bounded

- Like for example, their CPU bounded is 500-1000 Redux actions per second, XYZ-many computations per second

## JavaScript is faster than you thought

- "JIT optimised languages come with caveats"

  - by JIT, we mean that JS gets loaded and compiled to byte code then to C. Meaning behind the scenes, the code gets sped up, gets compiled into fast machine code and this happens "on the fly "which is why it is called JIT or "just in time." In comparison to C++ they compiled to machine code, super optimizde by that point and never goes to that intermediate step. JIT happens meanwhile when you run the code

- A problem with JIT would be this

a V8 accidentally broke react: [https://ponyfoo.com/articles/javascript-performance-pitfalls-v8](https://ponyfoo.com/articles/javascript-performance-pitfalls-v8)

- Depending on your project's dependencies, the lower you go in terms of your architecture, the more relevant JIT flaws becomes

- Other challenges in JS

String representations: such as in the V8 engine, there are many different strings such as SeqString or SlicedString and all of them "have different performance characteristics"

from [https://github.com/v8/v8/blob/e483fb2731c13e811783bbb4bd2a70272027c15b/src/objects.h#L107-L124](https://github.com/v8/v8/blob/e483fb2731c13e811783bbb4bd2a70272027c15b/src/objects.h#L107-L124):

```
//       - String
//         - SeqString
//           - SeqOneByteString
//           - SeqTwoByteString
//         - SlicedString
//         - ConsString
//         - ThinString
//         - ExternalString
//           - ExternalOneByteString
//           - ExternalTwoByteString
//         - InternalizedString
//           - SeqInternalizedString
//             - SeqOneByteInternalizedString
//             - SeqTwoByteInternalizedString
//           - ConsInternalizedString
//           - ExternalInternalizedString
//             - ExternalOneByteInternalizedString
//             - ExternalTwoByteInternalizedString
```
