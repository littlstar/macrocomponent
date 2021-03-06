# macrocomponent

Convenience wrapper around the [nanocomponent](https://github.com/yoshuawuyts/nanocomponent) DOM component library, for the most common case.

## Example

Instead of this boilerplate-y thing:

```js
const Component = require('nanocomponent')
const html = require('bel')
const morph = require('nanomorph')
const inherits = require('util').inherits

function View () {
  Component.call(this)
  this.foo = null
  this.bar = null
}

inherits(View, Component)

View.prototype._update = function (state) {
  return state.foo !== this.foo
    || state.bar !== this.bar  
}

View.prototype._render = function (state) {
  this.foo = state.foo
  this.bar = state.bar
  const el = html`
    <p>
      Hey ${state.foo}, how are you ${state.bar}ing?
    </p>
  `
  if (this._element) morph(this._element, el)
  else this._element = el
  return this._element
}
```

You can now do this:

```js
const component = require('macrocomponent')

const props = ['foo', 'bar']
const view = component(props, state => `
  <p>
    Hey ${state.foo}, how are you ${state.bar}ing?
  </p>
`)
```

..and it implements the same logic!

I'm going to experiment with a bit more magic, so maybe this will eventually be possible (but it is not yet!):

```js
const component = require('macrocomponent')

const view = component((foo, bar) => `
  <p>
    Hey ${foo}, how are you ${bar}ing?
  </p>
`)

```

## Installation

```js
$ npm install macrocomponent
```

## API

### component(props, render)

## License

MIT
