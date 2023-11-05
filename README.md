# ray-tracer-rust
Implementing a simple ray tracer in Rust vs the C++ variant and understanding the differences in coding, usability and security for these variants, as a project for the course Principles of Programming Languages.

Inspired from this book: https://raytracing.github.io/v3/books/RayTracingInOneWeekend.html#overview, credits to  Peter Shirley, Steve Hollasch and Trevor David Black.

Learning objectives: Rust syntax, modules, cargo, crates, references and borrowing, copy, clone, etc. crates, generics and traits, etc.

We need to at least learn how to create images, so we do so in the ppm format. Using the basic colours red, blue and green, we can create patterns and combinations using the double loop (256x256 pixels). 
Here: P3 is the image format which means text-based colour image. We also specified the image height, image width and maximum colour value for the render itself. 

Vec3 struct: We will use this to implement various concepts needed in image generation, from a point in 3D space to a specific colour using the combinations of red, blue and green. **We only used aliases for doing this, so we won’t get any warnings.**

Notice that vec3 is a small struct, so it is quite efficient to pass it by copy whenever we need to transfer it. Here is an interesting link: https://www.forrestthewoods.com/blog/should-small-rust-structs-be-passed-by-copy-or-by-borrow/
Key takeaways: 
- The code for passing structs by copying is much cleaner than by borrowing. Borrowing temporary values everytime for all small structs is impractical.
- Performance isn't affected for small structs whether you pass by copy or by reference.
- By default, regardless of passing by copy or by reference, Rust was doubly fast than C++ for this job.
- "Rust is remarkably more efficient at utilizing my CPU's floating point vectors. The difference is enormous! Rust f32 is almost 3.5x more efficient than C++ float. And, for some reason, C++ double is twice as efficient as float!"
This benchmarking reinforces our idea that implementing the ray tracer in Rust is going to be faster than C++ for large renders.

Another important difference to note is that **package handling** is much easier to use and well-implemented than C++. Utilising any new cargo package requires just one command line instruction. The project is also much better maintained in this way - the Cargo.toml file holds all external dependencies used in the project as opposed to a header file in C++. We have used the rand crate in our project.

Cargo typically builds and runs the program in debug mode, which is slower. For improved speed, we are using cargo run --release to build and execute in release mode. All the renders are faster.
