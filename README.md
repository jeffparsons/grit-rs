[![Rust](https://github.com/Byron/grit-rs/workflows/Rust/badge.svg)](https://github.com/Byron/grit-rs/actions)

**grit** is a command-line interface (*CLI*) to access git repositories. It's written to optimize the
user-experience, and perform as good or better than the native implementation.

The CLI uses various libraries to implement

 * [ ] a git *repository* and *references* (see `git-core`)
 * [ ] a git object database (see `git-odb` and
   [examples](https://github.com/Byron/grit-rs/tree/master/lib/git-odb/examples))
 * [ ] a transport layer for push and pull (see `git-transport`)

 **This project is early in development and currently strictly for fun**
 
 **Currently I am implementing whatever is needed to set a new record for solving
 [this
 problem](https://github.com/gitpython-developers/GitPython/issues/765#issuecomment-396072153)**

## Tasks

* **git-core**
  * **Repository**
    * [x] initialize
    * [ ] references
    * [ ] index
    * [ ] odb
    * [ ] remotes with push and pull
    * [ ] merging
    * [ ] configuration
* **git-odb**
  * **loose objects**
    * [x] traverse
    * [-] decode
      * [ ] commit
      * [ ] tree
      * [x] tag
      * [ ] blob
    * [ ] encode
      * [ ] commit
      * [ ] tree
      * [ ] tag
      * [ ] blob
  * **packs**
    * [x] traverse pack index
    * [x] decode pack entries
    * [ ] decode
      * [ ] full objects
      * [ ] deltified objects
    * [ ] create new packs
* **git-transport**
  * [ ] via ssh
    * [ ] push
    * [ ] pull
  * [ ] via https
    * [ ] push
    * [ ] pull

## Installation

**TBD**

## Project Goals

 * **a pure-rust implementation of git**
   * including *transport*, *object database*, *references* and *cli*
   * a simple command-line interface is provided for the most common git operations, optimized for
     user experience. A *simple-git* if you so will.
   * be the go-to implementation for anyone who wants to solve problems around git, and become
     *the* alternative to `GitPython` in the process.
   * become the foundation for a free distributed alternative to github.
 * **learn from the best to write the best possible idiomatic Rust**
   * *libgit2* is a fantastic resource to see what abstractions work, we will use them
   * use Rust's type system to make misuse impossible
 * **be the best performing implementation**
   * use Rust's type system to optimize for work not done without being hard to use
   * use multiple cores when available
 * **assure on-disk consistency**
   * assure reads never interfere with concurrent writes
   * assure multiple concurrent writes don't cause trouble
 * **take shortcuts, but not in quality**
   * binaries my use `anyhow::Error` exhaustively, knowing that these errors are solely user-facing.
   * internationalization is nothing we are concerned with right now

## Non-Goals

 * **replicate `git` command functionality perfectly**
   * `git` is `git`, and there is no reason to not use it. Our path is the one of simplicity to make
     getting started with git easy.
 * **be incompatible to git**
   * the on-disk format must remain compatible, and we will never contend with it.
 * **use async IO everywhere**
   * it's too young and makes things so much more difficult right now.
   * (it's considered on option as upgrade when async is stabilized)

## Roadmap to Future

As you can see from the version numbers, this project dispenses major version generously.

### Roadmap to 1.0

Provide a CLI to for the most basic user journey:

* [ ] initialize a repository
* [ ] create a commit
* [ ] add a remote
* [ ] push
 
## Development Practices

 * **test-first development**
   * protect against regression and make implementing features easy
   * user docker to test more elaborate user interactions
   * keep it practical, knowing that the Rust compiler already has your back
     for the mundane things, like unhappy code paths.
   * *use git itself* as reference implementation, and use their test-cases and fixtures where
     appropriate
   * *use libgit2* test fixtures and cases where appropriate
 * **safety first**
   * handle all errors, never unwrap
   * provide an error chain and make it easy to understand what went wrong.
 * **strive for an MVP and version 1.0 fast...**
   * ...even if that includes only the most common usecases.
 * **Prefer to increment major version rapidly...**
   * ...instead of keeping major version zero for longer than needed.

## Maintenance Guide

*TBD*
