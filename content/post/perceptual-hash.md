---
date: "2019-02-05"
title: Consolidating images with perceptual hashing
type: post
---
I have a lot of photos spread out over multiple devices and platforms from over the years. These are pictures from Facebook, old camera photos, Google Photos and so on. And most of these are duplicates, copied from one device to several different platforms and backups, all with very subtle differences depending on what platform they have been processed by.

Most of these have some matter of export functions for photos. But it is still a manual and tedious process to sort and combine them to a single set of photos that includes everything but also does so without duplicates.

As a programmer, there are several ways of automating the process. The easiest one is to compare images, pixel by pixel, to find copies. But there are also smarter ways to do this.

The most common method of quickly comparing files is through the use of hashes. Hashes are a way of reducing large quantities of data, such as files, to smaller and more manageable chunks.

The only problem with this approach is that while cryptographic hashes are useful for quickly finding duplicates they are very volatile. What this means is that a small change in a large file will result in a completely different hash. Compare the two images of a tiny radiator below, the original and one with an artistic filter.

I have included the hash output of MD5, a common cryptographic hash function, below each image. While the images are almost identical the resulting hashes are very different.

{{< figure src="/media/radiator.jpg" alt="A tiny radiator I found many years ago" caption="MD5: 90de6b60e0dcdb92114166f1a9c7e821" >}}

{{< figure src="/media/painting.jpg" alt="A tiny radiator I found many years ago" caption="MD5: c4ef0980be39404ee2e81344aa185cc3" >}}

To make hashes feasible for fingerprinting images in this manner, an alternative hashing method is required. Perceptual hashing is a method where the goal is to specifically have differences in a medium reflected in the corresponding hash. This means that a small change in the source will also have a small impact on the corresponding hash. I have included the same images from above below but this time with their perceptual hashes.

{{< figure src="/media/radiator.jpg" alt="A tiny radiator I found many years ago" caption="pHash: 07070f471b033007" >}}

{{< figure src="/media/painting.jpg" alt="A tiny radiator I found many years ago" caption="pHash: 07070f471b073007" >}}

This makes the problem of finding duplicate images a lot simpler to solve with the use of programming. In cases where two images result in the same perceptual hash, we can safely assume it is the same image in different formats or with different dimensions and simply save the better one.
