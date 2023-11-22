# ray-tracer-rust
1) **PROBLEM STATEMENT** <br><br>
Implementing a simple ray tracer in Rust vs the C++ variant and understanding the differences in coding, usability and security for these variants, as a project for the course Principles of Programming Languages.<br><br>Inspired from this book: https://raytracing.github.io/v3/books/RayTracingInOneWeekend.html#overview <br><br> Credits to  Peter Shirley, Steve Hollasch and Trevor David Black. <br><br>
The POPL angle here is that Rust provides a very safe and easy-to-use framework, which can vastly impact the industries that use ray tracers. We will also compare performance and observe the differences which will illustrate how one programming paradigm is better than the other.

2) **Software Architecture** <br><br>
We are using Rust with cargo vs C++ with cmake default build configurations.<br><br> Image generation is done using the ppm format, into which we have redirected our output.<br><br>
In our Rust implementation, we have used structs instead. Here are the details for that:

Structs:
- Camera
- HittableList
- HitRecord
- Ray
- Sphere
- Vec3 (aliased for Color and Point3)
- Lambertian
- Metal
- Dielectric

We have also used two traits in our project:
- Hittable
- Material

Here are the C++ implementation's software architecture details: <br>
- vec3 class with aliases color and point3
- ray class
- struct hit_record
- hittable class
- sphere class
- hittable_list class
- camera class

3) **POPL Aspects**: [to update]

- Hardware Utilisation: In an attempt to improve performance, we utilised structs in Rust versus the typical classes and objects in C++. We came across a test someone did on how passing small structs by copy is better than by reference in Rust, and how both of these are far faster than doing either of these in C++. <br><br>Here is the link: https://www.forrestthewoods.com/blog/should-small-rust-structs-be-passed-by-copy-or-by-borrow/ <br><br>
The key takeaway of this test is that Rust utilises the hardware of the floating point vectors (f32) much better than C++ by default. Thus this was a fair assumption from our side that the Rust implementation would be faster because we have very frequently come across passing structs by copy or reference in functions in our code.<br><br>
- We learned a lot about Rust project management and concepts that it has and how it is different from C++. We used structs and traits instead of the traditional object-oriented C++ implementation, and we have listed those structs and classes in the previous section for details.
- We learnt how cargo works and why it is a much easier to use environment than default C++ variant (like to include the "rand" crate using cargo, all we have to do was use the command `cargo add rand`. In general, package maagement is much more seamless and better in Rust than C++. It is therefore much easier for a game developer or animator to utilise this tool for their purposes if they so desire, simply by a single command.
- We learnt how borrowing and references work in Rust and how they are different in C++. There is no concept of owners in C++. <br>

![Screenshot_20231122_225007](https://github.com/ASC-073/ray-tracer-rust/assets/100084094/10dd2a07-f3c2-4e7c-91d5-a2a6a46dde3e)
    
In this code we have passed the Ray struct by borrowing, which can be found in the sphere.rs file, Line 24. This is a safer approach compared to C++.

![Screenshot_20231122_224921](https://github.com/ASC-073/ray-tracer-rust/assets/100084094/2730901b-7401-4aef-b113-872f38e35ee0)
    
  which has unsafe pointers by default.
- We used traits instead of the C++ object oriented approach:

![image](https://github.com/ASC-073/ray-tracer-rust/assets/100084094/a1be71b6-9f20-4603-b0b2-cbe14c87a34a)
![image](https://github.com/ASC-073/ray-tracer-rust/assets/100084094/790a8da6-8e58-499b-a5e9-61c8efdbb946)



4) **Results**:

5) **Potential For future work**:
- The guide encourages us to delve into parallelism, which could utilise various cores of our CPU with random seeds, in order to massively improve performance. We could expand on our project by using the concept of Fearless Concurrency in Rust - which allows us to implement concurrency without any risk of data races or risks straight out of the box. This is done using a crate called `Rayon` which enables data parallelism.
- Implementation Of the concept of lifetimes in this project could further increase run time safety, which can be implemented for various structs and other parameters for different parts of the code.
- We can also incorporate a dynamic memory allocator as an addition to this project for game developers. One of the biggest reasons C++ is more popular than Rust in the game industry is that we cannot allocate memory in Rust, so adding this would increase ease of access for the users.


**Instructions to run the Rust file**:
- Extract the project zip file into the PC
- Using a terminal, run the command: `cargo run > image.ppm`<br>
<br>The C++ implementation can be found in the guide link itself for comparison.<br>

