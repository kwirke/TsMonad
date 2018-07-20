# API

## Maybe

### constructors

#### `Maybe.just<T>(t: T) => Maybe<T>`
Returns a wrapper that represents the presence of value `t`.

#### `Maybe.nothing<T>() => Maybe<T>`
Returns a wrapper that represents the absence of a value.

#### `Maybe.maybe<T>(t?: T | null) => Maybe<T>`
Returns `Maybe.just(t)` if `t` is not null nor undefined, otherwise returns `Maybe.nothing()`.

#### `new Maybe<T>(type: MaybeType, value?: T)`
Constructs a Maybe
