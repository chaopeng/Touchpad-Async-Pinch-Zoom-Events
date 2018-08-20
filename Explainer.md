# Problem

Currently, Chromium has performance issue when user pinch zoom on touchpad. The major performance issue is because Chromium sending the [blocking ctrl-wheel events](https://github.com/w3c/uievents/issues/31) when user pinch zoom on Touchpad.

We have fixed a similar issue for [mouse wheel/touchpad scrolling](https://groups.google.com/a/chromium.org/forum/#!topic/blink-dev/5jrqZmUBV9c). This feature introduce [async wheel events: Not all wheel events are cancellable](https://github.com/w3c/uievents/pull/171/files). 

# Proposal

Introduce async touchpad pinch events, if the wheel event of the first pinch zoom event is not prevented by JS, then we send the following wheel events of pinch event as no blocking and no-cancellable. If the wheel event of the first pinch zoom event is prevented, then we send the following wheel events of pinch event as blocking and cancellable.

[Design Doc](https://docs.google.com/document/d/1Mou2PDOHcWqCcNQ3p-PaGjJddDulF6uQh-MBmTYGcEw/edit?usp=sharing)
[Demo](http://chaopeng.me/Touchpad-Async-Pinch-Zoom-Events/demo.html)

Demo page is mocking js running heavy job on wheel handler. We can see it has huge pinch zoom latency without async touchpad pinch events.
