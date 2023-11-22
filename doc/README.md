# ray-tracer-rust
1) **PROBLEM STATEMENT**
Implementing a simple ray tracer in Rust vs the C++ variant and understanding the differences in coding, usability and security for these variants, as a project for the course Principles of Programming Languages. Inspired from this book: https://raytracing.github.io/v3/books/RayTracingInOneWeekend.html#overview, credits to  Peter Shirley, Steve Hollasch and Trevor David Black.
The POPL angle here is that Rust provides a very safe and easy-to-use framework, which can vastly impact the industries that use ray tracers. We will also compare performance and observe the differences which will illustrate how one programming paradigm is better than the other.

2) **Software Architecture**
The C++ variant has used classes and objects to implement various concepts of ray tracing like camera, ray, colours, etc. The details are as follows: [to update]
In our Rust implementation, we have used structs instead. Here are the details for that: [to update]

3) **POPL Aspects**: [to update]

- Hardware Utilisation: In an attempt to improve performance, we utilised structs in Rust versus the typical classes and objects in C++. We came across a test someone did on how passing small structs by copy is better than by reference in Rust, and how both of these are far faster than doing either of these in C++. Here is the link: https://www.forrestthewoods.com/blog/should-small-rust-structs-be-passed-by-copy-or-by-borrow/
The key takeaway of this test is that Rust utilises the hardware of the floating point vectors (f32) much better than C++ by default. Thus this was a fair assumption from our side that the Rust implementation would be faster because we have very frequently come across passing structs by copy or reference in functions in our code.
- 

- We learned a lot about Rust project management and concepts that it has and how it is different from C++.
We used structs instead of objects (C++)[expand]
- We learnt how cargo works and why it is a much easier to use environment than default C++ variant (like to include the "rand" crate using cargo, all we have to do was use the command `cargo add rand`.
- We learnt how borrowing and references work in Rust and how they are different in C++. There is no concept of owners in C++. [add examples]
- We used generics and traits instead of the C++ object oriented approach: [add examples]


4) **Results**: <todo>

5) **Potential For future work**: <todo>

