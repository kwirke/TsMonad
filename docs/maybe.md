# Maybe

## Constructors

#### `Maybe.just<T>(t: T): Maybe<T>`
Helper function to build a Maybe object filled with a Just type.

#### `Maybe.nothing<T>(): Maybe<T>`
Helper function to build a Maybe object filled with a Nothing type.

#### `Maybe.maybe<T>(t?: T | null): Maybe<T>`
Helper function to build a Maybe object.

Returns `Maybe.just(t)` if `t` is not null nor undefined, otherwise returns `Maybe.nothing()`.

#### `new Maybe<T>(type: MaybeType, value?: T)`
Build a Maybe object. For internal use only.

- `type: MaybeType` Indicates if the Maybe content is a Just or a Nothing.
- `value: T` The value to wrap (optional).

## Helpers

#### `isJust<T>(t: Maybe<T>): boolean`
Helper function to check whether a Maybe is of the Just type.

```
Maybe.isJust(Maybe.just(4)) // => true
Maybe.isJust(Maybe.nothing()) // => false
```

#### `isNothing<T>(t: Maybe<T>): boolean`
Helper function to check whether a Maybe is of the Nothing type.

#### `sequence<T>(t: object): Maybe<object>`
**Aliases**: *sequence, all*

Helper function to convert a map of Maybe objects into a Maybe of a map of objects.

Returns `Maybe.just(t)` if all the fields in t have value, otherwise returns `Maybe.nothing()`.

## Methods in `Maybe<T>`

#### `unit<U>(u: U): Maybe<U>`
**Aliases**: *unit, of*

Wrap an object inside a Maybe.

```
Maybe.just('irrelevant').unit(6) // => Maybe.just(6)
Maybe.just('irrelevant').unit(null) // => Maybe.nothing()
```

#### `bind<U>(f: (t: T) => Maybe<U>): Maybe<U>`
**Aliases**: *bind, chain*

Apply the function passed as parameter on the object.

```
const maybeFirstChar = str => str.length ? Maybe.just(str[0]) : Maybe.nothing()
Maybe.just('hi').bind(maybeFirstChar) // => Maybe.just('h')
```

#### `fmap<U>(f: (t: T) => U): Maybe<U>`
**Aliases**: *fmap, lift, map*

Apply the function passed as parameter on the object.

```
const plusTwo = x => x + 2
Maybe.just(3).fmap(plusTwo) // => Maybe.just(5)

Maybe.just(4).fmap(x => null) // => Maybe.nothing()
```

#### `caseOf<U>(patterns: MaybePatterns<T, U>): U`
Execute a function depending on the Maybe content. It allows to unwrap the object for Just or Nothing types.

```
Maybe.just(3).caseOf({
    nothing: () => 0,
    just: x => x + 2,
}) // => 5
```

#### `defaulting(defaultValue: T): Maybe<T>`
Convert a possible Nothing into a guaranteed Maybe.Just.

```
Maybe.nothing().defaulting(9) // => Maybe.just(9)
```

#### `equals(other: Maybe<T>): boolean`
Compare the type and the content of two Maybe objects. Uses Monad [`eq` function](./monad.md).

```
Maybe.just(3).equals(Maybe.just(3)) // => true
Maybe.nothing().equals(Maybe.nothing()) // => true

Maybe.just(3).equals(Maybe.just(5)) // => false
Maybe.nothing().equals(Maybe.just(5)) //> => false
```

#### `valueOr<U extends T>(defaultValue: U): T|U`
Unwrap a Maybe with a default value.

```
Maybe.just(6).valueOr(3) // => 6
Maybe.nothing().valueOr(3) // => 3
```


