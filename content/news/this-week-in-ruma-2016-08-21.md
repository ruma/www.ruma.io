+++
title = "This Week in Ruma"
date = 2016-08-21
extra.author = "Jimmy Cuadra"
+++

Apologies for the missed update last week!
I was sick and didn't get a chance to write it.
However, there was work on the project last week.
I will just include those changes in this update.

## Notable changes to [ruma](https://github.com/ruma/ruma)

* Previous work to update Diesel and Serde to the latest versions have been completed.
* Ruma now uses the types from [ruma-identifiers](https://github.com/ruma/ruma-identifiers) to represent Matrix IDs instead of strings.
* Ruma now uses the latest version of [ruma-events](https://github.com/ruma/ruma-events) which also uses ruma-identifiers.
* The Docker Compose file now locks the Ruma development image to a specific version, so breaking changes to the image are now coordinated with Ruma.
  As part of the same change, the image is now locked to a specific version of the nightly compiler.
* Database migrations are now embedded in the ruma binary, which means a check out of the source code is no longer necessary.
* Add initial support for the message event creation API.
  This is a big milestone and one of the core APIs that makes Matrix work!

## Notable changes to [ruma-events](https://github.com/ruma/ruma-events)

* Added simple type aliases for custom events of each kind (basic, room, and state events).
* I'm experimenting again with a version of the API where the event kinds are traits instead of generic structs.
  They really feel like they should be traits, but the actual usage pattern for the events in the main ruma application may not work well like this.

## Notable changes to [ruma-identifiers](https://github.com/ruma/ruma-identifiers)

* Crate version 0.3.0 was released, which implements `Clone` for the ID types and `Copy` for the error type.
* I'm working on a change that would allow the ID types to be used directly as struct fields for Diesel table types.
  Right now it seems like more trouble than it's worth, but I'm following the issue on [user-defined `FromSql`/`ToSql` types](https://github.com/diesel-rs/diesel/issues/348).

## Matrix at large

* Paul Evans of the Matrix team is working on testing Ruma with [SyTest](https://github.com/matrix-org/sytest), a blackbox integration testing framework for Matrix homeservers.
  Even though few of the APIs are complete in Ruma so far, there are already a few tests passing!
* [SPEC-442](https://matrix.org/jira/browse/SPEC-442): Explain requirements and guarantees around transaction IDs
* [SPEC-444](https://matrix.org/jira/browse/SPEC-444): Add an API for getting auth flows
  The May 22, 2016 news update mentioned that Vector and Synapse use unspecified APIs for negotiating authentication flows, but an issue was never filed for improving that.

## Rust at large

* Starting to think about how permissions checks will work in Ruma, I opened an issue for [transaction isolation support](https://github.com/diesel-rs/diesel/issues/408) in Diesel as a possible way to prevent ToCToU errors.
