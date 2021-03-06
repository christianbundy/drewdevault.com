---
date: 2015-06-14
# vim: tw=80
title: osu!web - WebGL & Web Audio
layout: post
tags: [games, osu]
---

<script src="/js/underscore-min.js"></script>

I've taken a liking to a video game called [osu!](https://osu.ppy.sh) over the
past few months. It's a rhythm game where you use move your mouse to circles
that appear with the beat, and click (or press a key) at the right time. It
looks something like this:

<iframe src="https://www.youtube.com/embed/qdaZnQQAPqQ" frameborder="0" allowfullscreen></iframe>

The key of this game is that the "beatmaps" (a song plus notes to hit) are
user-submitted. There are thousands of them, and the difficulty curve is very
long - I've been playing for 10 months and I'm only maybe 70% of the way up the
difficulty curve. It's also a competitive game, which leads to a lot more fun,
where each user tries to complete maps a little bit better than everyone else
can. You can see on the left in that video - this is a very good player who
earned the #1 rank during this play.

In my tendency to start writing code related to every game I play, I've been
working on a cool project called [osu!web](http://www.drewdevault.com/osuweb).
This is a Javascript project that can:

* Decompress osu beatmap archives
* Decode the music with Web Audio
* Decode the osu! beatmap format
* Play the map!

In case you don't have any osz files hanging around, try out [this
one](https://sr.ht/f30.osz), which is the one from the video above.

![](https://sr.ht/044.png)

## osu!web and the future

This part of the blog post is for non-technical readers, mostly osu players.
osu!web is pretty cool, and I want to make it even better. My current plans are
just to make it a beatmap viewer, and I'm working now on achieving that goal. I
have to finish sliders and add spinners, and eventually work on things like
storyboards. Playing background videos is not in the cards because of
limitations with HTML5 video.

Eventually, I'd like to make it possible to link to a certain time in a certain
map, or in a certain replay. Oh yeah, I want to make it support replays, too.
If I get replays working, though, then I don't see any reason not to let players
try the maps out in their web browsers, too. Keep an eye out!

## Technical Details

This project is only possible thanks to a whole bunch of new web technologies
that have been stabilizing in the past year or so. The source code is [on
Github](https://github.com/SirCmpwn/osuweb) if you want to check it out.

### Loading beatmaps

When the user [drags and
drops](https://github.com/SirCmpwn/osuweb/blob/gh-pages/scripts/scenes/need-files.js#L8-L41)
an osz file, we use [zip.js](https://github.com/gildas-lormeau/zip.js) and
create a virtual filesystem of sorts to browse through the archive. In this
archive we have several things:

* A number of "tracks" - osu files that define notes and such for various
    difficulties
* The song (mp3) and optionally a video background (avi)
* Assets - a background image and optionally a skin (like a Minecraft texture
    pack)

![](https://sr.ht/ce6.png)

We then load the *.osu files and decode them. They look similar to ini files or
Unix config files. Here's a snippet:

    [General]
    AudioFilename: MuryokuP - Sweet Sweet Cendrillon Drug.mp3
    AudioLeadIn: 1000
    PreviewTime: 69853

    # snip

    [Metadata]
    Title:Sweet Sweet Cendrillon Drug
    TitleUnicode:Sweet Sweet Cendrillon Drug
    Artist:MuryokuP
    ArtistUnicode:MuryokuP
    Creator:Smoothie
    Version:Cendrillon

    # snip

    [HitObjects]
    104,308,1246,5,0,0:0:0:0:
    68,240,1553,1,0,0:0:0:0:
    68,164,1861,1,0,0:0:0:0:
    104,96,2169,1,0,0:0:0:0:
    172,60,2476,2,0,P|256:48|340:60,1,170,0|0,0:0|0:0,0:0:0:0:
    404,104,3399,5,0,0:0:0:0:
    
    # snip

This is decoded by
[osu.js](https://github.com/SirCmpwn/osuweb/blob/gh-pages/scripts/osu.js). For
some sections (like `[Metadata]`), it just puts each entry into a dict that you
can pull from later. It does more for things like hit objects, and understands
which of these lines is a slider versus a hit circle versus a spinner and so on.

I sneakily loaded a beatmap in the background in your browser as you were
reading. If you want to check it out, open up your console and play with the
`track` object. Ignore all the disqus errors, they're irrelevant.

![](https://sr.ht/a81.png)

## Enter stage: Web Audio

Web Audio had a bit of a rocky development cycle, what with Chrome thinking it's
special and implementing a completely different standard from everyone else.
Things have [settled](http://caniuse.com/#feat=audio-api) by now, and I can
start playing with it 😁 Bonus: Mozilla finally added mp3 support to all
platforms, including Linux (which my dev machine runs).

The osz file includes an mp3, which we
[extract](https://github.com/SirCmpwn/osuweb/blob/gh-pages/scripts/osu.js#L209-L224)
into an ArrayBuffer, and
[load](https://github.com/SirCmpwn/osuweb/blob/gh-pages/scripts/osu-audio.js)
into a Web Audio context. This is super cool and totally would not have been
possible even a few months ago - kudos to the teams implementing all this
exciting stuff in the browsers.

That's about all we're doing with Web Audio right now. I do add a gain node so
that you can control the volume with your mouse wheel. In the future, we can get
more creative by:

* Adding support for HT/DT mods
* Adding support for NC

## Enter stage: PIXI

Once we've decoded the beatmap and loaded the audio, we can play it. After
briefly showing the user a difficulty selection, we jump into rendering the map.
For this, I've decided to use [PIXI.js](http://pixijs.com/), which gives us a
really nice API to use on top of WebGL with a canvas fallback for when WebGL is
not available. I was originally just using canvas, but it wasn't very
performant, so I went looking for a 2D WebGL framework and found PIXI. It's
pretty cool.

First, we iterate over all of the hit objects on the beatmap and generate
sprites for them:

```js
this.populateHit = function(hit) {
    // Creates PIXI objects for a given hit
    hit.objects = [];
    hit.score = -1;
    switch (hit.type) {
        case "circle":
            self.createHitCircle(hit);
            break;
        case "slider":
            self.createSlider(hit);
            break;
    }
}

for (var i = 0; i < this.hits.length; i++) {
    this.populateHit(this.hits[i]); // Prepare sprites and such
}
```

This is all done before we start playing. We consider the timestamp in the music
that the hit is scheduled for, and then we place *all* of the hit objects into
an array and start the song. See code for
[createHitCircle](https://github.com/SirCmpwn/osuweb/blob/gh-pages/scripts/scenes/playback.js#L88-L143),
which puts together a bunch of sprites for each hit cirlce and sets their alpha
to zero. See also
[createSlider](https://github.com/SirCmpwn/osuweb/blob/gh-pages/scripts/scenes/playback.js#L145-L228),
which is more complicated (I'll go into detail later).

Each frame, we get the current time from the Web Audio layer, and we run a
function that updates a list of upcoming hit objects:

```js
this.updateUpcoming = function(timestamp) {
    // Cache the next ten seconds worth of hit objects
    while (current < self.hits.length
        && futuremost < timestamp + (10 * TIME_CONSTANT)) {
        var hit = self.hits[current++];
        for (var i = hit.objects.length - 1; i >= 0; i--) {
            self.game.stage.addChildAt(hit.objects[i], 2);
        }
        self.upcomingHits.push(hit);
        if (hit.time > futuremost) {
            futuremost = hit.time;
        }
    }
    for (var i = 0; i < self.upcomingHits.length; i++) {
        var hit = self.upcomingHits[i];
        var diff = hit.time - timestamp;
        var despawn = NOTE_DESPAWN;
        if (hit.type === "slider") {
            despawn -= hit.sliderTimeTotal;
        }
        if (diff < despawn) {
            self.upcomingHits.splice(i, 1);
            i--;
            _.each(hit.objects, function(o) {
                self.game.stage.removeChild(o);
                o.destroy();
            });
        }
    }
}
```

I adopted this pattern early on for performance reasons. During each frame's
rendering step, we only have the sprites and such loaded for hit objects in the
near future. This saves a lot of time. PIXI has all of these sprites loaded and
draws them for us each frame. During each frame, all we have to do is update
them:

```js
this.updateHitObjects = function(time) {
    self.updateUpcoming(time);
    for (var i = self.upcomingHits.length - 1; i >= 0; i--) {
        var hit = self.upcomingHits[i];
        switch (hit.type) {
            case "circle":
                self.updateHitCircle(hit, time);
                break;
            case "slider":
                self.updateSlider(hit, time);
                break;
            case "spinner":
                //self.updateSpinner(hit, time); // TODO
                break;
        }
    }
}
```

This is passed in the current timestamp in the song, and based on this we are
able to do some simple math to calculate how much alpha each note should have,
as well as the scale of the approach circle (which tells you when to click the
note):

```js
this.updateHitCircle = function(hit, time) {
    var diff = hit.time - time;
    var alpha = 0;
    if (diff <= NOTE_APPEAR && diff > NOTE_FULL_APPEAR) {
        alpha = diff / NOTE_APPEAR;
        alpha -= 0.5; alpha = -alpha; alpha += 0.5;
    } else if (diff <= NOTE_FULL_APPEAR && diff > 0) {
        alpha = 1;
    } else if (diff > NOTE_DISAPPEAR && diff < 0) {
        alpha = diff / NOTE_DISAPPEAR;
        alpha -= 0.5; alpha = -alpha; alpha += 0.5;
    }
    if (diff <= NOTE_APPEAR && diff > 0) {
        hit.approach.scale.x = ((diff / NOTE_APPEAR * 2) + 1) * 0.9;
        hit.approach.scale.y = ((diff / NOTE_APPEAR * 2) + 1) * 0.9;
    } else {
        hit.approach.scale.x = hit.objects[2].scale.y = 1;
    }
    _.each(hit.objects, function(o) { o.alpha = alpha; });
}
```

I've left out sliders, which again are pretty complicated. We'll get to them
after you look at this screenshot again:

![](https://sr.ht/044.png)

All of these hit objects are having their alpha and approach circle scale
adjusted each frame by the above method. Since we're basing this on the
timestamp of the map, a convenient side effect is that we can pass in any time
to see what the map should look like at that time.

## Curves

The hardest thing so far has been rendering sliders, which are hit objects that
you're meant to click and hold as you move across the "slider". They look like
this:

![](https://sr.ht/c97.png)

The golden circle is the area you need to keep your mouse in if you want to pass
this slider. Sliders are defined as a series of curves. There are a few kinds:

* Linear sliders (not curves)
* Catmull sliders
* Bezier sliders

For now I've only done bezier sliders. I give many thanks to
[opsu](https://github.com/itdelatrisu/opsu), which I learned a lot of useful
stuff about sliders from. Each slider is currently generated using the
now-deprecated "peppysliders" method, where the sprite is repeated along the
curve several times. If you look carefully as a slider fades out, you can notice
that this is the case.

![](https://sr.ht/787.png)

The newer style of sliders involves rendering them with a custom shader. This
should be possible with PIXI, but I haven't done any research on them yet.
Again, I expect to be able to draw a lot of knowledge from reading the opsu
source code.

I left out the initializer for sliders earlier, because it's long and
complicated. I'll include it here so you can see how this goes:

```js
this.createSlider = function(hit) {
    var lastFrame = hit.keyframes[hit.keyframes.length - 1];
    var timing = track.timingPoints[0];
    for (var i = 1; i < track.timingPoints.length; i++) {
        var t = track.timingPoints[i];
        if (t.offset < hit.time) {
            break;
        }
        timing = t;
    }
    hit.sliderTime = timing.millisecondsPerBeat *
        (hit.pixelLength / track.difficulty.SliderMultiplier) / 100;
    hit.sliderTimeTotal = hit.sliderTime * hit.repeat;
    // TODO: Other sorts of curves besides LINEAR and BEZIER
    // TODO: Something other than shit peppysliders
    hit.curve = new LinearBezier(hit, hit.type === SLIDER_LINEAR);
    for (var i = 0; i < hit.curve.curve.length; i++) {
        var c = hit.curve.curve[i];
        var base = new PIXI.Sprite(Resources["hitcircle.png"]);
        base.anchor.x = base.anchor.y = 0.5;
        base.x = gfx.xoffset + c.x * gfx.width;
        base.y = gfx.yoffset + c.y * gfx.height;
        base.alpha = 0;
        base.tint = combos[hit.combo % combos.length];
        hit.objects.push(base);
    }
    self.createHitCircle({ // Far end
        time: hit.time,
        combo: hit.combo,
        index: -1,
        x: lastFrame.x,
        y: lastFrame.y,
        objects: hit.objects
    });
    self.createHitCircle(hit); // Near end
    // Add follow circle
    var follow = hit.follow =
        new PIXI.Sprite(Resources["sliderfollowcircle.png"]);
    follow.visible = false;
    follow.alpha = 0;
    follow.anchor.x = follow.anchor.y = 0.5;
    follow.manualAlpha = true;
    hit.objects.push(follow);
    // Add follow ball
    var ball = hit.ball = new PIXI.Sprite(Resources["sliderb0.png"]);
    ball.visible = false;
    ball.alpha = 0;
    ball.anchor.x = ball.anchor.y = 0.5;
    ball.tint = 0;
    ball.manualAlpha = true;
    hit.objects.push(ball);

    if (hit.repeat !== 1) {
        // Add reverse symbol
        var reverse = hit.reverse =
            new PIXI.Sprite(Resources["reversearrow.png"]);
        reverse.alpha = 0;
        reverse.anchor.x = reverse.anchor.y = 0.5;
        reverse.x = gfx.xoffset + lastFrame.x * gfx.width;
        reverse.y = gfx.yoffset + lastFrame.y * gfx.height;
        reverse.scale.x = reverse.scale.y = 0.8;
        reverse.tint = 0;
        // This makes the arrow point back towards the start of the slider
        // TODO: Make it point at the previous keyframe instead
        var deltaX = lastFrame.x - hit.x;
        var deltaY = lastFrame.y - hit.y;
        reverse.rotation = Math.atan2(deltaY, deltaX) + Math.PI;

        hit.objects.push(reverse);
    }
    if (hit.repeat > 2) {
        // Add another reverse symbol
        var reverse = hit.reverse_b
            = new PIXI.Sprite(Resources["reversearrow.png"]);
        reverse.alpha = 0;
        reverse.anchor.x = reverse.anchor.y = 0.5;
        reverse.x = gfx.xoffset + hit.x * gfx.width;
        reverse.y = gfx.yoffset + hit.y * gfx.height;
        reverse.scale.x = reverse.scale.y = 0.8;
        reverse.tint = 0;
        var deltaX = lastFrame.x - hit.x;
        var deltaY = lastFrame.y - hit.y;
        reverse.rotation = Math.atan2(deltaY, deltaX);
        // Only visible when it's the next end to hit:
        reverse.visible = false;

        hit.objects.push(reverse);
    }
}
```

As you can see, there are many more moving pieces here. The important part is
the curve:

```js
hit.curve = new LinearBezier(hit, hit.type === SLIDER_LINEAR);
for (var i = 0; i < hit.curve.curve.length; i++) {
    var c = hit.curve.curve[i];
    var base = new PIXI.Sprite(Resources["hitcircle.png"]);
    base.anchor.x = base.anchor.y = 0.5;
    base.x = gfx.xoffset + c.x * gfx.width;
    base.y = gfx.yoffset + c.y * gfx.height;
    base.alpha = 0;
    base.tint = combos[hit.combo % combos.length];
    hit.objects.push(base);
}
```

In the [curve
code](https://github.com/SirCmpwn/osuweb/tree/gh-pages/scripts/curves), a
series of points along each curve are generated for us to place sprites at.
These are precomputed like all other hit objects to save time during playback.
However, the render updater is still quite complicated:

```js
this.updateSlider = function(hit, time) {
    var diff = hit.time - time;
    var alpha = 0;
    if (diff <= NOTE_APPEAR && diff > NOTE_FULL_APPEAR) {
        // Fade in (before hit)
        alpha = diff / NOTE_APPEAR;
        alpha -= 0.5; alpha = -alpha; alpha += 0.5;

        hit.approach.scale.x = ((diff / NOTE_APPEAR * 2) + 1) * 0.9;
        hit.approach.scale.y = ((diff / NOTE_APPEAR * 2) + 1) * 0.9;
    } else if (diff <= NOTE_FULL_APPEAR && diff > -hit.sliderTimeTotal) {
        // During slide
        alpha = 1;
    } else if (diff > NOTE_DISAPPEAR - hit.sliderTimeTotal && diff < 0) {
        // Fade out (after slide)
        alpha = diff / (NOTE_DISAPPEAR - hit.sliderTimeTotal);
        alpha -= 0.5; alpha = -alpha; alpha += 0.5;
    }

    // Update approach circle
    if (diff >= 0) {
        hit.approach.scale.x = ((diff / NOTE_APPEAR * 2) + 1) * 0.9;
        hit.approach.scale.y = ((diff / NOTE_APPEAR * 2) + 1) * 0.9;
    } else if (diff > NOTE_DISAPPEAR - hit.sliderTimeTotal) {
        hit.approach.visible = false;
        hit.follow.visible = true;
        hit.follow.alpha = 1;
        hit.ball.visible = true;
        hit.ball.alpha = 1;

        // Update ball and follow circle
        var t = -diff / hit.sliderTimeTotal;
        var at = hit.curve.pointAt(t);
        var at_next = hit.curve.pointAt(t + 0.01);
        hit.follow.x = at.x * gfx.width + gfx.xoffset;
        hit.follow.y = at.y * gfx.height + gfx.yoffset;
        hit.ball.x = at.x * gfx.width + gfx.xoffset;
        hit.ball.y = at.y * gfx.height + gfx.yoffset;
        var deltaX = at.x - at_next.x;
        var deltaY = at.y - at_next.y;
        if (at.x !== at_next.x || at.y !== at_next.y) {
            hit.ball.rotation = Math.atan2(deltaY, deltaX) + Math.PI;
        }

        if (diff > -hit.sliderTimeTotal) {
            var index = Math.floor(t * hit.sliderTime * 60 / 1000) % 10;
            hit.ball.texture = Resources["sliderb" + index + ".png"];
        }
    }

    if (hit.reverse) {
        hit.reverse.scale.x = hit.reverse.scale.y = 1 + Math.abs(diff % 300) * 0.001;
    }
    if (hit.reverse_b) {
        hit.reverse_b.scale.x = hit.reverse_b.scale.y = 1 + Math.abs(diff % 300) * 0.001;
    }
    _.each(hit.objects, function(o) {
        if (_.isUndefined(o._manualAlpha)) {
            o.alpha = alpha;
        }
    });
}
```

Much of this is the same as the hit circle updater, since we have a similar hit
circle at the start of the slider that needs to update in a similar fashion.
However, we also have to move the rolling ball and the follow circle along the
slider as the song progresses. This involves calling out to the curve code to
figure out what point is (`current_time / slider_end`) along the length of the
slider. We put the ball there, and we also ask for the point at (`(current_time +
0.01) / slider_end`) and make the ball rotate to face that direction.

## Conclusions

That's the bulk of the work neccessary to make an osu renderer. I'll have to add
spinners once I feel like the slider code is complete, and a friend is working
on adding hit sounds (sound effects that play when you correctly hit a note).
The biggest problem he's facing is that Web Audio has no good solution for
low-latency audio playback. On my side of things, though, everything is going
great. PIXI was a really good choice - it's an easy to use API and the WebGL
frontend is fast as hell. osu!web plays a map with performance that compares to
the performance of osu! native.

<script src="/js/osu.js"></script>

<script>
var xhr = new XMLHttpRequest();
xhr.open("GET", "/example.osu");
xhr.onload = function() {
    window.track = new Track(xhr.responseText);
    window.track.decode();
};
xhr.send();
</script>

