---
title: Introduction to SVG Ripper
subtitle: Ultimate tool to use SVGs in your projects
tags: svg, svgripper, svg-optimization
domain: huly.blog
---

Past weekends I did work on website for Hardcore Engineering. Done in with Astro in minimalistic style I was excited to see four 100s in Lighthouse. So I started to think what I can optimize more here, just for fun.

It was really clear that World Map SVG is the biggest part of the website. I downloaded free version from [Sitemaps](https://www.amcharts.com/svg-maps/), and it was 150K. I do not need more deailed map, because use it just for fun effect, but I belive some people deal with SVGs of megabytes.

So that nice Sunday, I was first think to gzip it and decompress on the client with ligtweight library such as [pako]() or [tiny-inflate](https://github.com/foliojs/tiny-inflate), but that does not makes a lot of sense, since most HTTP servers and client browers exchange data in compressed format. So I started to think about _real_ SVG optimization.

I was never interested in nature of SVG files, so I dig into it. Basically SVG file is a set of operations (commands), like `M 0 0 L 100 100` which means "move to 0,0 and draw line to 100,100". So vast majority of SVG file is just this commands and coordinates.

Another importand aspect is that coordinates can be absolute or relative (to last point). Cool guys who invented SVG format, made things nice and type of coordinates is defined by command (upper-case commands use absolute coordinates, and lower-case commands use relative ones). So output of `M 50 50 L 60 60` is the same as output of `M 50 50 l 10 10`.

It's very common situation when same command is repeated may times, so we can avoid specifying command and use last one when command omitted. Basically `l 10 10 l 2 -2` can be written as `l 10 10 2 -2`.

Outcome of this research is that most of SVG content is data which follow this pattern [CMD [X, Y]...], so we need to store this data in very efficient way. So the idea of `SVG Ripper` was born.

## SVG Ripper

Vector graphics is good in that term that it does not matter how big you want to render final image. However if I render SVG in small size, such as 32x32 (consider rendering world map in such size), many operations will be `NOOP`s, since they will draw something inside single pixel.

So I want not only compess SVG data in very efficient way, but also optimize them removing all unnecesary data.

SVG files numbers are not arbitraty, but values from range defined by SVG file's `viewbox`. Absolute ones within viewbox and relative coordinates are likely within some smaller range, but also can't go ouside of viewbox.

(I'm not SVG expert, maybe it's allowed to draw ouside and then get back inside, but I will just generate error messages for such cases)

When SVG will be rendered, each coordinate will point to some pixel on the screen, so it does not make sense to have them in range more than 8192x8192. This is enough to render any SVG file on 8K displat at higest quality possible. So, in the worst case we need 13 bits for each coordinate.

In real life, almost nobody wants to render SVG on whole 8K screen. For example at Hardcore Engineering website, I render world map in 800 pixels width, and do not need more. However, I want it to be perfectly renedered on Retina displays, or even better displays in future. Retina display has 2x resolution, so I need 1600 pixels width, or 2400 for cooler monitors.

So these result in some default settings for SVG Ripper. By deafult SVG Ripper will optimze SVG files for 8192x8192 viewbox, and it needs 13 bits for each coordinate. However, you can change these settings if you want to render SVG in smaller size, or you want to use less memory decreasing rendering precision.

## World Map SVG

Let me use World Map SVG as example. It's 150K, and I want to see how much I can optimize it with SVG Ripper. World Map SVG viewbox is 2000x857, and for my case I do not need more than 800 pixels width (or 1600 pixels on Retnia). This means I need 686 pixels vertically. So we need 11 bits maximum for X coordinate, and 10 bits for Y coordinate.

Another important aspect that we still want to be vector graphics, and we do not covert SVG to raster image. By limiting bits to store coordinates, we just limit precision of rendering, but not the quality of image. So we can still render SVG in any size, but with less precision. We also preserve subpixel data but will precision selected by user.

For example if you choose 11 bits precision for 1024 wide viewport, SVGRipper will be able to keep 1/2 of pixel precision. If you choose 12 bits for the same viewport, it will be 1/4 of pixel precision. So you will be able to render such SVG on 4K display without any loss of quality.

```
l minX -0.2 maxX 0.3 minY -0.5 maxY 0.4 dX 0.50 dY 0.90 len 6
l minX -0.2 maxX 0.3 minY -0.3 maxY 0.3 dX 0.50 dY 0.60 len 4
l minX -0.5 maxX 0.3 minY -0.7 maxY 0.6 dX 0.80 dY 1.30 len 11
l minX -0.4 maxX 0.4 minY -0.1 maxY 0.1 dX 0.80 dY 0.20 len 4
l minX -0.1 maxX 0.1 minY -0.2 maxY 0.1 dX 0.20 dY 0.30 len 4
l minX -0.5 maxX 0.4 minY -0.5 maxY 0.8 dX 0.90 dY 1.30 len 9
l minX -0.4 maxX 0.6 minY -0.3 maxY 0.2 dX 1.00 dY 0.50 len 7
l minX -0.4 maxX 1.2 minY -0.5 maxY 0.6 dX 1.60 dY 1.10 len 12
l minX -0.2 maxX 0.1 minY -0.2 maxY 0.2 dX 0.30 dY 0.40 len 4
l minX -0.1 maxX 0.1 minY -0.2 maxY 0.1 dX 0.20 dY 0.30 len 4
l minX -0.6 maxX 0.6 minY -0.5 maxY 0.9 dX 1.20 dY 1.40 len 22
l minX -0.3 maxX 0.5 minY -0.7 maxY 0.6 dX 0.80 dY 1.30 len 15
l minX -0.9 maxX 0.5 minY -0.6 maxY 0.6 dX 1.40 dY 1.20 len 24
```

```
l minX -18.5 maxX 26.3 minY -7.2 maxY 5.8 dX 44.80 dY 13.00 len 131
l minX -3.5 maxX 7.2 minY -5.2 maxY 7.2 dX 10.70 dY 12.40 len 34
l minX -3.7 maxX 4.7 minY -5.4 maxY 5.8 dX 8.40 dY 11.20 len 39
```

## SVGRipper Process

So keeping all these in mind, let's define the process of SVG Ripper.

### Normazlie Coordinates

First we need to normilize SVG file. Based on number of bits we want to use for X and for Y coordinates, we need to calculate X and Y scale factors.

For example if I have 2000x857 viewbox, we need to rescale coordinates to 2048x1024 viewbox. This would normazie coordinates without loosing quality (we still use floating point numbers). So X-scale will be 2048/2000 any Y will be 1024/857. This is very straightforward operation:

```typescript
const scale = (values: Coord[], factorX: number, factorY: number) =>
  values.map(([x, y]) => [x * factorX, y * factorY]);
```

```
M minX 590.7 maxX 606.7 minY 76.8 maxY 85.8 dX 16.0 dY 9.0 len 11 	5	4
M minX 358.2 maxX 735.8 minY 65.6 maxY 277.6 dX 377.7 dY 212.0 len 289 	9	8
M minX 520.2 maxX 588.8 minY 57.0 maxY 87.2 dX 68.6 dY 30.2 len 45 	7	5
M minX 582.9 maxX 592.4 minY 55.0 maxY 60.5 dX 9.5 dY 5.5 len 6 	4	3
M minX 686.4 maxX 703.6 minY 54.2 maxY 60.6 dX 17.2 dY 6.3 len 11 	5	3
M minX 639.9 maxX 742.6 minY 54.0 maxY 131.7 dX 102.7 dY 77.7 len 73 	7	7
M minX 595.5 maxX 622.7 minY 53.8 maxY 69.7 dX 27.2 dY 15.9 len 15 	5	5
```

## SVGRipper Encoding Format

After all observations we can define encoding format for SVG Ripper. Basically, it will be a stream of commands and coordinates. Initially, for experiments I will use 2 bits per command, since World Map SVG uses only `M`, `m`, `l`, and `z`. Actaually they also use `Z`, but since Z command do not assume any coordinates, they are equivalent. So we can use 2 bits for command encoding.

After command written we should decide how we will stream coordinates. Let's write down some options:

- There is single coordinate after the command.
- There are many coordinates after the command.

So let's use 1 bit for this infomation. 0 will mean single coordinate, and 1 will mean many coordinates. For single coordinate we will use all X bits for X and all Y bits for Y, which we defined at quality decision point.

For many coordinates, we need to specify ()
