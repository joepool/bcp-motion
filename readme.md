# New Project

1. Copy project-01.txt, rename it (e.g. project-05.txt).
2. Fill in the fields below.
3. Open manifest.txt and add the new filename on its own line, wherever you want it to appear in the list.
4. Save. Reload the site (must be served over http, see note below).

## Fields

**filename**

the "file name" shown in the little top bar of the project card, e.g. brand-film.mp4. Optional — defaults to the title, slugified, with .mp4 on the end.

**title**

the project's display title.

**vimeo**

the numeric Vimeo video ID (the number in the video's URL, e.g. vimeo.com/1214386590 -> 1214386590).

**thumbnail**

path to an image shown behind the play button before the video loads, e.g. images/project-05/cover.jpg. Optional — leave blank to use the plain diagonal-stripe placeholder.

**subheading**

free text shown under the title, e.g. "lead motion designer · 30s brand film". Whatever you type here is displayed exactly as-is.

**tags**

comma-separated list of software/tools, e.g. "After Effects, Cinema 4D".

**description**

the paragraph shown under the title.

**process**

one image per line (repeat the "process:" line as many times as you need), OR a single comma-separated line. These populate the "process/" filmstrip. To put a Vimeo video in the strip instead of an image, see VIDEOS IN PROCESS/ASSET STRIPS below.

**asset**

same as above but for the "assets/" filmstrip. You can use "asset:" or "assets:" — both work, and both accept repeated lines or a comma list.

## Image Paths

Whatever you put after process:/asset: is used directly as the image src, so:

* "still_01.jpg"                -> looked up as images/still_01.jpg
* "images/project-05/still.jpg" -> used exactly as written
* "https://.../still.jpg"       -> used exactly as written (works fine for hosting stills externally too)

If an image path is wrong or the file doesn't exist, the tile now shows a "⚠ missing" label instead of silently looking blank, and the browser's console (right-click -> Inspect -> Console tab) will print the exact path it tried to load, e.g. "Image not found: http://.../images/still_01.jpg" — compare that against where the file actually sits to spot the mismatch. Common causes: the file is in a different folder than the path says, the extension doesn't match (.jpg vs .png), or the filename's capitalization differs (most static hosts are case-sensitive even if your computer isn't).

## Videos in process/asset strip

Any process: or asset: entry can be a Vimeo video instead of an image. Use this format in place of a filename:

```
vimeo:<video id>|<thumbnail path>|<label>
```

* <video id>        required — the numeric ID from the video's URL, same as the top-level "vimeo:" field.
* <thumbnail path>  optional — an image shown in the strip tile so it doesn't look like a blank tile with just a play icon. Same path rules as any other image (see IMAGE PATHS above). Leave blank to just show the play icon on the plain placeholder.
* <label>            optional — text shown on the tile and as the lightbox caption. Defaults to "vimeo <id>" if left out.

Examples:

```
process: vimeo:76979871|images/reel-thumb.jpg|reel_wip.mov
process: vimeo:76979871
asset: vimeo:76979871||bts clip
```

Clicking the tile opens the same popup used for images, but plays the Vimeo video in it instead. You can mix video and image entries freely within one process: or asset: strip.

## Development

This page loads project files with fetch(), which browsers block when you open index.html directly by double-clicking it (file://). To preview locally, run a tiny server from the site's root folder:

```
python3 -m http.server
```

...then visit http://localhost:8000 in your browser. Any real static host (GitHub Pages, Netlify, Vercel, Cloudflare Pages, etc.) serves files over http automatically, so this is only a local-preview quirk.
