---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Optimize animation for better web page performance

Nowadays, all popular web browsers use the GPU to render parts of web pages, especially when animation is used. For example, an animation using the CSS's `transform` property performs much smoother than one using the `left` and `top` properties.

Using `transform: translateZ(0)` or `will-change: transform` has become something popular like how we used `zoom: 1` for IE6 some years ago. These little hacks tell web browsers to create a separate layer that will be rendered by the GPU. This behavior is called `compositing` in modern web browsers.

In this article, we will talk about the pros and cons of `compositing` and how to optimize it for better web page performance.

## Continuous repainting problem

Normally, when rendering a web page, the browser will paint it from the CPU and then send the final image to the GPU to display it on the screen. Therefore, if an animation is not prepared to be rendered by the GPU, the browser will continuously repaint the web page from the CPU for every animation frame and then send the result to the GPU for display.

Let's say we have a web page with 2 elements, `A` and `B`, which are positioned absolutely and each has a different `z-index`. If we move the `A` element by the `left` property with CSS animation, the browser has to recalculate the element's position for every animation frame, render an image of the new state of the web page, and then send it again to the GPU for display.

While modern browsers are smart enough to repaint only the changed area of the web page, continuous repainting still reduces the web page's performance and the animation is also not smooth, especially on a complex layout with a lot of content.

I've created a sample page to demo this behavior. [Click here to download the page](https://drive.google.com/file/d/1HYULt7U4HJ69RxCAt9jyXAWxRYB00mTd/view?usp=sharing) and import it into your PageFly app installation. Publish the imported page and open the live page with Chrome, you should see the document element is continuously repainted on the `Layers` panel of the Chrome DevTools similar to the image below.

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-03 at 11.07.13.png" alt=""><figcaption></figcaption></figure>

The continuous repainting problem occurs clearly like that because the animation I've created plays infinitely. You might not notice this problem if animations play just one time.

It would be better to repaint just the animation in a separate layer and then offset it over the entire page image without the animation. This behavior called `compositing` by modern web browsers and can be done entirely by the GPU.

To optimize the `compositing` using the GPU, the browser needs to ensure the following conditions:

* The animated CSS property does not affect the document flow.
* The animated CSS property does not depend on the document flow.
* The animated CSS property does not cause a repaint.

Currently, `transform` and `opacity` are the only properties that meet these conditions. For animations using other CSS properties, we can use the CSS `will-change` directive to force the browser to render the animation in a separate layer.

## Optimize animation using `will-change` directive

I have animated some images using the `left` property in the sample page above. To avoid the continuous repainting problem, I would use the `will-change` directive to move each animation to a separate layer.

You can [download the revised version of the sample page above](https://drive.google.com/file/d/1Gcvtd\_pV5347opaK-sHwH0NabCpVlbmt/view?usp=drive\_link) and import it into your PageFly app installation to see how the `will-change` directive works. As you can see on the `Layers` panel of the Chrome DevTools, the document element is no longer continuously repainted.

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-03 at 14.03.25.png" alt=""><figcaption></figcaption></figure>

Additionally, you will see a new layer containing only the animated element. If you scroll the web page down, you will see new layers being created every time new animations are scrolled into view. Layers of animations that are off the view will also be automatically removed.

This behavior occurs because I animate these elements by a property other than `transform` and `opacity`. Because of that, the animation is rendered dynamically by the CPU instead of being rendered permanently by the GPU. The use of `will-change` directive is to tell the browser that there will be changes in the `left` property so the browser can prepare ahead for rendering an animation.

Now, let's inspect and compare the performance of the web page before and after optimization. On the Chrome DevTools, click on the `Performance` tab and record about 3 seconds of an animation.

On the performance analysis result of the original sample page, you will see many paint events similar to the following image.

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-03 at 17.04.10.png" alt=""><figcaption></figcaption></figure>

`Paint` events are almost gone on the performance analysis result of the revised version of the sample page but there are still many `recalculate style` events as you can see in the image below.

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-03 at 17.11.31.png" alt=""><figcaption></figcaption></figure>

The continuous repainting problem has gone so we can stop here if the web page contains just a few animations and these animations don't play infinitely. On the other hand, we can optimize even further by rendering animations completely and permanently using the GPU.

## Optimize animations using `transform` property

We already know that `transform` and `opacity` are the only CSS properties that meet the conditions of not affecting the document flow, not depending on the document flow, and not causing a repaint. Therefore, only animations using these properties can be completely and permanently rendered by the GPU.

Let's optimize further animations on the sample page using the `transform` property instead of the `left` property. You can [download another revised version of the sample page](https://drive.google.com/file/d/1DnifZsF2UfD\_X4eCmx4F-zOCQRxVGeCc/view?usp=drive\_link) and import it into your PageFly app installation to see the difference. Publish the newly imported page, visit the live page, open the Chrome DevTools, and switch to the `Layers` tab, you should see several permanent layers similar to the following image.

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 10.40.57.png" alt=""><figcaption></figcaption></figure>

Let's see what the web page performance looks like now. Switch to the `Performance` tab and record about 3 seconds of an animation. You should see all events related to `reflow` and `repaint` actions have been gone.

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-04 at 11.01.46.png" alt=""><figcaption></figcaption></figure>

The web page performance is much better now. Besides, animations are also much smoother. But, the good thing is not free and we have to trade for it. In this case, the trade-off is the GPU memory consumption reserved by permanent animation layers.

Memory consumption should not be a problem on PCs having GPU usually bundled with GBs of RAM. But on mobile devices with limited GPU memory, especially on low to mid-end devices, the browser can lag, or even crash, when the memory is overflown.

## Optimize memory consumption

Storing an image in the GPU memory is the same as displaying an image on the screen, pixel by pixel. An image of a solid color with the dimensions of 800x600 pixel sizes less than 1KB when saved in PNG format. Guess its size when storing in the GPU memory.

To calculate its size in memory, we multiply its width by its height for the number of pixels, then multiply the result by 4 because every pixel is described by 4 bytes (1 byte for red color, 1 byte for green color, 1 byte for blue color, and 1 byte for the transparency). It is approximately 1.8MB when stored in GPU memory.

Thus, the only way to reduce the memory consumption of an animation layer is to reduce its dimension. Normally, human eyes would not see any difference if we reduce the dimension of an image by about 10% and then scale it up to the original dimension when displaying.

To do that, we can use `transform: scale(1.1)` when animating an element that is scaled down by 10%. You can [download the last revised version of the sample page](https://drive.google.com/file/d/1gz23YrSmgBM\_K2YX9y\_NYtQYOM7ffEG0/view?usp=drive\_link) and import it into your PageFly app installation to inspect how the memory consumption is optimized.

## Conclusion

Nowadays, almost all web pages have at least one animation. So, optimize animation for better web performance is a critical process.

Using `will-change` directive to optimize animation using CSS property other than `transform` and `opacity` can save GPU memory because layers only created when animations are scrolled into view and will be removed automatically when animations are off the view.

Using `transform` property to animate an element can result in much smoother animation because animations are initialized once on page load and permanently cached but the problem with GPU memory consumption pop up and might cause the browser to lag, or even crash, on mobile devices.

Last but not least, compositing a web page using layers also cause the browser to use more resources to organize and manage layers. So, overusing compositing layers should be avoided.

## References

* [Tricks for GPU Composited CSS](https://ariya.io/2014/02/tricks-for-gpu-composited-css)
* [CSS GPU Animation: Doing It Right](https://www.smashingmagazine.com/2016/12/gpu-animation-doing-it-right/)
* [When and how to use CSS will-change](https://blog.logrocket.com/when-how-use-css-will-change/)
* [On translate3d and layer creation hacks](https://aerotwist.com/blog/on-translate3d-and-layer-creation-hacks/)
