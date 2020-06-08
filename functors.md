# Functors

* Functor: A type that implements a `map` as a mean to apply a function on its value preserving __composition__ `F(x).map(f).map(g) === F(x).map(g(f(x)))` and __identity__ `F(x).map(x => x) === F(x)`.
* Pointed Functor: A functor that implements an `of` method that returns a Functor of the given value.
* Applicative Functor: A functor that implements `ap` method that the value of one container on the value of another container.
* Semigroups: A type that implements `concat` that is __associative__ `a + ( b + c ) === (a + b) + c`.
* Monoids: It's a semigroup that has an __identity__ element that when combined with any other element returns that other element `1 + 0 === 1, 2 + 0 === 2` or `1 * 1 = 1, 2 * 1 == 2`.
* Monads: Is a pointed functor that implements a `flatmap` or `chain` that when applied to a nested monad returns an unidimensional monad.
* Natural Transformation:
* Isomorphism: Change from a type to other type without losing information.
