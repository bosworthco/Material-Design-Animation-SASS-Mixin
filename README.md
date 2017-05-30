Material-Design-Animation-SASS-Mixin
======
SASS Mixin based 100% on the Google Material Design animation specifications located here:
https://www.google.com/design/spec/motion/duration-easing.html
https://www.google.com/design/spec/motion/movement.html

## Usage
```CSS
.MyElement {
  @include transition(deceleration, width);
}
```
or simply
```CSS
.MyElement {
  @include transition(standard);
}
```

## Mixin
```SASS
/*************************************
  $ANIMATION
**************************************
* Created by James Bosworth - Based on Google Material Design Spec
* https://www.google.com/design/spec/motion/duration-easing.html
* https://www.google.com/design/spec/motion/movement.html
*
* USAGE:
* @include transition(deceleration, width);
* or just
* @include transition(standard);
*/

$standard-curve:      cubic-bezier(0.4, 0.0, 0.2, 1);
$deceleration-curve:  cubic-bezier(0.0, 0.0, 0.2, 1);
$acceleration-curve:  cubic-bezier(0.4, 0.0, 1, 1);
$sharp-curve:         cubic-bezier(0.4, 0.0, 0.6, 1);

@mixin transition($name: null, $property: all) {
  @if $name != null {
    // Standard curve
    // This is the most common easing curve. Objects quickly accelerate and
    // slowly decelerate between on-screen locations. It applies to growing
    // and shrinking material, among other property changes
    @if $name == standard {
      transition: $property 200ms $standard-curve;

      @media #{$tablet} {
        transition: $property 275ms $standard-curve;
      }
      @media #{$desktop} {
        transition: $property 300ms $standard-curve;
      }
      @media #{$widescreen} {
        transition: $property 375ms $standard-curve;
      }
    }

    // Deceleration curve (“Easing out”)
    // Objects enter the screen at full velocity from off-screen and
    // slowly decelerate to a resting point. During deceleration,
    // objects may scale up either in size (to 100%) or opacity (to 100%).
    // In some cases, when objects enter the screen at 0% opacity,
    // they may slightly shrink from a larger size upon entry.
    @else if $name == deceleration {
      transition: $property 225ms $deceleration-curve;

      @media #{$tablet} {
        transition: $property 295ms $deceleration-curve;
      }
      @media #{$desktop} {
        transition: $property 325ms $deceleration-curve;
      }
      @media #{$widescreen} {
        transition: $property 395ms $deceleration-curve;
      }
    }

    // Acceleration curve (“Easing in”)
    // Objects leave the screen at full velocity. They do not decelerate when off-screen.
    // They accelerate at the beginning of the animation and may scale down in
    // either size (to 0%) or opacity (to 0%). In some cases, when objects leave
    // the screen at 0% opacity, they may also slightly scale up or down in size.
    @else if $name == acceleration {
      transition: $property 195ms $acceleration-curve;

      @media #{$tablet} {
        transition: $property 225ms $acceleration-curve;
      }
      @media #{$desktop} {
        transition: $property 275ms $acceleration-curve;
      }
      @media #{$widescreen} {
        transition: $property 300ms $acceleration-curve;
      }
    }

    // Sharp curve
    // The sharp curve is used by objects that may return to the screen at any time.
    // Objects may quickly accelerate from a starting point on-screen, then quickly
    // decelerate in a symmetrical curve to a resting point immediately off-screen.
    // The deceleration is faster than the standard curve since it doesn't follow an
    // exact path to the off-screen point. Objects may return from that point at any time.
    @else if $name == sharp {
      transition: $property 300ms $sharp-curve;

      @media #{$tablet} {
        transition: $property 325ms $sharp-curve;
      }
      @media #{$desktop} {
        transition: $property 375ms $sharp-curve;
      }
      @media #{$widescreen} {
        transition: $property 395ms $sharp-curve;
      }
    }
  }
}
```

## Assumptions
You will need to have your breakpoints namespaced for use as variables, e.g. `@media #{$tablet} {}` if not, replace `#{$tablet}` with your media queries directly.

### Notes
*Please note: This is an experiment and although it's awesome and works perfectly, it generates a shitload lot of CSS so you may want to reduce the specificity for use in any production websites.*

### MIT License

> Copyright (c) 2017 James Bosworth

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
