# Rust Multithreaded Web Server

This is a little practice example of a multithreaded web server implemented using the [Rust Programming Language](https://www.rust-lang.org/).

## Usage

To use this web server and try it, it is required [Cargo](https://doc.rust-lang.org/stable/cargo/) to be installed.

First, clone this repository

```
git clone https://github.com/alexriosj/rust_mt_web_server
cd rust_mt_web_server
```

With `cargo` already installed, simply run:

```
cargo run
```

The server will just accept one request due to the educative focus.
If you want to test more request change the `.take(2)` from the main function in `src/bin/main.rs` as the following code:

```Rust
fn main() {
    // --snip--

    for stream in listener.incoming() {
        // --snip--
    }

    // --snip--
}
```

You can interact with three request:

- GET /
- GET /sleep
- Other (this returns back a 404 NOT FOUND error). e.g.: `127.0.0.1/test`

The `/sleep` route will sleep the current thread 5 seconds, so then thanks to the multithread architecture other requests to `/` will be resolved before `/sleep` finishes.

#### Used Techniques

- Fixed to 4 threads to prevent creation of infinite threads.
- Management of a channel to be able to send and receive messages between threads.
- Correct clean up when shutting down the server if an error ocurrs.

#### Notes

- This is an example and it does not implement all robustness required for a production web server.
