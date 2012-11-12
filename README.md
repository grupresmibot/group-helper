# Ember.js group helper

This is an experimental plugin to allow an application developer to change the granularity of bindings in a template. This can lead to significant performance improvements when outputting many of bound properties, inside of an #each for example.

The general rule is that the `group` helper causes the nearest view to be rerendered when a property inside it changes.

Currently requires Ember.js master.

## Usage

```javascript
  {{#group}}
    {{firstName}} {{lastName}}
  {{/group}}
```

Changes to `firstName` or `lastName` will rerender the whole `group` block.

```javascript
  {{#group}}
    {{#each people}}
      {{firstName}} {{lastName}}
    {{/each}}
  {{/group}}
```

The whole `group` block will be rerendered upon a change to the `people` array or any property within it.

```javascript
  {{#group}}
    {{#each people groupedRows=true}}
      {{firstName}} {{lastName}}
    {{/each}}
  {{/group}}
```

Specifying the `groupedRows` property will cause the #each to behave more like a normal bound #each. Since each row will have a virtual view associated with it, when a property within a row changes it will rerender only that row.

```javascript
  {{#group}}
    {{#each people itemViewClass="App.RowView"}}
      {{firstName}} {{lastName}}
    {{/each}}
  {{/group}}
```

You can alternatively specify an `itemViewClass` to get the normal bound #each behavior as detailed above.
