# CoCart Documentation

This is the repository for the CoCart documentation.

The documenation is powered by [Slate](https://github.com/lord/slate).

If you would like to contribute to the documentation to either correct a mistake, maybe add another language or something else. Then please follow these [contribution guidelines](https://github.com/co-cart/co-cart-docs/blob/master/CONTRIBUTING.md).

## Getting Started

#### Requirements

You're going to need:

 - **Linux or macOS** — Windows may work, but is unsupported.
 - **Ruby, version 2.3.1 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

#### Getting Set Up

1. Fork this repository on GitHub.
2. Clone *your forked repository* (not this original one) to your hard drive with `git clone https://github.com/YOURUSERNAME/co-cart-docs.git`
3. `cd co-cart-docs`
4. Initialize and start Slate. You can either do this locally, or with Vagrant:

```shell
# either run this to run locally
bundle install
bundle exec middleman server

# OR run this to run with vagrant
vagrant up
```

You can now see the docs at http://localhost:4567.

