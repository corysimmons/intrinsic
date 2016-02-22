# @include intrinsic(16, 9);

[![Bower](https://img.shields.io/bower/v/intrinsic.svg)]()

A simple mixin for easy intrinsic ratios.

### Why?
[Intrinsic ratios](http://alistapart.com/article/creating-intrinsic-ratios-for-video) are pretty sweet for making certain content responsive.
They're also pretty sweet for helping to mitigate page [reflow](https://developers.google.com/speed/articles/reflow) (something visitors really hate).

A lot of people use stuff like [FitVids.js](https://github.com/davatron5000/FitVids.js) to help make YouTube videos and such responsive, but
it seems pretty heavy-handed to use a JS lib for a simple CSS technique. It also obfuscates what's going on and people tend to just throw it in their
stack whenever they are embedding a YouTube video.

This approach combines Dave Rupert's (FitVids' author) [mixin approach](http://daverupert.com/2015/12/intrinsic-placeholders-with-picture) with
Matthijs Kuiper's [`&::before` approach](http://blog.learningspaces.io/flexible-cover-images-using-intrinsic-ratio) and sprinkles in the ability
to feed it your own ratios for various content and background-color while said content is loading.

### When should I use this?
Use it on embedded videos, maps, and pretty much anywhere you have an element with a standardized size (thumbnails, hero images, etc.) to help prevent
page reflow.

### Installation
- `bower install intrinsic`
- `@import 'bower_components/intrinsic/intrinsic';`

### Usage
**[CodePen Demo](http://codepen.io/corysimmons/pen/zrVWqQ?editors=1100)**<br>
Be sure to [throttle](http://elijahmanor.com/enhanced-chrome-emulation-tools/) your connection ("Regular 2G" is good) to see how how it looks in low-bandwidth settings.

```scss
.youtube {
  @include intrinsic(16, 9);
}

.bg-cover {
  @include intrinsic(16, 9);
  
  background: lighten(dodgerblue, 25%)  url(https://www.fillmurray.com/1600/900) center no-repeat;
  background-size: cover;
}
```

```html
<div class="youtube">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/JhHMJCUmq28" frameborder="0" allowfullscreen></iframe>
</div>

<div class="bg-cover"></div>
```

### Options
- `$x` - The width ratio (e.g. `16` in `16:9`).
- `$y` - The height ratio (e.g. `9` in `16:9`).
- `$bg` - The background color. Defaults to `darken(white, 5%)`. You need to manually add this to your `background` property if you use the background cover technique (see the example code).

**Note:** You can use fixed numbers but they'll get stripped. `intrinsic(1600px, 900px)` turns into `1600, 900`. This is because we can't divide fixed numbers like `1600px / 900px` (not even with `calc`).
