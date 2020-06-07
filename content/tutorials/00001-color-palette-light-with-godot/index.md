---
title: "Color palette light with Godot"
date: 2020-06-07T03:29:50-03:00
description: "Create a light in Godot using only color palette's colors"
tags: [tutorials, gamedev, godot, light, shader, pico-8, lospec]
authors: [jc]
---

![Original image](assets/pico-8-palette-example-kingdom-of-nerea-in-pico-8-by-davit-masia.png)

## Color palette light, what?

When you use a regular Light2D, Godot just increments the pixels' RGB values, whitening everything that is enlightened.

![Regular light](regular_light2d.png)

If you create your own light shader, you control every light and shadow color, and every pixel will be in your color palette, it makes your game more consistent.

![Color palette light](thumbnail.png)


## Create the project

First you need to create a new project in Godot, using GLES3.

![Create new project](create_new_project.png)


## Download the assets

For this tutorial we will be using the [PICO-8 color palette](https://lospec.com/palette-list/pico-8), so please download the [assets file](assets.zip) and decompress it into the project's folder.

[assets.zip](assets.zip) contains a folder called "assets" with the following images:

- [pico-8-palette-example-kingdom-of-nerea-in-pico-8-by-davit-masia.png](assets/pico-8-palette-example-kingdom-of-nerea-in-pico-8-by-davit-masia.png) (Lospec's PICO-8 example image)
- [light.png](assets/light.png)
- [pico-8_light.png](assets/pico-8_light.png)

Now your project's file structure must look like this:

![Project's file structure](file_structure.png)

Reimport all 3 image assets as 2D Pixel.

![Reimport as 2D Pixel](reimport_2d_pixel.png)


## Create the scene

Create a new 2D Scene and add the [Lospec's PICO-8 example image](assets/palette-list/pico-8-palette-example-kingdom-of-nerea-in-pico-8-by-davit-masia.png) to the tree and add a new Light2D.

![Project tree](project_tree.png)

Then assign [light.png](assets/light.png) as Light2D texture, and put its mode as Mix.

![Light2D properties](light2d_properties.png)


## Assign the shader

Select the "pico-8-palette-example-kingdom-of-nerea-in-pico-8-by-davit-masia" Node and assign a new ShaderMaterial and new Shader to it.

![ShaderMaterial](shader_material.png)

![Shader](shader.png)

Copy and paste the shader code:

```c
shader_type canvas_item;

// Godot color palette light shader
// Author: Juan Colacelli
// Website: https://juancolacelli.com
// License: GNU GPLv3

uniform sampler2D color_palette;
uniform bool dark_mode = false;

vec4 getColorByMode(int index, int mode) {
  return texelFetch(color_palette, ivec2(index, mode), 0);
}

vec4 getColor(int index) {
  return getColorByMode(index, 1);
}

vec4 getLightColor(int index) {
  return getColorByMode(index, 2);
}

vec4 getDarkColor(int index) {
  return getColorByMode(index, 0);
}

int getColorPaletteIndex(vec4 color_to_find) {
  for (int i = 0; i < textureSize(color_palette, 0).x; i++) {
    if (color_to_find == getColor(i)) {
        return i;
    }
  }

  return -1;
}

void fragment() {
  vec4 pixel = texture(TEXTURE, UV);
  int color_palete_index = getColorPaletteIndex(pixel);

  if (color_palete_index > -1) {
    vec4 light_color = getLightColor(color_palete_index);
    vec4 dark_color = getDarkColor(color_palete_index);

    if (AT_LIGHT_PASS) {
      if (dark_mode) {
        COLOR = pixel
      } else {
        COLOR = light_color
      }
    } else {
      if (dark_mode) {
        COLOR = dark_color;
      } else {
        COLOR = pixel;
      }
    }
  } else {
    COLOR = vec4(1.0, 1.0, 0.0, 1.0);
  }
}
```

Now your Shader will have a new param called "Color Palette", assign [pico-8_light.png](assets/pico-8_light.png) to it.

![Shader param](shader_param.png)

The shader will search the original color index, and replace it with its equivalent light or shadow color.

## Enjoy your new light!

![Light mode](light_mode.png)

If you want to use the dark mode, enable in the shader's params.

![Dark mode param](dark_mode_param.png)

![Dark mode](dark_mode.png)

## How does the shader work?

"Color Palette" param has one image wich contains the original color palette color, and its light and shadow equivalences.

![PICO-8 equivalences](pico-8_light_big.png)


## Explore new options

If you change the "Color Palette" param for another image, you can use other palettes, or i.e an [B/W style light image](assets/pico-8_palette_bw.png).

![B/W mode](bw_mode.png)


## Source code

View full project source code on: [GitLab](https://gitlab.com/juancolacelli/juancolacelli.com_tutorials/-/tree/master/00001-color-palette-light-with-godot)
