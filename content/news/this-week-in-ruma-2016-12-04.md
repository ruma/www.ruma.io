+++
title = "This Week in Ruma"
date = 2016-12-04
extra.author = "Jimmy Cuadra"
+++

## From the editor

We had a very productive week, landing several pull requests, including a major revamp of ruma-events and new APIs.

A very important milestone was reached: The number of unstable Rust features Ruma uses was reduced from six to two!
Ruma was migrated to the new Macros 1.1 approach for custom derive, which meant we were able to drop the `custom_attribute`, `custom_derive`, and `plugin` features.
As part of the integration of the ruma-events revamp, `specialization` was also removed.
With `question_mark` now stable, Ruma uses only `proc_macro` (Macros 1.1, which will be stable in a few more releases) and `try_from`, which I hope to see movement on soon.
The day that Ruma can target stable Rust is approaching!

The revamp of ruma-events changed the design of the library, so each of the kinds of event in Matrix (events, room events, and state events) are now traits rather than structs with two generic parameters.
This change took quite a while, so I'm happy to have it finally integrated into Ruma.

## Notable changes to [ruma](https://github.com/ruma/ruma)

* Added support for local room invitations.
* Removed unstable features: `custom_attribute`, `custom_derive`, `plugin`, and `specialization`.
* Updated to Macros 1.1 versions of Serde and Diesel.

## Notable changes to [ruma-events](https://github.com/ruma/ruma-events)

* `Event`, `RoomEvent`, and `StateEvent` are now traits.

## Notable changes to [ruma-identifiers](https://github.com/ruma/ruma-identifiers)

* Released crate version 0.4.3, a small bump to update dependencies.

## Call for participation

Here are a couple of items to check out if you're interested in contributing to the project:

* For implementation: [Implement the Into\<Option\> trick for ApiError.](https://github.com/ruma/ruma/issues/115).
* For review and discussion: [Add types to support heterogeneous collections of events](https://github.com/ruma/ruma-events/pull/5).
