# Repository to reproduce an issue with `cargo-watch` and Rust 1.66+

## Description of the issue

The process created by the `cargo-watch` binary (when installed with Rust version 1.66 or later), does not terminate when receiving an interruption or termination signal. However, the same process terminates correctly when `cargo-watch` is installed with Rust version 1.65 or earlier.

Tested on a MacBook Pro M1 with Ventura 13.1

## Steps to reproduce the error

Install `cargo-watch` with Rust 1.66+ toolchain:  
`cargo +1.66 install --force cargo-watch`

Launch the `cargo-watch` command:  
`cargo watch --debug -x run`

Stop the processus (either with Ctrl-c on the ongoing `cargo-watch` process or `pkill cargo-watch`)

You can see that the signal has been sent according to the logs `DEBUG - Sending signal SIGTERM to process group id=1234` but the processes in group `1234` have not been terminated.

(You can test that everything is working fine by using `cargo-watch` installed with a Rust version 1.65, i.e. `cargo +1.65 install --force cargo-watch`)

Issue created here: https://github.com/watchexec/cargo-watch/issues/249
