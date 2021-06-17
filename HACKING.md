## Summary

- To be able to use the latest/adequate version of Sass, install `dart-sass`.
- `meson install` will regenerate the CSS every time you modify the SCSS files.
- Note that Meson always builds out-of-tree, so the regenerated CSS files will
  appear in your builddir.
- Do not edit the PNG directly, edit the source SVG files and run `./render-assets.sh`.
- To be able to run `./render-assets.sh`, install `inkscape` and `optipng`.
- To change the colors of SVG files, use a text editor instead of a image editor.

## How to tweak the theme

### SCSS

Materia is a complex theme, so to keep it maintainable it's written and
processed in Sass, like the upstream Adwaita.

Here's a rundown of the "supporting" stylesheets, that are unlikely to be the
right place for a drive by stylesheet fix:

File | Description
:-- | :--
`_theme.scss` | Variables to allow easier definition of widget sizing/styling.
`_color-palette.scss` | Material Design color palette definitions. We don't recommend editing this unless Google updates the color scheme.
`_theme-color.scss` | Global color definitions. We keep the number of defined colors to a necessary minimum. It covers both the light variant and the dark variant.
`_public-colors.scss` | SCSS colors exported through GTK to allow for 3rd party apps color mixing.
`_drawing.scss` | Drawing helper mixings/functions to allow easier definition of widget drawing under specific context.
`_common.scss` | Actual definitions of style for each widget. This is where you are likely to add/remove your changes.

You can read about Sass on its [web page](http://sass-lang.com/documentation/).
Once you make your changes to the SCSS files, you can run `meson install`
to generate the final CSS files.

### SVG

In Materia, to keep it maintainable, SVG files are basically edited on
text-based. So if you just want to change the colors of SVG files, it is
recommended to use a **text editor** instead of a image editor.

Several SVG files are used to render the PNG assets. Once you make your changes
to the SVG files, run the `./render-assets.sh` script to render the PNG assets.

## How to change the color scheme

### Script

To easily change the color scheme, you can use the `change_color.sh` script (or
just use the [oomox](https://github.com/themix-project/oomox) app).

> Originally, `change_color.sh` and `scripts/*.sh` were implemented for oomox,
but you can also run it on the command line without the app.

> Note: This script doesn't support Chrome extensions for now.

For example, to change the color scheme to the previous Flat-Plat, run the
script as follows:

For `bash`:

```bash
./change_color.sh -o Flat-Plat <(echo -e "BG=F5F5F5\nFG=212121\nMATERIA_VIEW=FFFFFF\nMATERIA_SURFACE=FAFAFA\nHDR_BG=455A64\nHDR_FG=FFFFFF\nSEL_BG=42A5F5\n")
```

For `fish`:

```fish
./change_color.sh -o Flat-Plat (echo -e "BG=F5F5F5\nFG=212121\nMATERIA_VIEW=FFFFFF\nMATERIA_SURFACE=FAFAFA\nHDR_BG=455A64\nHDR_FG=FFFFFF\nSEL_BG=42A5F5\n" | psub)
```

### Manual

If you want to change the color scheme in more detail, edit the files where
colors are defined.

#### SCSS

- `src/_sass/_color-palette.scss`
- `src/_sass/_theme-color.scss`

#### SVG

- `src/gtk-3.0/assets.svg`
- `src/gtk-2.0/assets{,-dark}.svg`
- `src/cinnamon/assets/*.svg`
- `src/gnome-shell/assets{,-dark}/*.svg`
- `src/unity/*/*.svg`
- `src/xfwm4/xfwm4{,-dark,-light}/*.svg`
- `src/chrome/chrome-scrollbar{,-dark}/icons/*.svg`

> Note: Do not forget to run `./render-assets.sh` after changing the colors of
`src/gtk-3.0/assets.svg` and `src/gtk-2.0/assets{,-dark}.svg`.

#### Misc

- `src/gtk-2.0/gtkrc{,-dark,-light}`
- `src/metacity-1/metacity-theme-2{,-light}.xml`
- `src/xfwm4/xfwm4{,-dark,-light}/themerc`
- `src/chrome/chrome-theme{,-dark,-light}/manifest.json`

> Note: The colors of `manifest.json` are defined in RGB format, so you need to
convert your colors from HEX format to RGB format.

After all the steps, run `meson install` to rebuild the themes.

## Useful Links

### Upstream theme sources

- [GTK 4](https://gitlab.gnome.org/GNOME/gtk/tree/master/gtk/theme/Adwaita)
- [GTK 3](https://gitlab.gnome.org/GNOME/gtk/tree/gtk-3-24/gtk/theme/Adwaita)
- [GTK 2](https://gitlab.gnome.org/GNOME/gnome-themes-extra/tree/master/themes/Adwaita/gtk-2.0)
- [GNOME Shell](https://gitlab.gnome.org/GNOME/gnome-shell/tree/master/data/theme)
  - [Sass sources](https://gitlab.gnome.org/GNOME/gnome-shell-sass) (legacy)
- [Metacity](https://gitlab.gnome.org/GNOME/gnome-themes-extra/tree/gnome-3-14/themes/Adwaita/metacity-1) (legacy)

> For other upstream theme sources of apps/DEs, see the comments in the source code.

### Tips

- [Material Design Guidelines](https://www.material.io/guidelines/)
- [CSS Guidelines for Materia](https://github.com/nana-4/materia-theme/wiki/CSS-Guidelines)
- [The GTK Inspector](https://blog.gtk.org/2017/04/05/the-gtk-inspector/)
- [Theming in GTK 4](https://developer.gnome.org/gtk4/stable/theming.html)
- [Theming in GTK 3](https://developer.gnome.org/gtk3/stable/theming.html)
- [GTK 2 Theming Tutorial](https://wiki.gnome.org/Attic/GnomeArt/Tutorials/GtkThemes)
- [The Pixmap Engine](https://wiki.gnome.org/Attic/GnomeArt/Tutorials/GtkEngines/PixmapEngine)
- [Designing Metacity Themes](https://wiki.gnome.org/Attic/GnomeArt/Tutorials/MetacityThemes)
- [Unity/Theming](https://wiki.ubuntu.com/Unity/Theming)
- [Xfwm4 theme how-to](https://wiki.xfce.org/howto/xfwm4_theme)
- [Chrome Themes](https://developer.chrome.com/extensions/themes)
