# Defining Modules

```js
var Apple = fruitmachine.define({
  name: 'apple',
  template: templateFunction,
  tag: 'section',
  classes: ['class-1', 'class-2'],

  // Event callbacks (optional)
  initialize: function(options){},
  setup: function(){},
  mount: function(){},
  teardown: function(){},
  destroy: function(){}
});
```

Define does two things:

- It registers a module internally for [Lazy](module-instantiation.md#lazy) module instantiation
- It returns a constructor that can be [Explicitly](module-instantiation.md#explicit) instantiated.

Internally `define` extends the default `fruitmachine.Module.prototype` with the parameters you define. Many of these parameters can be overwritten in the options passed to the constructor on a per instance basis. It is important you don't declare any parameters that conflict with `fruitmachine.Module.prototype` core API (check the [source]() if you are unsure).

### Options

- `name {String}` Your name for this module.
- `template {Function}` A function that will return the module's html (we like [Hogan](http://twitter.github.com/hogan.js/))
- `tag {String}` The html tag to use on the root element (defaults to 'div') *(optional)*
- `classes {Array}` A list of classes to add to the root element. *(optional)*
- `initialize {Function}` Define a function to run when the module is first instantiated (only ever runs once) *(optional)*
- `setup {Function}` A function to be run every time `Module#setup()` is called. You can safely assume the presence of `this.el` at this point; however, this element is not guaranteed to exist or be associated with the module in the future, for example if the module's parent is re-rendered. *(optional)*
- `mount {Function}` A function to be run every time `Module#mount()` is called, i.e. when the module has been associated with a new DOM element. Should be used to bind any DOM event listeners. *(optional)*
- `teardown {Function}` A function to be run when `Module#teardown()` or `Module#destroy()` is called. `teardown` will also run if you attempt to setup an already 'setup' module.
- `destroy {Function}` Run when `Module#destroy()` is called (will only ever run once) *(optional)*
