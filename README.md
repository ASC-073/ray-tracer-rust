# ray-tracer-rust
1) **PROBLEM STATEMENT** <br>
Implementing a simple ray tracer in Rust vs the C++ variant and understanding the differences in coding, usability and security for these variants, as a project for the course Principles of Programming Languages. Inspired from this book: https://raytracing.github.io/v3/books/RayTracingInOneWeekend.html#overview, credits to  Peter Shirley, Steve Hollasch and Trevor David Black.
The POPL angle here is that Rust provides a very safe and easy-to-use framework, which can vastly impact the industries that use ray tracers. We will also compare performance and observe the differences which will illustrate how one programming paradigm is better than the other.

3) **Software Architecture** <br>
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

4) **POPL Aspects**: [to update]

- Hardware Utilisation: In an attempt to improve performance, we utilised structs in Rust versus the typical classes and objects in C++. We came across a test someone did on how passing small structs by copy is better than by reference in Rust, and how both of these are far faster than doing either of these in C++. <br><br>Here is the link: https://www.forrestthewoods.com/blog/should-small-rust-structs-be-passed-by-copy-or-by-borrow/ <br><br>
The key takeaway of this test is that Rust utilises the hardware of the floating point vectors (f32) much better than C++ by default. Thus this was a fair assumption from our side that the Rust implementation would be faster because we have very frequently come across passing structs by copy or reference in functions in our code.
- 

- We learned a lot about Rust project management and concepts that it has and how it is different from C++. We used structs and traits instead of the traditional object-oriented C++ implementation, and we have listed those structs and classes in the previous section for details.
- We learnt how cargo works and why it is a much easier to use environment than default C++ variant (like to include the "rand" crate using cargo, all we have to do was use the command `cargo add rand`.
- We learnt how borrowing and references work in Rust and how they are different in C++. There is no concept of owners in C++. <br>


`fn hit(&self, r: &Ray, t_min: f64, t_max: f64, rec: &mut HitRecord) -> bool {
        let oc = r.origin() - self.center;
        let a = r.direction().length_squared();
        let half_b = vec3::dot(oc, r.direction());
        let c = oc.length_squared() - self.radius * self.radius;
        let discriminant = half_b * half_b - a * c;
        if discriminant < 0.0 {
            return false;
        }
        let sqrt_d = f64::sqrt(discriminant);
        // Find the nearest root that lies in the acceptable range
        let mut root = (-half_b - sqrt_d) / a;
        if root <= t_min || t_max <= root {
            root = (-half_b + sqrt_d) / a;
            if root <= t_min || t_max <= root {
                return false;
            }
        }
        rec.t = root;
        rec.p = r.at(rec.t);
        let outward_normal = (rec.p - self.center) / self.radius;
        rec.set_face_normal(r, outward_normal);
        rec.mat = Some(self.mat.clone());
        true
    }`
    
In this code we have passed the Ray struct by borrowing, which can be found in the sphere.rs file, Line 24. This is a safer approach compared to C++.

`bool hit(const ray& r, interval ray_t, hit_record& rec) const override {
        vec3 oc = r.origin() - center;
        auto a = r.direction().length_squared();
        auto half_b = dot(oc, r.direction());
        auto c = oc.length_squared() - radius*radius;
        auto discriminant = half_b*half_b - a*c;
        if (discriminant < 0)
            return false;
        // Find the nearest root that lies in the acceptable range.
        auto sqrtd = sqrt(discriminant);
        auto root = (-half_b - sqrtd) / a;
        if (!ray_t.surrounds(root)) {
            root = (-half_b + sqrtd) / a;
            if (!ray_t.surrounds(root))
                return false;
        }
        rec.t = root;
        rec.p = r.at(rec.t);
        vec3 outward_normal = (rec.p - center) / radius;
        rec.set_face_normal(r, outward_normal);
        rec.mat = mat;
        return true;
    }`
  which has unsafe pointers by default.
- We used generics and traits instead of the C++ object oriented approach: [add examples]


4) **Results**: <todo>

5) **Potential For future work**:
- The guide encourages us to delve into parallelism, which could utilise various cores of our CPU with random seeds, in order to massively improve performance. We could expand on our project by using the concept of Fearless Concurrency in Rust - which allows us to implement concurrency without any risk of data races or risks straight out of the box. This is done using a crate called `Rayon` which enables data parallelism.
