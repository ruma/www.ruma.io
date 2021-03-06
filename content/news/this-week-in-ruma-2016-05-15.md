+++
title = "This Week in Ruma"
date = 2016-05-15
extra.author = "Jimmy Cuadra"
+++

## From the editor

There were only a few commits this week, but there was very good progress on the test suite and some internals.
After trying several ways to work around libtest's lack of global setup and teardown hooks, and some issues with the way each test was running an Iron server in a thread keeping database connections open forever, I decided to move the setup and teardown outside of the Rust code itself.
I explored the code of libtest and libsyntax and got to understand how it works and some of its limitations.
I might be creating an RFC for Rust soon to give the programmer independent control of the test collector and the test runner, which are currently bound together under the `--test` flag (AKA `--cfg test`.)

Now the PostgreSQL Docker container is started and stopped, and database migraitons are run from a shell script which wraps `cargo test`.
The Iron app was similarly decoupled from the Iron server, so that integration testing can be done with `iron-test` without ever starting an actual server.
Finally, I made some more progress on Matrix's user-interactive authentication system and got part of the `/login` endpoint completed.
I expect it to be fully functional by next week.

## Notable changes to `ruma`

* Cleaned up test suite

  Complicated setup and teardown extracted from the Rust code.
  Test cases moved into the modules they test, rather than within a `tests`-directory-style module in `src/test`.

* Introduced `iron-test` to facilitate testing

  The test suite now has a single support type, `test::Test`, which does per-test setup and teardown via RAII and provides succinct helper methods for making requests and testing the responses.

* Initial version of the `/login` API added.

  The logic is all there, but there are some places where deserialization of the types used in the request body must be manually implemented because they differ in structure from what Serde can do with its custom derive attributes.

## Matrix at large

The sections about authentication, registration, and login in the spec have seen some very nice improvements recently, but there are still some parts that are misleading or unclear.
I'm in the process of getting a few things clarified that will help finally nail down how these various APIs should work.
