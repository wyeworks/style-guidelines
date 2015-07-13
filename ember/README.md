# Ember Style Guide

```js
import Ember from 'ember';

let service = Ember.inject.service;

let {
  alias,
  none
} = Ember.computed;

export default Ember.Service.extend({
  store: service(),
  isAnon: none('user'),

  findUser() {
    return this
      .get('store')
      .findById('user', 'me')
      .then(user => {
        this.set('user', user);

        return user;
      });
  },

  invalidate() {
    return this.findUser();
  }
});
```

```js
import Ember from 'ember';

let notEmpty = Ember.computed.notEmpty;

export default Ember.Service.extend({
  page: null,
  image: null,

  hasPage: notEmpty('page'),

  clear: function() {
    this.setProperties({
      page: null,
      image: null
    });
  }
});
```

```js
import Ember from 'ember';
import DS from 'ember-data';

const URL = '/api/1/my-action';

let $ = Ember.$;

export default DS.Adapter.extend({

  findQuery: function(store, type, { url, forceUpdate }) {
    let data = { url };

    if(forceUpdate) {
      data.force = true;
    }

    return $.post(URL, JSON.stringify(data));
  }
});
```

## Naming

* [1.1](#1.1) Use `camelCase` for function names and variables
* [1.2](#1.2) Use `PascalCase` for class names
* [1.3](#1.3) Use `ALL_CAPS_SNAKE_CASE` for constants

> Classes in this context refer to functions used as prototypes, objects
> declared using the ES2015 `class` syntax and objects that _inherit_ from
> `Ember.Object`

## Variables

* [2.1](#2.1) Prefer `let` over `var` and use `const` semantically to indicate
  immutability. Please, remember that `const` variables are mutable in
  JavaScript variables are mutable in JavaScript.
* [2.2](#2.2) Use one `let` statement for one line declarations and for null
  variables and use separate `let` assignments for multi line declarations and
  destructuring assignments.

```js
let lorem = {},
    ipsum = 5,
    dolor;

let {
  PI,
  E
} = Math;

let daysOfWeek = [
  'Sunday',
  'Monday',
  'Tuesday',
  'Wednesday',
  'Thursday',
  'Friday',
  'Saturday'
];
```
