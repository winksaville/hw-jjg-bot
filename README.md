# hw-jjg-bot

This is an experiment using two jj-git repos, one for the
app code and one for the bot session information.
The goal is to allow the bot to manipulate the app code,
app repo and bot session repo.

In a previous experiment, where there is only one repo for both
the app code and bot session information, kinda worked. But the bot
could not commit the session information because of circular references.
Instead it would commit the app code and I'd amend the commit adding
the bots session information. Also, things like merging was impossible.
I believe splitting them into two repos might solve at least some
of these problems.

The package root is the repo for the application code and in this
document it will be designated as `/`.

The bots session information is in a nested repo, `/.claude`.

Here are basically the steps used to create these repos:

Note: I'm explicitlly ignoring .jj and .git to be obvious although
it maybe unnecessary.

```
wink@fwlaptop 26-02-28T17:53:24.215Z:~
$ cd data/prgs/rust
wink@fwlaptop 26-02-28T17:53:50.464Z:~/data/prgs/rust
$ cargo new --lib hw-jjg-bot
    Creating library `hw-jjg-bot` package
note: see more `Cargo.toml` keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html
wink@fwlaptop 26-02-28T18:04:16.367Z:~/data/prgs/rust
$ cd hw-jjg-bot/
wink@fwlaptop 26-02-28T18:04:21.786Z:~/data/prgs/rust/hw-jjg-bot (main)
$ claude-symlink.sh .claude
Created target directory: .claude
Created: /home/wink/.claude/projects/-home-wink-data-prgs-rust-hw-jjg-bot -> /home/wink/data/prgs/rust/hw-jjg-bot/.claude
wink@fwlaptop 26-02-28T18:08:14.543Z:~/data/prgs/rust/hw-jjg-bot (main)
$ cp ~/data/prgs/licenses/README-APACHE-MIT-LICENSE.md README.md
wink@fwlaptop 26-02-28T18:09:43.194Z:~/data/prgs/rust/hw-jjg-bot (main)
$ cp ~/data/prgs/licenses/LICENSE-APACHE .
wink@fwlaptop 26-02-28T18:09:56.464Z:~/data/prgs/rust/hw-jjg-bot (main)
$ cp ~/data/prgs/licenses/LICENSE-MIT .
wink@fwlaptop 26-02-28T18:10:00.578Z:~/data/prgs/rust/hw-jjg-bot (main)
$ printf '/target\n/.claude\n/.git\n/.jj\n' > .gitignore
wink@fwlaptop 26-02-28T18:30:55.433Z:~/data/prgs/rust/hw-jjg-bot (main)
$ printf '/.git\n/.jj\n' > .claude/.gitignore
wink@fwlaptop 26-02-28T18:30:59.193Z:~/data/prgs/rust/hw-jjg-bot (main)
$ jj st
Working copy changes:
A .gitignore
A Cargo.toml
A LICENSE-APACHE
A LICENSE-MIT
A README.md
A src/lib.rs
Working copy  (@) : tvyzspys 5ce8f2d7 (no description set)
Parent commit (@-): zzzzzzzz 00000000 (empty) (no description set)
wink@fwlaptop 26-02-28T18:38:09.658Z:~/data/prgs/rust/hw-jjg-bot (main)
$ cd .claude/
wink@fwlaptop 26-02-28T18:38:14.766Z:~/data/prgs/rust/hw-jjg-bot/.claude (main)
$ jj st
Working copy changes:
A .gitignore
Working copy  (@) : srsprxym 72d59336 (no description set)
Parent commit (@-): zzzzzzzz 00000000 (empty) (no description set)
wink@fwlaptop 26-02-28T18:38:17.829Z:~/data/prgs/rust/hw-jjg-bot/.claude (main)
```

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE) or http://apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the work by you, as defined in the Apache-2.0 license, shall
be dual licensed as above, without any additional terms or conditions.
