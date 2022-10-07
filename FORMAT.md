# AGS Theme Format
This document specifies the AGS theme JSON format and the changes from one version to the other.
Comments are allowed but should be avoided because they're not valid JSON.

## Compatibility
The new format is not retrocompatible, but old themes can be loaded fine on 3.6.0.36.

Adding new entries is always safe, since the Editor will ignore anything it doesn't know about.

It's possible to make a cross-version theme by using the old color format (r,g,b,a) for the 3.5 entries. New sections can be in any format.

## Changelog
- 3.6.0.36: New theme format (hex colors, fallbacks, import sprite button, and others)
- 3.5.0.31: Added link colors for WelcomePane
- 3.4.2: Custom themes were introduced

# Main sections
```
{
  "name": "Theme Name", // metadata, ignored by the Editor
  "version": "0.0.0", // metadata, ignored by the Editor
  "background": color,
  "global": {...} // (since 3.6.0.36) global styles used as fallbacks
  "main-container": {...} // main container and dockpanel skin
  "main-menu": {...}
  "tool-bar": {...}
  "status-strip": {...}
  "welcome": {...}
  "project-panel": {...}
  "properties-panel": {...}
  "output-panel": {...}
  "find-results-panel": {...}
  "call-stack-panel": {...}
  "general-settings": {...}
  "palette": {...}
  "sprite-selector": {...}
  "text-parser-editor": {...}
  "lip-sync-editor": {...}
  "gui-editor": {...}
  "inventory-editor": {...}
  "dialog-editor": {...}
  "view-editor": {...}
  "character-editor": {...}
  "view-preview": {...}
  "cursor-editor": {...}
  "font-editor": {...}
  "audio-editor": {...}
  "global-variables-editor": {...}
  "room-editor": {...}
  "script-editor": {...}
}
```

Note: All sections are optional when using AGS 3.6.0.36, but are required if targeting lower versions.
The `"global"` colors will be used as fallback where applicable, so it's not necessary to specify every single section if you're targeting 3.6.0.36 and above.


# Default types
## color
HTML String (since 3.6.0.36)
`string` must be a valid HTML color ("#fff", "#ffffff", "#ffffff00", "transparent", "red", etc)

Or the old-style definition (since 3.4.2)
```
{
  "r": int,
  "g": int,
  "b": int,
  "a": int,
}
```

`int` values must be within 0-255

## button
```
{
  "background": color,
  "foreground": color,
  "flat": {
    "style": int, // (FlatStyle) Flat = 0, Popup = 1, Standard = 2, System = 3
    "border": {
      "size": int,
      "color": color
    }
  }
}
```

## box
```
{
  "background": color,
  "foreground": color
}
```

## listview
```
{
  "background": color,
  "foreground": color,
  "owner-draw": bool,
  "grid-lines": bool,
  "last-column-width": int,
  "draw-item": bool,
  "draw-sub-item": bool,
  "column-header": {
    "background": color,
    "foreground": color,
    "border": color
  }
}
```

## combobox
```
{
  "background": color,
  "foreground": color,
  "drop-down": {
    "background": color,
    "foreground": color
  },
  "drop-down-closed": {
    "background": color,
    "foreground": color
  },
  "item-selected": {
    "background": color,
    "foreground": color
  },
  "item-not-selected": {
    "background": color,
    "foreground": color
  },
  "border": {
    "background": color
  },
  "button-dropped-down": {
    "background": color,
    "foreground": color
  },
  "button-not-dropped-down": {
    "background": color,
    "foreground": color
  }
}
```

If defined, all the above values must be specified.
Internally, the original ComboBox will be replaced with a CustomComboBox.

## propertygrid
```
{
  "background": color,
  "line": color,
  "category": color,
  "splitter": color, // since 3.6.0.36
  "view": {
    "background": color,
    "foreground": color,
    "border": color
  },
  "help": {
    "background": color,
    "foreground": color,
    "border": color
  }
}
```

Note: (3.4.2) "category" was once called "category-fore" in the specific case of "general-settings".


## text-box
```
{
  "background": color,
  "foreground": color,
  "border-style": int // (BorderStyle) None = 0, FixedSingle = 1, Fixed3D = 2
}
```

# Sections

## main-container
```
"main-container": {
  "dock-background": color,
  "background": color,
  "foreground": color,
  "skin": { // VS2005 Dockpanel theme only
    "auto-hide": {
      "tab-gradient": {
        "start": color,
        "end": color,
        "text": color
      },
      "dock-strip-gradient": {
        "start": color,
        "end": color
      }
    },
    "dock-pane": {
      "document-gradient": {
        "dock-strip-gradient": {
          "start": color,
          "end": color
        },
        "active-tab-gradient": {
          "start": color,
          "end": color,
          "text": color
        },
        "inactive-tab-gradient": {
          "start": color,
          "end": color,
          "text": color
        }
      },
      "tool-window": {
        "active-caption-gradient": {
          "start": color,
          "end": color,
          "text": color
        },
        "inactive-caption-gradient": {
          "start": color,
          "end": color,
          "text": color
        },
        "active-tab-gradient": {
          "start": color,
          "end": color,
          "text": color
        },
        "inactive-tab-gradient": {
          "start": color,
          "end": color,
          "text": color
        },
        "dock-strip-gradient": {
          "start": color,
          "end": color
        }
      }
    }
  }
}
```

`"skin"` definitions are only applicable to the VS2005 Dockpanel theme.


## main-menu
```
"main-menu": {
  "background": color
  "foreground": color,
  "border": color,
  "background-dropdown": color,
  "separator": color,
  "selected": {
    "gradient": {
      "begin": color,
      "end": color
    }
  },
  "pressed": {
    "gradient": {
      "begin": color,
      "middle": color,
      "end": color
    }
  },
  "item": {
    "border": color,
    "selected": color
  },
  "check": {
    "background": color,
    "foreground": color,
    "border": color,
    "selected": color,
    "pressed": color
  },
  "margin": {
    "gradient": {
      "begin": color,
      "middle": color,
      "end": color
    }
  }
}
```

## tool-bar
```
"tool-bar": {
  "background": color,
  "border": color,
  "separator": color,
  "selected-gradient": {
    "begin": color,
    "end": color
  },
  "overflow-gradient": {
    "begin": color,
    "middle": color,
    "end": color
  },
  "gradient": {
    "begin": color,
    "middle": color,
    "end": color
  },
  "grip": {
    "light": color,
    "dark": color
  }
}
```


## status-strip
```
"status-strip": {
  "background": color,
  "foreground": color
}
```


## welcome
```
"welcome": {
  "background": color,
  "foreground": color,
  "panel1": {
    "background": color,
    "foreground": color
  },
  "panel2": {
    "background": color,
    "foreground": color,
    "link": color // since 3.5.0.31
  },
  "pnlTipOfTheDay": {
    "background": color,
    "foreground": color,
    "link": color // since 3.5.0.31
  },
  "pnlRight": {
    "background": color,
    "foreground": color,
    "link": color // since 3.5.0.31
  }
}
```

## project-panel
```
"project-panel": {
  "background": color,
  "project-tree": {
    "background": color,
    "foreground": color,
    "line": color
  }
}
```

## properties-panel
```
"properties-panel": {
  "background": color,
  "combobox": combobox
  },
  "grid": propertygrid
}
```

## output-panel
```
"output-panel": listview
```

## find-results-panel
```
"find-results-panel": listview
```

## call-stack-panel
```
"call-stack-panel": listview
```

## general-settings
```
"general-settings": {
  "background": color,
  "foreground": color,
  "property-grid": propertygrid
}
```

## palette
```
"palette": {
  "background": color,
  "foreground": color,
  "color-finder": {
    "background": color,
    "foreground": color,
    "color-number-box": text-box,
    "btn-color-dialog": button
  },
  "palette-page": box,
  "draw-mode": int, // (TabDrawMode) Normal = 0, OwnerDrawFixed = 1
  "draw-item": {
    "background": {
      "selected": color,
      "not-selected": color
    },
    "foreground": color
  }
}
```

Note: old 3.4.2 themes had "group-box" entries inside "color-finder" and "palette-page", but were never used. Both page and groupbox share the same colors.

## sprite-selector
```
"sprite-selector": {
  "background": color,
  "foreground": color,
  "list": {
    "background": color,
    "foreground": color
  },
  "tree": {
    "background": color,
    "foreground": color,
    "line": color
  },
  "btn-import-new": button // since 3.6.0.36
}
```

## text-parser-editor
```
"text-parser-editor": {
  "background": color,
  "foreground": color,
  "box": box,
  "list-view": listview
}
```

## lip-sync-editor
```
"lip-sync-editor": {
  "background": color,
  "foreground": color,
  "text-boxes": text-box
}
```

## gui-editor
```
"gui-editor": {
  "background": color,
  "foreground": color
}
```

## inventory-editor
```
"inventory-editor": {
  "background": color,
  "foreground": color,
  "current-item-box": box,
  "left-box": box,
  "right-box": box
}
```

## view-editor
```
"view-editor": {
  "background": color,
  "foreground": color,
  "btn-delete-option": button,
  "btn-new-option": button,
  "btn-new-frame": button
}
```


## character-editor
```
"character-editor": {
  "background": color,
  "foreground": color,
  "box": box,
  "btn-make": button
}
```


## view-preview
```
  "view-preview": {
    "background": color,
    "foreground": color,
    "numeric-loop": {
      "background": color,
      "foreground": color
    },
    "numeric-frame": {
      "background": color,
      "foreground": color
    },
    "numeric-delay": {
      "background": color,
      "foreground": color
    }
  }
```

## cursor-editor
```
  "cursor-editor": {
    "background": color,
    "foreground": color,
    "box": box
  }
```

## font-editor
```
  "font-editor": {
    "background": color,
    "foreground": color,
    "box": box,
    "btn-import": button
    }
  }
```


## audio-editor
```
  "audio-editor": {
    "background": color,
    "foreground": color,
    "audio-type": box,
    "audio-clip-box": box,
    "btn-play": button,
    "btn-pause": button,
    "btn-stop": button
  }
```

## global-variables-editor
```
"global-variables-editor": {
  "background": color,
  "foreground": color,
  "box": {
    "background": color,
    "foreground": color
  },
  "list": {
    "background": color,
    "foreground": color,
    "owner-draw": true,
    "grid-lines": false,
    "last-column-width": -2,
    "draw-item": true,
    "draw-sub-item": true,
    "column-header": {
      "background": color,
      "foreground": color,
      "border": color
    }
  }
}
```

## room-editor
```
"room-editor": {
  "background": color,
  "foreground": color,
  "box": box,
  "buffered-panel": {
    "background": color,
    "foreground": color
  },
  "btn-change-image": button,
  "btn-delete": button,
  "btn-export": button,
  "combo-view-type": combobox, // note: this isn't a normal combobox anymore
  "combo-backgrounds": combobox
}
```


## script-editor
```
  "script-editor": {
    "background": color,
    "foreground": color,
    "combo-functions": combobox,
    "text-editor": {
      "global-default": {
        "background": color,
        "foreground": color
      },
      "default": {
        "background": color,
        "foreground": color
      },
      "word-1": {
        "background": color,
        "foreground": color
      },
      "word-2": {
        "background": color,
        "foreground": color
      },
      "identifier": {
        "background": color,
        "foreground": color
      },
      "comment": {
        "background": color,
        "foreground": color
      },
      "comment-line": {
        "background": color,
        "foreground": color
      },
      "comment-doc": {
        "background": color,
        "foreground": color
      },
      "comment-line-doc": {
        "background": color,
        "foreground": color
      },
      "comment-doc-keyword": {
        "background": color,
        "foreground": color
      },
      "comment-doc-keyword-error": {
        "background": color,
        "foreground": color
      },
      "number": {
        "background": color,
        "foreground": color
      },
      "regex": {
        "background": color,
        "foreground": color
      },
      "string": {
        "background": color,
        "foreground": color
      },
      "string-eol": {
        "background": color,
        "foreground": color
      },
      "operator": {
        "background": color,
        "foreground": color
      },
      "preprocessor": {
        "background": color,
        "foreground": color
      },
      "line-number": {
        "background": color,
        "foreground": color
      },
      "indent-guide": {
        "background": color,
        "foreground": color
      },
      "fold-margin": color,
      "fold-margin-hi": color,
      "marknum-folder": {
        "background": color,
        "foreground": color
      },
      "marknum-folder-end": {
        "background": color,
        "foreground": color
      },
      "marknum-folder-open": {
        "background": color,
        "foreground": color
      },
      "marknum-folder-open-mid": {
        "background": color,
        "foreground": color
      },
      "marknum-folder-mid-tail": color,
      "marknum-folder-sub": color,
      "marknum-folder-tail": color,
      //"selected": color, // since 3.4.2 - selected background color
      "selected": { // since 3.6.0.36
        "background": color,
        "foreground": color // use "transparent" to keep original color
      },
      //"caret": color  // since 3.4.2 - caret foreground color
      "caret": { // since 3.6.0.36
        "caret-fore": color,
        "caret-line-back": color,
        "caret-line-back-alpha": int // 0-255
      },
      "marker-breakpoint": { // since 3.6.0.36
        "background": color,
        "foreground": color
      },
      "marker-breakpoint2": { // since 3.6.0.36
        "background": color,
        "foreground": color
      },
      "current-statement": { // since 3.6.0.36
        "background": color,
        "foreground": color
      },
      "current-statement2": { // since 3.6.0.36
        "background": color,
        "foreground": color // use "transparent" to keep original color
      }
    }
  }
}
```

# Dockpanel themes

AGS 3.x uses the default VS2005 theme.
AGS 4.x (will) allow to change dockpanel theme between VS2005 and VS2015 variants (Blue, Dark, Light).

Only VS2005 allows to change themeable properties through `Skin`. Newer themes require compilation but can theoretically inherit colors from vstheme files.


# Developers
A set of convenience methods have been added to apply colors to common elements:

- `public void ControlHelper(Control control, string path)`
- `public void GroupBoxHelper(GroupBox box, string path)`
- `public void ButtonHelper(Button btn, string path)`
- `public void ListViewHelper(ListView lvw, string path)`
- `public bool ComboBoxHelper(ControlCollection ctrl, ref ComboBox cb, string path)`
- `public void PropertyGridHelper(PropertyGrid grid, string path)`
- `public void TextBoxHelper(TextBox textbox, string path)`

The `path` defines the specific declaration for that element, which will fall back to `"global"` styles if not found.

Fallbacks can be declared as `string[]` in order of priority when using one of the available methods from `ColorTheme.cs`, like `SetColor()`.

Search for `LoadColorTheme` to find examples of how various components have been themed.
