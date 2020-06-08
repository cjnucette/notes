# Flexbox

* `display: flex`: creates a flex container.
* `flex-direction: row`: is the default, it accepts `row` and `columns`.
* __Direct children__ of the flex container become flex items.
* With `flex-direction: row`, flex items align one beside the other in a row using as little space as needed to accommodate each flex item within the flex container's width; even though, each element wants to occupy 100% of the space. In `flex-direction: column` each element will be placed one below the other and will use 100% of the flex container's width.
* The property `gap` is going to be available to provide space between flex items, but for the moment it's only supported by firefox. So an alternative solution is needed. One solution is the used of the `+` combinator, as in: `.item + .item { margin-left: 1em }`. This will set a margin of `1em` in every flex item (with a class of .item) but the first.
* `align-items: stretch`: is the default, it makes the flex item to stretch to the height (or width depending on the flex-direction property) of the flex container. it accepts `flex-start`, `flex-end`, `center`, `stretch`, `space-around`, `space-evenly`, and `space-between`.
* `justify-content: flex-start`: is the default, it makes the flex items to align to the start (inline-start or block-start depending on the flex-direction property) of the flex container. it accepts `flex-start`, `flex-end`, `center`, `space-around`, `space-evenly`, and `space-between`.
