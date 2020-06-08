# CSS Cascade.

## First Tier: Importance
The type of the rule.

1. transition
2. important
3. animation
4. normal

## Second Tier: Origin
Where the rule are defined.

1. Website (user defined)
2. user
3. browser ( defaults )

__Note__: The hierarchy here is actually _reverse_ for `!important` rules, meaning that an `!important` __browser default__ rule wins over an `!important` __website__ rule (whereas a __website__ rule normally wins over a __browser default__).

## Third Tier: Specificity
How specific a rule is.

1. inline
2. id
3. class | attributes | pseudo-class
4. type | pseudo-element

__Note__: One thing to note about levels on this tier is that __the number of hits on the highest-reached level matter__.

## Fourth Tier: Position
Order that the rules are defined.

Rules that are defined later in linked style sheets or `<style>` tags will win, given that everything else in the Cascade is the same.

