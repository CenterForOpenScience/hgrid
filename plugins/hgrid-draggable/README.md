# hgrid-draggable.js (experimental)

Drag-and-drop support for hgrid.js.

## Dependencies

- jQuery
- HGrid >= 0.1.1

## Usage 

```html
<script src="hgrid.js"></script>
<script type="hgrid-draggable.js"></script>
```

```js
var draggable = new HGrid.Draggable({
  onDrag: function(event, items) {
    # ... 
  },
  onDrop: function(event, items, folder) {
    # ...
  }
  canDrag: function(item) {
    if (item.name === "Don't drag me") {
        return false;
    }
    return true;
  },
  acceptDrop: function(item, folder, done) {
    if (folder.name === 'Forbidden') {
      done('Cannot drop here');
    }
    done();
  }
});

// Make the name column draggable
HGrid.Col.Name.behavior = 'move';

var grid = new HGrid({
    # ...
})
grid.registerPlugin(draggable);

```


## Available Options

- `onDrag(event, items)`: Fired while items are being dragged
- `onDrop(event, items, folder)`: Fired when items are dropped into a folder.
- `canDrag(item)`: Returns whether an item can be dragged.
- `acceptDrop(item, folder, done)`: Validation function that is invoked when an item is dropped into a folder. `done` is a function that, if called with a string argument, raises the error message and prevents the drop from proceeding.
- `canAcceptDrop(folder)`: Returns whether a folder is a valid drop target.
- `rowMoveManagerOptions`: Additional options passed to the `Slick.RowMoveManager` constructor. Available options: ``cancelEditOnDrag``, ``proxyClass``, and ``guideClass``.
- `rowSelectionModelOptions`: Additional options passed to the `HGrid.RowSelectionModel` constructor. Available options: ``selectActiveRow``.


## TODO

- Fix drop position
- Make folders draggable
- Multiple selection


## Development

Requirements

- NodeJS
- Bower

```sh
$ npm install  # installs gulp + gulp plugins
$ bower install  # installs dependencies (e.g. HGrid, qUnit...)
```


### Running tests and building

Tests are run using the `gulp` build tool.

```sh
$ gulp
```

You can also start watch mode, which will build and run tests whenever a file is changed.

```sh
$ gulp watch
```


