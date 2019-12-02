## Version 2.0.1

Many optimizations, bug fixes, and new features. With this version, the popular "calendar" showcase
for range libraries is supported (see [./test/calendar.cpp](calendar.cpp) for more).

### Other

- ChainRange does not require the output type to be default-constructible.

## Version 2.0.0

Many optimizations, bug fixes, and new features. With this version, the popular "calendar" showcase
for range libraries is supported (see [./test/calendar.cpp](calendar.cpp) for more).

### Features

- Algorithms added:
  - `chain()`
  - `cycle()`
  - `flatten()`
  - `for_each()`
  - `group_adjacent_by()`
  - `in_groups_of_exactly()`
  - `in_groups_of()`
  - `null_sink()`
  - `padded()`
  - `tee()`
  - `zip_longest()`

### Bugfixes

- Overload resolution for `as_input_range()` was very confusing. This has been cleaned up.
- Some operations that were expected to be idempotent were not (#1).
- Combinators now support non-default-constructible value types, unless the output explicitly
  requires it (#7).
- Fix `first()` after `sort()` (#8).
- `sort()` can now be constructed with comparison predicates taking more than one constructor
  argument.
- `sort()`/`min()`/`max()` support non-default-constructible and non-copyable predicates.

### Optimizations

- When compilers support it, `__builtin_expect` is utilized in inner loops to aid code layout.
- Idempotency is now only ensured when the input isn't already idempotent.
- Fine-tuning of many internal loops to avoid unnecessary branches.
- Where possible, the "empty base class" optimization is used. This mostly applies to combinators
  that take a standard comparison predicate (`std::less`, `std::equal_to`, etc.).
- `group_adjacent_by()` no longer requires internal temporary storage in a vector (#6).

### Other

- Grouping combinators now produce subranges instead of `std::array`s or `std::vector`s, eliminating
  the need to allocate temporary internal storage.
- Added a benchmark suite using Google Benchmark.
- Cleanup of internal naming conventions.
- `T::is_finite` is no longer required for input ranges (defaults to `false` if missing).
- `min()` and `max()` can now operate with a custom comparison function.

### Contributors

- René Kijewski
- Jules Ricou
- Simon Ask Ulsnes

## Version 1.0.1

Bug fixes and feature enhancements. Thanks for the valuable feedback from /r/cpp!

## Features

- Added `enumerate(...)` as an alias for `zip(seq(), ...)`.
- Added `reverse()` sink, which reverses the order of the input.
- Renamed `first_n()` to `take()` (keeping `first_n()` as an alias).
- Renamed `fill()` to `repeat()` (keeping `fill()` as an alias).
- Renamed `fill_n()` to `repeat_n()` (keeping `fill_n()` as an alias).

### Bugfixes

- Fixed a bug where `zip(...)` would not explicitly convert its inputs to ranges, meaning standard
  containers could not be used directly.
- Fixed a bug where `zip(...)` would produce tuples containing expired references.

## Other

- Added MIT license (See [./LICENSE](LICENSE)).
- Updated README, including more examples.