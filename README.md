# duzhenlin-quill-audio-resize-module
A module for Quill rich text editor to allow audio to be resized.

## Usage

### install 
```javascript
npm i duzhenlin-quill-audio-resize-module
```

### Webpack/ES6

```javascript
import Quill from 'quill';
import AudioResize from 'quill-audio-resize-module';

Quill.register('modules/AudioResize', AudioResize);

const quill = new Quill(editor, {
    // ...
    modules: {
        // ...
        AudioResize: {
            // See optional "config" below
        }
    }
});
```

/!\ You also need to add CSS to disable pointer-events in the audio iframe while in editor mode to prevent

```css
.quill-editor iframe {
    pointer-events: none;
}
```

### Script Tag

Copy audio-resize.min.js into your web root or include from node_modules

```html
<script src="/node_modules/quill-audio-resize-module/audio-resize.min.js"></script>
```

```javascript
var quill = new Quill(editor, {
    // ...
    modules: {
        // ...
        AudioResize: {
            // See optional "config" below
        }
    }
});
```

/!\ You also need to add CSS to disable pointer-events in the audio iframe while in editor mode to prevent

```css
.quill-editor iframe {
    pointer-events: none;
}
```

### Config

For the default experience, pass an empty object, like so:
```javascript
var quill = new Quill(editor, {
    // ...
    modules: {
        // ...
        AudioResize: {}
    }
});

Functionality is broken down into modules, which can be mixed and matched as you like. For example,
the default is to include all modules:

```javascript
const quill = new Quill(editor, {
    // ...
    modules: {
        // ...
        AudioResize: {
            modules: [ 'Resize', 'DisplaySize', 'Toolbar' ]
        }
    }
});
```

Each module is described below.

#### `Resize` - Resize the audio

Adds handles to the audio's corners which can be dragged with the mouse to resize the audio.

The look and feel can be controlled with options:

```javascript
var quill = new Quill(editor, {
    // ...
    modules: {
        // ...
        AudioResize: {
            // ...
            handleStyles: {
                backgroundColor: 'black',
                border: 'none',
                color: white
                // other camelCase styles for size display
            }
        }
    }
});
```

#### `DisplaySize` - Display pixel size

Shows the size of the audio in pixels near the bottom right of the audio.

The look and feel can be controlled with options:

```javascript
var quill = new Quill(editor, {
    // ...
    modules: {
        // ...
        AudioResize: {
            // ...
            displayStyles: {
                backgroundColor: 'black',
                border: 'none',
                color: white
                // other camelCase styles for size display
            }
        }
    }
});
```

#### `Toolbar` - audio alignment tools

Displays a toolbar below the audio, where the user can select an alignment for the audio.

The look and feel can be controlled with options:

```javascript
var quill = new Quill(editor, {
    // ...
    modules: {
        // ...
        AudioResize: {
            // ...
            toolbarStyles: {
                backgroundColor: 'black',
                border: 'none',
                color: white
                // other camelCase styles for size display
            },
            toolbarButtonStyles: {
                // ...
            },
            toolbarButtonSvgStyles: {
                // ...
            },
        }
    }
});
```

#### `BaseModule` - Include your own custom module

You can write your own module by extending the `BaseModule` class, and then including it in
the module setup.

For example,

```javascript
import { Resize, BaseModule } from 'quill-audio-resize-module';

class MyModule extends BaseModule {
    // See src/modules/BaseModule.js for documentation on the various lifecycle callbacks
}

var quill = new Quill(editor, {
    // ...
    modules: {
        // ...
        AudioResize: {
            modules: [ MyModule, Resize ],
            // ...
        }
    }
});
```
