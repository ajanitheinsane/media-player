# Media Player [<img src="https://jonathantneal.github.io/media-player/logo.svg" alt="" width="90" height="90" align="right">][Media Player]

[![NPM Version][npm-img]][npm-url]
[![Linux Build Status][cli-img]][cli-url]

[Media Player] is a tiny, responsive, international, accessible, cross browser,
easily customizable media player written in plain vanilla JavaScript.

<p align="center">
  <img src="https://jonathantneal.github.io/media-player/screenshot.png" alt="Media Player Screenshot" width="400">
</p>

[Media Player] can be controlled with any pointer or keyboard, whether it’s to
play, pause, move across the timeline, mute, unmute, adjust the volume, enter
or leave fullscreen, or download the source.

<p align="center">
  <img src="toolbar-classes.png" alt="Diagram of Media Player" width="665" height="116">
</p>

[Media Player] is designed for developers who want complete visual control over
the component. It’s also for developers who want to hack at or extend the
player without any fuss. The player itself does all the heavy lifting; semantic
markup, accessibility management, language, fullscreen, text direction,
providing pointer-agnostic scrubbable timelines, and lots of other cool
sounding stuff.

<p align="center">
  <img src="time-classes.png" alt="Diagram of Time Slider" width="598" height="82">
</p>

## Usage

```bash
npm install --save mediaplayer
```

Import the library and create a new [Media Player] using any media element:

```js
import MediaPlayer from 'mediaplayer';

// get target from media with controls
const $target = document.querySelector('audio[controls], video[controls]');

// assign media player from target (all these options represent the defaults)
const player = new MediaPlayer(
  $target,
  {
    prefix: 'media',
    lang: {
      play: 'play',
      pause: 'pause',
      mute: 'mute',
      unmute: 'unmute',
      volume: 'volume',
      currentTime: 'current time',
      remainingTime: 'remaining time',
      enterFullscreen: 'enter fullscreen',
      leaveFullscreen: 'leave fullscreen',
      download: 'download'
    },
    svgs: {
      play: '#symbol-play',
      pause: '#symbol-pause',
      mute: '#symbol-mute',
      unmute: '#symbol-unmute',
      volume: '#symbol-volume',
      currentTime: '#symbol-currentTime',
      remainingTime: '#symbol-remainingTime',
      enterFullscreen: '#symbol-enterFullscreen',
      leaveFullscreen: '#symbol-leaveFullscreen',
      download: '#symbol-download'
    },
    dir: : 'ltr'
  }
);
```

The `prefix` is used before flat class names, which are otherwise:

```scss
.media-player {
  .media-media { /* video or audio element */ }

  .media-toolbar {
    .media-control.media-play {
      .media-symbol.media-play-symbol { /* play svg */ }
      .media-symbol.media-pause-symbol { /* pause svg */ }
    }

    .media-control.media-mute {
      .media-symbol.media-mute-symbol { /* mute svg */ }
      .media-symbol.media-unmute-symbol { /* unmute svg */ }
    }

    .media-text.media-current-time { /* plain text */ }
    .media-text.media-remaining-time { /* plain text */ }

    .media-slider.media-volume {
      .media-range.media-volume-range { /* full volume */ }
      .media-range.media-volume-meter { /* current volume */ }
    }

    .media-slider.media-time {
      .media-range.media-time-range { /* full duration */ }
      .media-range.media-time-meter { /* elapsed time */ }
    }

    .media-control.media-download {
      .media-symbol.media-download-symbol { /* download svg */ }
    }

    .media-control.media-fullscreen {
      .media-symbol.media-enterfullscreen-symbol { /* enter full screen svg */ }
      .media-symbol.media-leavefullscreen-symbol { /* leave full screen svg */ }
    }
  }
}
```

Note the convenience classes like `media-control`, `media-symbol`,
`media-slider`, `media-range` and `media-range-meter`. These make it easier to
style a group of controls or to add new controls.

The `lang` object is used to provide accessible labels to each control in any
language. Undefined labels will use English labels.

The `svgs`
object is used to assign an SVG sprite to each control. The `dir` string is
used to determine the text-flow of the component, and both left-to-right
(`ltr`) and right-to-left (`rtl`) modes are supported.

## Media Player Instance

All DOM generated by [Media Player] is easily accessible from its instance.

```js
new Media(mediaElement, options);
```

- `media`: the original media target
- `toolbar`: the toolbar containing all the media controls
- `play`: the play button
- `playSymbol`: the play image
- `pauseSymbol`: the pause image
- `mute`: the mute button
- `muteSymbol`: the image seen before clicking mute
- `unmuteSymbol`: the image used after clicking mute
- `currentTime`: the current time element
- `currentTimeText`: the current time text node
- `remainingTime`: the remaining time element
- `remainingTimeText`: the remaining time text node
- `time`: the time slider
- `timeRange`: the time slider range
- `timeMeter`: the time slider meter
- `volume`: the volume slider
- `volumeRange`: the volume slider range
- `volumeMeter`: the volume slider meter
- `download`: the download button
- `downloadSymbol`: the download image
- `enterFullscreenSymbol`: the full screen enter image
- `leaveFullscreenSymbol`: the full screen leave image

## Sliders

Volume and time controls sliders allow you to drag volume up or down and time
backward or forward. By default, these sliders work left-to-right, meaning that
dragging the slider to the right advances the control. When the component
detects a right-to-left environment, this automatically flips.

These control can be configured to work in any direction — right-to-left
(`rtl`), top-to-bottom (`ttb`), bottom-to-top (`btt`) — with the following
configuration:

```js
new MediaPlayer(audioElement, {
  volumeDir: 'btt', // (volume will drag bottom to top)
  timeDir: 'ttb' // (time will drag top to bottom)
});
```

## Accessibility

[Media Player] automatically assigns <strong>ARIA</strong> roles and labels to
its controls, which always reflect the present state of the media player.
Special slider roles are used for volume and time which are then given helpful
keyboard controls.

## Events

Three new events are dispatched by [Media Player]. `playchange`
dispatches whenever play or pause toggles. `timechange` dispatches more rapidly
than timeupdate. `canplaystart` dispatches the first time media can play
through.

## Demos

- [Standard Experience](https://jonathantneal.github.io/media-player/)
- [Right-To-Left Experience](https://jonathantneal.github.io/media-player/rtl.html)
- [Playlist Experience](https://jonathantneal.github.io/media-player/playlist.html)
- [Subtitled Experience](https://jonathantneal.github.io/media-player/subtitles.html)

## Keyboard Controls

### Spacebar, Enter / Return

When focused on the **play button** or the **timeline slider**, pressing the
**spacebar** or **enter / return** toggles the playback of the media.

When focused on the **mute button** or the **volume slider**, pressing the
**spacebar** or **enter / return** toggles the muting of the media.

### Arrows

When focused on the **play button** or the **timeline slider**, pressing the
**left arrow** or **right arrow** moves the timeline forward or backward. The
timeline moves by increments of 1 second, unless **shift** is also pressed,
in which case it moves by 10 seconds.

When focused on the **mute button** or the **volume slider**, pressing the
**left arrow** or **right arrow** moves the volume up or down. The volume moves
by increments of 1%, unless **shift** key is also pressed, in which case it
moves by 10%.

For `ltr` languages written from left to right (like English), the
**left arrow** moves the timeline backward or the volume down, and the
**right arrow** moves the timeline forward or the volume up.

For `rtl` languages written from right to left (like Hebrew or Arabic), the
**left arrow** moves the timeline forward or the volume up, and the
**right arrow** moves the timeline backward or the volume down.

**[RTL Demo]**

## Browser compatibility

[Media Player] works in all browsers supporting Audio, Video, and SVG elements.
This includes Chrome, Edge, Firefox, Internet Explorer 9+, Opera, and Safari 6+.
Older versions of Edge and Internet Explorer may need additional assistance
loading SVGs from an external URL.

## Licensing

[Media Player] and its icons use the CC0 “No Rights Reserved” license.

---

[Media Player] compiles as 2.52 kB of JS and 604 B of CSS (gzipped).

[Media Player]: https://github.com/jonathantneal/media-player

[npm-url]: https://www.npmjs.com/package/mediaplayer
[npm-img]: https://img.shields.io/npm/v/mediaplayer.svg
[cli-url]: https://travis-ci.org/jonathantneal/media-player
[cli-img]: https://img.shields.io/travis/jonathantneal/media-player.svg

[PostCSS Import]: https://github.com/postcss/postcss-import
[RTL Demo]: https://jonathantneal.github.io/media-player/rtl.html
