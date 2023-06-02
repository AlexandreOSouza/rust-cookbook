## [Rust book](https://doc.rust-lang.org/book/)

## [Rust by example](https://doc.rust-lang.org/rust-by-example/)

- Rust has a main function that execute the code
  - Like main function in Java
- There is a compiler, you can using by `rustc` than execute the compiled file `./{filename}`

## Comments

- There two main types of comments in Rust
  - Regula comment
    - `// or /* */`
  - Doc comment
    - `/// Generate libary docs for the following item.`
    - `//! Generate libary docs for the enclosing item.`

## Formated Print

- [Check more examples](https://doc.rust-lang.org/rust-by-example/hello/print.html)
- Printing is based on macros defined in `std::fmt`
  - `format!`: write formatted text to String
  - `print!`: same as format! but the text is printed to the console (io::stdout)
  - `println!`: same as print! but a new line is appended
  - `eprint!`: same as print! but the text is printed to the standard error (io::stderr)
  - `eprintln!`: same as eprint! but a newline is appended
- In general the `{}` will be automatically replaced with any arguments,

```rust
fn main(){
 println!("{} days", 31);

 // We can define positional arguments
 println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");

 // Named arguments
 println!("{subject} {verd} {object}",
   object="the lazy dog",
   subject="the quick brow fox",
   verb="jumps over"
 );

 // Different formatting can be invoked by specifying the format character
 // after a `:`.
 println!("Base 10:               {}",   69420); // 69420
 println!("Base 2 (binary):       {:b}", 69420); // 10000111100101100
 println!("Base 8 (octal):        {:o}", 69420); // 207454
 println!("Base 16 (hexadecimal): {:x}", 69420); // 10f2c
 println!("Base 16 (hexadecimal): {:X}", 69420); // 10F2C
}

```

## [Primitives](https://doc.rust-lang.org/rust-by-example/primitives.html)

- Rust provides access to a wide variety of primitives. A sample includes:

- Scalar types
  - Signed integers: i8, i16, i32, i64, i128 and isize (pointer size)
  - Unsigned integers: u8, u16, u32, u64, u128 and usize (pointer size)
  - Floating point: f32, f64
  - char Unicode scalar values like 'a', 'α' and '∞' (4 bytes each)
  - bool either true or false
  - The unit type (), whose only possible value is an empty tuple: ()
- Compound Types
  - Arrays like [1, 2, 3]
  - Tuples like (1, true)o

### Structes

- There are three types of structures that can be creating using the `struct` keyword:
  - Tuple struct
  - C struct (Classic)
  - Unit structes

```rust
// An attribute to hide warnings for unused code.
#![allow(dead_code)]

#[derive(Debug)]
struct Person {
    name: String,
    age: u8,
}

// A unit struct
struct Unit;

// A tuple struct
struct Pair(i32, f32);

// A struct with two fields
struct Point {
    x: f32,
    y: f32,
}

// Structs can be reused as fields of another struct
struct Rectangle {
    // A rectangle can be specified by where the top left and bottom right
    // corners are in space.
    top_left: Point,
    bottom_right: Point,
}

fn main() {
    // Create struct with field init shorthand
    let name = String::from("Peter");
    let age = 27;
    let peter = Person { name, age };

    // Print debug struct
    println!("{:?}", peter);

    // Instantiate a `Point`
    let point: Point = Point { x: 10.3, y: 0.4 };

    // Access the fields of the point
    println!("point coordinates: ({}, {})", point.x, point.y);

    // Make a new point by using struct update syntax to use the fields of our
    // other one
    let bottom_right = Point { x: 5.2, ..point };

    // `bottom_right.y` will be the same as `point.y` because we used that field
    // from `point`
    println!("second point: ({}, {})", bottom_right.x, bottom_right.y);

    // Destructure the point using a `let` binding
    let Point { x: left_edge, y: top_edge } = point;

    let _rectangle = Rectangle {
        // struct instantiation is an expression too
        top_left: Point { x: left_edge, y: top_edge },
        bottom_right: bottom_right,
    };

    // Instantiate a unit struct
    let _unit = Unit;

    // Instantiate a tuple struct
    let pair = Pair(1, 0.1);

    // Access the fields of a tuple struct
    println!("pair contains {:?} and {:?}", pair.0, pair.1);

    // Destructure a tuple struct
    let Pair(integer, decimal) = pair;

    println!("pair contains {:?} and {:?}", integer, decimal);
}
```

### Enum

- Is the same as any language
  - To access a enum value use `{enum}::{value}`
  - enum can use structs in the value

### Constants

- Rust has two different types of constants which can be declared in any scope including global. Both require explicit type annotation:
  - const: An unchangeable value (the common case).
  - static: A possibly mutable variable with 'static lifetime. The static lifetime is inferred and does not have to be specified. Accessing or modifying a mutable static variable is unsafe.

## Expressions

- A Rust programa is made up of a series of statements:
  - We can use a expression to assign a value to a variable:

```rust
fn main() {
   let x = 5u32;

   let y = {
       let x_squared = x * x;
       let x_cube = x_squared * x;

       // This expression will be assigned to `y`
       x_cube + x_squared + x
   };

   let z = {
       // The semicolon suppresses this expression and `()` is assigned to `z`
       2 * x;
   };

   println!("x is {:?}", x);
   println!("y is {:?}", y);
   println!("z is {:?}", z);
}
```

## [Flow Control](https://doc.rust-lang.org/rust-by-example/flow_control.html)
