# CarpurideLogoGenerator

Browser app that takes an image and creates a boot logo file (`isp_part.bin`) for Carpuride CarPlay / Android Auto displays. Everything runs locally in your browser, no image is uploaded anywhere.

> **This is a fork** of [domints/CarpurideLogoGenerator](https://github.com/domints/CarpurideLogoGenerator) by Dominik Szymański. It adds the **W602BS Pro** (6.2", 1080×540) and is hosted on GitHub Pages:
>
> **https://seppelp.github.io/CarpurideLogoGenerator/**
>
> Differences to upstream: W602BS Pro added to the model list, usage analytics removed, a short how-to on the page. Everything else, including the file format, is unchanged.

## Supported models

| Option in the app | Covers | Resolution |
| --- | --- | --- |
| W502 | 502 / 502B / 502Pro / 502B Pro / 502BS / 502H | 800×480 |
| W602BS Pro | 602BS / 602S Pro | 1080×540 |
| W701/W702/… | 701 / 702 / 702B / 702Pro / 702B Pro / 702BS / 702H / 712D / 702S Pro / 702RS Pro / 706 / 707 / 708 | 1024×600 |
| W901 | 901 / 101 / C3 / V9 / V3 | 1024×600 |
| W103 | 103 / 609 | 1280×480 |

Resolutions follow the [official Carpuride boot screen guide](https://carpuride.com/blogs/guide/carpuride-system-boot-screen-setup-guide).

**Not supported:** W603 / W603B / W603D, W903 / W905 (these expect a `boot_logo.jpg`, not a `.bin`) and C92 / C98 (`CARB3.img`). Models with 1600×600 or 1920×720 panels (W903 / W904 / V92R, W125A / W125S / W125P) are not in this fork's dropdown; see upstream PR [#7](https://github.com/domints/CarpurideLogoGenerator/pull/7).

## How to create and install a boot logo

### 1. Prepare the image

- Make the image **exactly** the resolution of your model (see table above). The app will warn you if it does not match; a wrong size gets cropped or padded with black, which rarely looks good.
- Use a static image (PNG or JPG). Animated formats are not supported by the device.
- Dark or black backgrounds usually look best, because the display edges are black anyway.

### 2. Generate the file

1. Open the app and pick your model in **Select model**. The glowing box is your display at its real pixel size.
2. Click **Upload image file or logo bin file** and choose your image. It is drawn onto the canvas.
3. Click **Download boot logo**. Your browser downloads a file named `isp_part.bin`.

The step is a little memory intensive. If the browser hangs, close other tabs or restart the browser and try again.

### 3. Put it on a USB stick

1. Format a USB stick as **FAT32** (FAT also works). Carpuride recommends a USB 3.0 stick of **32 GB or less**.
2. Copy `isp_part.bin` into the **root** of the stick.
3. Make sure it is the **only file** on the stick and that the name is **exactly** `isp_part.bin`. A second download often ends up as `isp_part(1).bin`, which the device will ignore.

### 4. Flash it on the device

1. Plug the stick into the USB port of your Carpuride unit while it is powered off.
2. Power the unit on. It detects the file, writes the new boot logo and usually shows a short confirmation.
3. Power off, remove the stick, power on again. Your logo should appear on boot.

### Checking an existing `isp_part.bin`

You can also upload an existing `isp_part.bin` (for example one you received from Carpuride support). The app shows its resolution and "magic" value and tells you whether it matches the selected model. It does not modify the file.

## Warranty

This software is provided **as is**, without any warranty. Flashing a boot logo with the wrong resolution or for the wrong model can leave your device in a bad state. Double-check the model and resolution before you flash, and keep the original file from Carpuride if you have one. Neither the upstream author nor the maintainer of this fork takes responsibility for damaged devices.

The tool is free for personal and community use. For commercial use please contact the upstream author (see the warranty dialog in the app).

## Development

```bash
npm ci
npm start        # dev server with live reload
npm run build    # production build into dist/
```

Pushes to `master` are built and deployed to GitHub Pages automatically by `.github/workflows/pages.yml`.

## License

MIT, see [LICENSE](LICENSE). Original work by Dominik Szymański ([domints](https://github.com/domints)).
