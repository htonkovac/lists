# Lists
created following this tutorial: https://rust-unofficial.github.io/too-many-lists/first-layout.html

## Learnings

### Enums
```rust
pub enum SomeEnum {
  Empty
  Elem(i32)
}```

In memory Enums are represented with a tag (integer telling us which type is stored) + space for the largest element


#### NullPointer Optimization

```rust
pub enum OptimizedEnum {
  Empty,
  Elem(Box<i32>)
}`

In this case, the enum in memory is only as big as the Box. Box is a non-null pointer.
 So if the value is all 0s. Then it is the Empty case.

#### Hiding implementation details
we start with this (have in mind struct elements are implicitly private):
```rust
struct Node {
    elem: i32,
    next: List,
}

pub enum List {
    Empty,
    More(Box<Node>),
}
```
i solved it like this:
```rust

public struct List {
  head: Link
}

struct Link {
  elem: Elem
  next: Box<Link>
}

enum Elem {
  Empty,
  Something(Box<i32>)
}
```
the author like this:

```rust

pub struct List {
    head: Link,
}

enum Link {
    Empty,
    More(Box<Node>),
}

struct Node {
    elem: i32,
    next: Link,
}

```

the problem with my variant is that it can be empty but still have a Next
