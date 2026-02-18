Bitcoin Core, also known by its process name `bitcoind`, is by far the most popular implementation of a Bitcoin node. It is written in C++ and as of today available as version 29.0. It is a descendant of the "original" Bitcoin implementation, released in January 2009 by Satoshi Nakamoto. The source code can be found on the project's website [bitcoincore.org](https://bitcoincore.org/) as well as the [Github repository.](https://github.com/bitcoin/bitcoin).

- [Unix Build Notes](https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md)

On Ubuntu, there are three ways we can download the Bitcoin Core software:

- From source, meaning built from the raw source code
- As a binary from the project's website, meaning as a program ready to be executed
- As a binary from a software repository, similar to an app store

Downloading the program from an app store is the most convenient way, but it also requires trust in that app store, as we won't be able to perfectly verify what code we will be running. Downloading the program from the project's site mainly puts trust into the competence of the individuals that compiled the software for us. Compiling from source minimizes trust and (theoretically) allows us to verify line by line what code we will be running on our machine.

As enthusiasts of open source and self-sovereign software, we will recommend installing Bitcoin Core from source, but will also document the other options here for your convenience.

Compiling software can be understood a bit like baking a cake. We take the raw ingredients, that is math and information, and mix it in a way defined by the recipe, which we download in form of the source code. How exactly we read this recipe depends on the project's programming language.

[[Automatically Attach a Volume to your Machine]]
[[Connect to your node]]
