# BMW of El Cajon

![BMW of El Cajon](https://github.com/toddcf/bmw-el-cajon/assets/img/2019-x7/overhead-helipad/1268x499-min.jpg "BMW of El Cajon")

### Technology Used

- HTML5
- CSS3
- Foundation 5.5.3
- Photoshop CC 2018

## Techniques

### BMW Button Hover Effects

BMW has very specific marketing guidelines for everything, including their buttons. The specs call for a very specific linear gradient from top to bottom, which transitions to a solid color when hovered over.

The problem with this is that CSS does not allow transitions for gradients, so this BMW mandate results in a brief flash of white background when the button is first hovered over -- hardly the classy look and feel we are going for.

So I put a lot of work into figuring out a way to achieve the same effect smoothly, and since no one will probably ever notice otherwise, here it is:

#### HTML

```
<a class="bmw-primary-btn-link" href="#">
  <div class="bmw-primary-btn-wrapper">
    <div class="bmw-primary-btn">Pre-Order Today</div>
  </div>
</a>
```

#### CSS

```
.bmw-primary-btn-wrapper {
  display: block;
  position: relative;
  width: 191px; /* BMW mandate */
  height: 51px; /* BMW mandate */
  background: -webkit-gradient(linear, left top, left bottom, from(rgba(28,98,197,1)), color-stop(50%, rgba(28,105,211,1)), color-stop(100%, rgba(28,105,211,1)), to(rgba(255,255,255,1)));
  background: -webkit-linear-gradient(top, rgba(28,98,197,1) 0%, rgba(28,105,211,1) 50%, rgba(28,105,211,1) 100%, rgba(255,255,255,1) 100%);
  background: -o-linear-gradient(top, rgba(28,98,197,1) 0%, rgba(28,105,211,1) 50%, rgba(28,105,211,1) 100%, rgba(255,255,255,1) 100%);
  background: linear-gradient(to bottom, rgba(28,98,197,1) 0%, rgba(28,105,211,1) 50%, rgba(28,105,211,1) 100%, rgba(255,255,255,1) 100%); /* BMW mandate */
  background-position: left top;
  background-size: 100% 200%;
  cursor: pointer;
  -webkit-transition: all .2s ease;
  -o-transition: all .2s ease;
  transition: all .2s ease;
}

.bmw-primary-btn {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%,-50%);
      -ms-transform: translate(-50%,-50%);
          transform: translate(-50%,-50%);
  font-weight: bold;
  font-size: 14px; /* BMW mandate */
  text-transform: uppercase; /* BMW mandate */
  color: #fff; /* BMW mandate */
  width: 100%;
  text-align: center;
}

.bmw-primary-btn-wrapper:hover,
.bmw-primary-btn-wrapper:active,
.bmw-primary-btn-wrapper:focus {
  background-color: transparent;
  background-position: left bottom;
  color: #fff;
}
```

Essentially, there is a background for the button that is twice the size of the displayed button.

The background has a linear gradient, but the color change stops at the halfway point, and then becomes a solid color for the other half.

That background is positioned so that you only see the half with the color change by default. When you hover, the position switches to display the half with the solid color.

And then I've added a transition, so that the background is essentially "sliding" upon hover, giving it the appearance of a smooth change from a linear gradient to a solid color.

### Subtle H1 Gradient

On the [BMW Series 8 page](https://www.google.com), the white H1 font sometimes winds up overlaying the bright white lights in the background image, depending on screen size.

To combat this, I added a very subtle linear gradient background to the text that goes from transparent on the top, to a 20% opacity black in the center, to transparent again on the bottom. Hopefully you don't notice it -- but the text becomes readable as a result.

#### HTML

`<h1 id="marquee-headline"><span class="shaded">New BMW 8 Series</span></h1>`

#### CSS

```
.shaded {
    background: -webkit-gradient(linear, left top, left bottom, from(rgba(0,0,0,0)), color-stop(rgba(0,0,0,0.2)), to(rgba(0,0,0,0)));
    background: -webkit-linear-gradient(rgba(0,0,0,0), rgba(0,0,0,0.2), rgba(0,0,0,0));
    background: -o-linear-gradient(rgba(0,0,0,0), rgba(0,0,0,0.2), rgba(0,0,0,0));
    background: linear-gradient(rgba(0,0,0,0), rgba(0,0,0,0.2), rgba(0,0,0,0));
  }
  ```