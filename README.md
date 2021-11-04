# SVG [![Package][package-img]][package-url] [![Documentation][documentation-img]][documentation-url] [![Build][build-img]][build-url]

The package provides an SVG composer and parser.

## Example: Composing

```rust
use svg::Document;
use svg::node::element::Path;
use svg::node::element::path::Data;

let data = Data::new()
    .move_to((10, 10))
    .line_by((0, 50))
    .line_by((50, 0))
    .line_by((0, -50))
    .close();

let path = Path::new()
    .set("fill", "none")
    .set("stroke", "black")
    .set("stroke-width", 3)
    .set("d", data);

let document = Document::new()
    .set("viewBox", (0, 0, 70, 70))
    .add(path);

svg::save("image.svg", &document).unwrap();
```

## Example: Parsing

```rust
use svg::node::element::path::{Command, Data};
use svg::node::element::tag::Path;
use svg::parser::Event;

let path = "image.svg";
let mut content = String::new();
for event in svg::open(path, &mut content).unwrap() {
    match event {
        Event::Tag(Path, _, attributes) => {
            let data = attributes.get("d").unwrap();
            let data = Data::parse(data).unwrap();
            for command in data.iter() {
                match command {
                    &Command::Move(..) => println!("Move!"),
                    &Command::Line(..) => println!("Line!"),
                    _ => {}
                }
            }
        }
        _ => {}
    }
}
```

## Contribution

Your contribution is highly appreciated. Do not hesitate to open an issue or a
pull request. Note that any contribution submitted for inclusion in the project
will be licensed according to the terms given in [LICENSE.md](LICENSE.md).

[build-img]: https://github.com/bodoni/svg/workflows/build/badge.svg
[build-url]: https://github.com/bodoni/svg/actions/workflows/build.yml
[documentation-img]: https://docs.rs/svg/badge.svg
[documentation-url]: https://docs.rs/svg
[package-img]: https://img.shields.io/crates/v/svg.svg
[package-url]: https://crates.io/crates/svg

## Standards Compliance

| Standard | Compatibility | Notes |
| -------- | ------- | ------|
| [SVG 1.1 Tiny](https://web.archive.org/web/20111229174443/http://www.w3.org/TR/SVGMobile/) | Partial | |
| [SVG 1.2 Tiny](https://www.w3.org/TR/SVGMobile12/index.html) | Partial | |


### SVG Tiny Support
| Elements | 1.1 | 1.2 | Supported |
| -------- | --- | --- | --------- |
| a | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animate | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animateColor | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animateMotion | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animateTransform | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animation |  | :heavy_check_mark: | :x: |
| audio |  | :heavy_check_mark: | :x: |
| circle | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| clipPath |  |  | :white_check_mark: |
| defs | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| desc | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| discard |  | :heavy_check_mark: | :x: |
| ellipse | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| filter |  |  | :white_check_mark: |
| font |  | :heavy_check_mark: | :x: |
| font-face | :heavy_check_mark: | :heavy_check_mark: | :x: |
| font-face-name | :heavy_check_mark: | | :x: |
| font-face-src | :heavy_check_mark: | :heavy_check_mark: | :x: |
| font-face-uri |  | :heavy_check_mark: | :x: |
| foreignObject | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| g | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| glyph | :heavy_check_mark: | :heavy_check_mark: | :x: |
| handler |  | :heavy_check_mark: | :x: |
| hkern | :heavy_check_mark: | :heavy_check_mark: | :x: |
| image | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| line | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| linearGradient |  | :heavy_check_mark: | :white_check_mark: |
| listener |  | :heavy_check_mark: | :x: |
| marker |  |  | :white_check_mark: |
| mask |  |  | :white_check_mark: |
| metadata | :heavy_check_mark: | :heavy_check_mark: | :x: |
| missing-glyph | :heavy_check_mark: | :heavy_check_mark: | :x: |
| mpath | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| path | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| pattern |  |  | :white_check_mark: |
| polygon | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| polyline | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| prefetch |  | :heavy_check_mark: | :x: |
| radialGradient |  | :heavy_check_mark: | :white_check_mark: |
| rect | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| script |  | :heavy_check_mark: | :x: |
| set | :heavy_check_mark: | :heavy_check_mark: | :x: |
| solidColor |  | :heavy_check_mark: | :x: |
| stop |  | :heavy_check_mark: | :white_check_mark: |
| svg | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| symbol |  |  | :white_check_mark: |
| switch | :heavy_check_mark: | :heavy_check_mark: | :x: |
| tbreak |  | :heavy_check_mark: | :x: |
| text | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| textPath |  |  | :white_check_mark: |
| textArea |  | :heavy_check_mark: | :x: |
| title | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| tspan |  | :heavy_check_mark: | :x: |
| use | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| video |  | :heavy_check_mark: | :x: |


| Elements         | 1.1                | 1.2                | Supported          |
|------------------|--------------------|--------------------|--------------------|
| a                | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animate          | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animateColor     | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animateMotion    | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animateTransform | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| animation        |                    | :heavy_check_mark: | :x:                |
| audio            |                    | :heavy_check_mark: | :x:                |
| circle           | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| clipPath         |                    |                    | :white_check_mark: |
| defs             | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| desc             | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| discard          |                    | :heavy_check_mark: | :x:                |
| ellipse          | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| filter           |                    |                    | :white_check_mark: |
| font             |                    | :heavy_check_mark: | :x:                |
| font-face        | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| font-face-name   | :heavy_check_mark: |                    | :x:                |
| font-face-src    | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| font-face-uri    |                    | :heavy_check_mark: | :x:                |
| foreignObject    | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| g                | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| glyph            | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| handler          |                    | :heavy_check_mark: | :x:                |
| hkern            | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| image            | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| line             | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| linearGradient   |                    | :heavy_check_mark: | :white_check_mark: |
| listener         |                    | :heavy_check_mark: | :x:                |
| marker           |                    |                    | :white_check_mark: |
| mask             |                    |                    | :white_check_mark: |
| metadata         | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| missing-glyph    | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| mpath            | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| path             | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| pattern          |                    |                    | :white_check_mark: |
| polygon          | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| polyline         | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| prefetch         |                    | :heavy_check_mark: | :x:                |
| radialGradient   |                    | :heavy_check_mark: | :white_check_mark: |
| rect             | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| script           |                    | :heavy_check_mark: | :x:                |
| set              | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| solidColor       |                    | :heavy_check_mark: | :x:                |
| stop             |                    | :heavy_check_mark: | :white_check_mark: |
| svg              | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| symbol           |                    |                    | :white_check_mark: |
| switch           | :heavy_check_mark: | :heavy_check_mark: | :x:                |
| tbreak           |                    | :heavy_check_mark: | :x:                |
| text             | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| textPath         |                    |                    | :white_check_mark: |
| textArea         |                    | :heavy_check_mark: | :x:                |
| title            | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| tspan            |                    | :heavy_check_mark: | :x:                |
| use              | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: |
| video            |                    | :heavy_check_mark: | :x:                |