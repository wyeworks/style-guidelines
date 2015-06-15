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
