# Styling guidelines
We prefer SCSS with BEM naming methodology. Component classNames should look like: 'ComponentName__element-name--some-modifier' the **block** will be in UpperCamelCase to reflect react component name, **element** and **modifier** will be lower case separated with single dash.

We should use simple lib for react to generate classNames - https://github.com/sunify/bem-classname

The SCSS for a component should look like this:

```css
$module: 'note';

.#{$module} {
  &__content {
    background: white;
  }

  &--featured {
    .#{$module}__content {
      background: #eee;
    }
  }
}
```

##Generic style

I would like that the properties are alphabetical sorted. The '@include' and '@extend' must be in top of selector. Only the '@include' of a breakpoints must be at bottom.

Avoid nesting selectors more than 3 levels deep.

##Local variables

Local variables should be defined on top of file. All colors should be variables.

##Breakpoints

We have breakpoints mixin. The styles for specific breakpoints should be specified in each selector.
