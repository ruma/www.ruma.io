+++
title = "This Week in Ruma"
date = 2016-05-29
extra.author = "Jimmy Cuadra"
+++

## From the editor

In addition to the changes to `ruma` enumerated below, there was some great progress on the future user-facing documentation for Ruma.
My partner, who works as a technical writer, helped me brainstorm and outline what information people would need to understand Matrix and Ruma, how to get a copy of Ruma, configure it, and deploy it.
As always, needing to explain something simply to someone else forces you to understand it at a deeper level yourself.
I think the project is going to benefit greatly from some longer form explanations of of the what, why, and how of Matrix that aren't targeted at technical people.

## Notable changes to `ruma`

* Usage of the `try!` macro has been converted to using the new question mark syntax.

  Use of this unstable feature is one nice benefit of Ruma targeting nightly Rust.

* Added support for authentication with an access token.

  This is the mechanism which almost all endpoints that require authentication use.

* Added the `/logout` endpoint which revokes all access tokens associated with the user.

* Added the `/account/password` endpoint which lets the user change their account password.

  This endpoint uses both user-interactive authentication and access token authentication.
  The reasons for this were not clear to me, so I discussed it in #matrix-dev:matrix.org, and was able to distill the results of the discussion into [SPEC-407](https://matrix.org/jira/browse/SPEC-407).

* Moved and renamed various free functions into static methods on the types that they manipulate.

* Filled in some missing API documentation and added the `#![deny(missing_docs)]` attribute to make sure docs are added as new items are.

## Matrix at large

This week there was a story posted to Hacker News about how Google failed to recognize the value of Gchat, which resulted in the usual discussion of chat services that exist today.
I left a comment encouraging people to look at Matrix, and it generated a good amount of discussion and publicity for the project.
Be sure to read [the thread](https://news.ycombinator.com/item?id=11794914)!
