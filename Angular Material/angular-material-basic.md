# Angular Material Basic Layout on HTML

### How does Angular Material's layout work?
**layout="row"**
html components in a div with layout="row" would be laid horizontally like below
```html
<div layout="row">
  <div flex>A</div>
  <div flex>B</div>
</div>
```
This is going to be
**A B**

**layout="column"**
html components in a div with layout="column" would be laid vertically like below
```html
<div layout="column">
  <div flex>C</div>
  <div flex>D</div>
</div>
```
This is going to be
**C**
**D**

### To be responsive
There are numerous layout sizes for the case where the size of device extends or shrinks
For example, layout-xs, layout-sm, layout-gt-sm ... etc.
xs, sm, gt .. stand for extra-small, small, greater than small each.

```html
<div layout="column" layout-lg="row">
  <div flex>E</div>
  <div flex>F</div>
</div>
```
In this case, the layout would be set as a column as the default.
But, when the size of device extends more than large it would be changing to layout-lg which will pose components horizontally.

### Reference
https://material.angularjs.org/latest/layout/container
