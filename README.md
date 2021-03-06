# direct2d-rs [![Crates.io](https://img.shields.io/crates/v/direct2d.svg)](https://crates.io/crates/direct2d)

[Documentation](https://docs.rs/direct2d/*/direct2d/)

Safe abstractions for drawing on Windows using Direct2D

To use it, add this to your Cargo.toml:
```toml
[dependencies]
direct2d = "0.1"
```

## Example

```rust
extern crate direct2d;

use direct2d::device_context::{DeviceContext, IDeviceContext};
use direct2d::render_target::IRenderTarget;
use direct2d::brush::SolidColorBrush;
use direct2d::image::Bitmap;

fn draw(context: &mut DeviceContext, target: &Bitmap) {
    let brush = SolidColorBrush::create(&context)
        .with_color(0xFF_7F_7F)
        .build().unwrap();

    context.begin_draw();
    context.set_target(target);
    context.clear(0xFF_FF_FF.into());
    
    context.draw_line((10.0, 10.0).into(), (20.0, 20.0).into(), &brush, 2.0, None);
    context.draw_line((10.0, 20.0).into(), (20.0, 10.0).into(), &brush, 2.0, None);

    match context.end_draw() {
        Ok(_) => {/* cool */},
        Err(_) => panic!("Uh oh, rendering failed!"),
    }
}
```
