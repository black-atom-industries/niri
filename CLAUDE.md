# Black Atom Niri Adapter

## Overview

This is a Black Atom adapter for the Niri Wayland compositor. It generates partial KDL configuration files that can be included in the main niri config.

## Commands

- Generate themes: `black-atom-core generate` (run from this directory)

## Project Structure

```
niri/
├── black-atom-adapter.json     # Adapter configuration
├── themes/
│   ├── default/
│   │   └── collection.template.kdl
│   ├── jpn/
│   ├── stations/
│   ├── terra/
│   └── mnml/
└── README.md
```

## Template Format

Templates use Eta syntax and generate partial KDL configs for niri's `include` directive:

```kdl
overview {
    backdrop-color "<%= theme.ui.bg.default %>"
}

layout {
    focus-ring {
        active-color "<%= theme.ui.fg.accent %>"
        inactive-color "<%= theme.ui.fg.subtle %>"
    }
}
```

## Theme Properties Used

- `theme.meta.label` - Human-readable theme name
- `theme.ui.bg.default` - Background color
- `theme.ui.fg.accent` - Accent/active color
- `theme.ui.fg.subtle` - Subtle/inactive color
- `theme.palette.red` - Urgent/error color

## Niri Include Feature

Niri v25.11+ supports `include` which allows splitting config into multiple files. The generated themes are designed to be included and will override the color settings in the main config.

Key behaviors:
- Included files are watched and trigger live-reload on changes
- Settings merge with main config (later settings override earlier ones)
- Works only at top level of config (not inside sections)
