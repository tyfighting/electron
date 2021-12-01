Chrome comic (Chrome 架构，有助于理解electron)

- first, browsers need to be more stable. when you're writing an important email or editing a document, a browser crash a big deal.
- browsers also need ti be faster. they need to start faster, load pages faster, and for web apps, javascript itself can be a lot faster
- they need to be more secure. given what's known about mass browsers exploits, browsers need architectural changes to disadvantage malware.
- and we want browsers to find that sweet spot between too many features and too few, with a clean, simple and efficient user interface.
- finally, google chrome is a fully open source browser.
- we want others to adopt ideas from us just as we've adopted good ideas from others

part one: stability,testing and the multi-process architecture
- when we started this project. the gears guys were saying that one of the problems with browsers is that they're inherently single-threaded
- for example, once you have javascript executing, it's going to keep going, and the browser can't do anything else until javascript returns control to the browser.
- so develops write apis that are asynchronous and every now and then the browser locks up because javascript is hung up on something
- the gears guys were thinking about a multi-threaded browser, but that led us to talk about, well, instead of multiple threads what if we have multiple processes? each having its own memory and its own copy of the global data structures.
- we're applying the same kind of process isolation you find in modern operating systems
- so, separate processes rendering separate tabs.
- and now you have separate javascript threads as well.
- one tab can be busy, while you're still using all the others
- and if there's a browser bug in the renderer(and our experience is that it's almost impossible to eliminate all bugs), we still only lose the one tab.
