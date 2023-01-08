---
layout: single
title:  "Getting Rusty Code and Racer to Work Together"
date:   2017-02-14 00:00:00 -0700
---

While installing the Rusty Code extension in Visual Studio Code is pretty straightforward, Racer wouldn't work out of the box after clicking the "install dependencies" (or whatever it was called) button. In fact, I never received a confirmation message that the dependencies finished installing.

<!--more-->

After a while of no progress in the output window, I checked in the terminal and saw that Racer installed fine, but VS Code showed the following error:

> RUST_SRC_PATH environment variable must be set to point to the src directory of a rust checkout.

So, it turns out that a default Rust install doesn't come with the source code and simply running the following command makes the whole thing work:

```bash
rustup component add rust-src
```

If running `rustup` doesn't work, make sure that your `cargo/bin` directory is added to your `PATH`, by adding the following line to your `.bashrc` script:

```bash
PATH=~/.cargo/bin:$PATH
```

Or wherever else Cargo is installed on your machine.
