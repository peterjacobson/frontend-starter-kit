# CSS

## Formatting

We delegate that to [Prettier](https://prettier.io/). Make sure [your text editor](https://code.visualstudio.com/&sa=D&ust=1520457897533000&usg=AFQjCNF3QTfRTIBG7ZBDeYbNMcYimiKSbw) has [that extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode), and that it's configured to auto-format on save. Here's [the ESLint config](https://github.com/springload/eslint-plugin-springload).

## File Structure

We use a methodology called [ITCSS](https://www.xfive.co/blog/itcss-scalable-maintainable-css-architecture/),
in which CSS is organised by increasing CSS specificity (CSS reset or normalize, then base styles, component styles, and finally utility classes, or that general approach). 
Note: There is a framework built from this concept called [INUITCSS](https://github.com/inuitcss/inuitcss)


## CSS preprocessors / compilers / templaters

[Sass](https://github.com/sass/libsass) for build-time styles. Where possible prefer build-time styles more than run-time styles, because they're probably faster.

For CSS-In-JS we like [Glamor](https://github.com/threepointone/glamor) and [Glamorous](https://glamorous.rocks/).


### Naming conventions

Use [BEM](https://en.bem.info/) (**b**lock__**e**lement--**m**odifier) with lowercase words separated by single hyphens. E.g. `.block-name`, or `.block-name__element-name`,or `.block-name__element-name--modifier-name`.   
There is only ever one "block".   
Double underscores are only ever one level deep. If you need deeper then consider using different names.  
Don't use camelCase.  


# Advice

Avoid nesting selectors. This can make styles less reusable and it will mess with the cascade, and styles will be very hard to override.  
Don't use string concatenation (&__element-name) for classes, but pseudoes are ok.   


<table>
  <tbody>
    <tr>
      <th>
        Good (easy to search)
      </td>
      <th>
        Bad (hard to search for "tile__content")
      </th>
    </tr>
    <tr>
      <td>
        .tile { /* properties */ }<br>
        .tile__content { /* properties */ }<br>
        .tile__heading { /* properties */ }<br>
      </td>
      <td>
       .tile { /* properties */<br>
        &nbsp; &__content { /* properties */ }<br>
        &nbsp; &__heading { /* properties */ }<br> }<br>
      </td>
    </tr>
    <tr>
      <th>
        Good (&amp; for pseudoes is fine)
      </th>
    </tr>
    <tr>
     <td>
      .tile { /* properties */<br>
      &nbsp; &:hover { /* properties */ }<br> }<br>
     </td>
    </tr>
    <tr>
     <td>
      .tile { /* properties */ }<br>
      .tile:hover { /* properties */ }<br>
     </td>
    </tr>
  </tbody>
</table>

### Naming files and components

Component files should use the 'block' name as the file name, there shouldn't be any css in the file that doesn't start with the block name. eg. `_components.btn.scss`.  
File names should be all lowercase and using period (.) to seperate words. eg. `_objects.grid.scss`, `_objects.grid.spacing.scss`  
Images: Try and prefix file names with what they are: I.e. if it’s a sprite for buttons, call it `sprite-buttons.png`. If it’s an icon for Facebook, call it `icon-facebook.png` etc.  


<table>
 <tbody>
  <tr>
   <th>
     Good (in _components.btn.scss)
   </th>
   <th>
     Bad (in _components.btn.scss)
   </th>
  </tr>
  <tr>
    <td>
     .btn { /* properties */ }<br>
     .btn--white { /* properties */ }<br>
     .btn__text { /* properties */ }<br>
   </td>
   <td>
    .modal-btn { /*properties */ }
   </td>
  </tr>
 </tbody>
</table>

## More advice

Don't use `@extends`. Prefer `@includes` instead if necessary.

Media Queries should be inside or near css block, not at the bottom or top of files.

Use classes for styling only, don’t use IDs in your CSS.

Elements shouldn't be targeted after classes (with few exceptions). e.g. `.container td`. However one notable exception is places where we can't add classes, such as WYSIWYG fields where the user is creating tags and we can't control that, and in such cases the rules should be carefully scoped and ordered as per ITCSS.

<table>
 <tbody>
  <tr>
   <th>
    Good
   </th>
   <th>
    Bad
   </th>
  </tr>
  <tr>
   <td>
    .list { list-style: none; }<br>
    .list__item {/* properties */}<br>
    .banner--home {/* properties */}<br>
   </td>
   <td>
    ul.list { list-style: none;}<br>
    .list li {/* properties */}<br>
    .home div.banner {/* properties */}<br>
   </td>
  </tr>
  </tbody>
</table>

Avoid using the words 'mobile' or 'desktop' in classNames, instead opt for more relative terminology such as: small, medium, large, x-large etc. This is because small desktops can match the size of large tablets, so using generic terms is more accurate.

Don’t use units on line-heights. Do this: `line-height: 1.25`, don't do this: `line-height: 1.25rem`.

CSS Margins collapse into each other, so only set margins along one axis direction (e.g. `top and left`, or `right and bottom`, but not `left and right and top and bottom`). We typically use `right and bottom`. And be consistent with 
[vertical spacing](http://webtypography.net/2.2.2)

Modifier (AKA State) classes use `...--is-something`. A state class is a modifier of an element or block. Using .active or similar on its own is too obscure, if there is more than one class on an element it is not clear which the `.-active` class belongs to.

<table>
 <tbody>
  <tr>
   <th>
    Good
   </th>
   <th>
    Bad
   </th>
  </tr>
  <tr>
   <td>
    .block--is-animating {/* properties */}<br>
    .modal--is-active {/* properties */}<br>
    .accordion--is-open {/* properties */}<br>
   </td>
   <td>
    .is-active {/* properties */}<br>
    .-active {/* properties */}<br>
    .open {/* properties */}<br>
   </td>
  </tr>
  </tbody>
</table>

## New or Old?

For legacy projects we follow whatever conventions they have, but where possible we try to migrate to these newer approaches.
