# BMW of El Cajon

## Techniques Learned

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