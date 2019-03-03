# Unique Image Variations

A module for ProcessWire CMS/CMF. Ensures that all ImageSizer options and focus settings affect image variation filenames.

![uiv](https://user-images.githubusercontent.com/1538852/53693222-4a5d5c80-3e02-11e9-8e1f-b96a3fb3eecf.png)

## Background

When using methods that produce image variations such as `Pageimage::size()`, ProcessWire includes some of the ImageSizer settings (height, width, cropping location, etc) in the variation filename. This is useful so that if you change these settings in your `size()` call a new variation is generated and you see this variation on the front-end.

However, ProcessWire does not include several of the other ImageSizer settings in the variation filename:
* upscaling
* cropping, when set to false or a blank string
* interlace
* sharpening
* quality
* hidpi quality
* focus (whether any saved focus area for an image should affect cropping)
* focus data (the top/left/zoom data for the focus area)

This means that if you change any of these settings, either in `$config->imageSizerOptions` or in an `$options` array passed to a method like `size()`, and you already have variations at the requested size/crop, then ProcessWire will not create new variations and will continue to serve the old variations. In other words you won't see the effect of your changed ImageSizer options on the front-end until you delete the old variations.

## Features

The Unique Image Variations module ensures that any changes to ImageSizer options and any changes to the focus area made in Page Edit are reflected in the variation filename, so new variations will always be generated and displayed on the front-end.

## Installation

[Install](http://modules.processwire.com/install-uninstall/) the Unique Image Variations module.

In the module config, set the ImageSizer options that you want to include in image variation filenames.

## Warnings

Installing the module (and keeping one or more of the options selected in the module config) will cause all existing image variations to be regenerated the next time they are requested. If you have an existing website with a large number of images you may not want the performance impact of that. The module is perhaps best suited to new sites  where image variations have not yet been generated.

Similarly, if you change the module config settings on an existing site then all image variations will be regenerated the next time they are requested.

If you think you might want to change an ImageSizer option in the future (I'm thinking here primarily of options such as interlace that are typically set in `$config->imageSizerOptions`) and would *not* want that change to cause existing image variations to be regenerated then best to not include that option in the module config after you first install the module.
