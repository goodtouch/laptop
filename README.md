Laptop
======

Laptop is a script to set up an macOS laptop for web and mobile development.

It can be run multiple times on the same machine safely.
It installs, upgrades, or skips packages
based on what is already installed on the machine.

Requirements
------------

We support:

* macOS Mavericks (10.9)
* macOS Yosemite (10.10)
* macOS El Capitan (10.11)
* macOS Sierra (10.12)

Older versions may work but aren't regularly tested.
Bug reports for older versions are welcome.

Install
-------

Download the script:

```sh
curl --remote-name https://raw.githubusercontent.com/goodtouch/laptop/master/mac
```

Review the script (avoid running scripts you haven't read!):

```sh
less mac
```

Execute the downloaded script:

```sh
sh mac 2>&1 | tee ~/laptop.log
```

Optionally, review the log:

```sh
less ~/laptop.log
```

Optionally, [install thoughtbot/dotfiles][dotfiles].

[dotfiles]: https://github.com/thoughtbot/dotfiles#install

Debugging
---------

Your last Laptop run will be saved to `~/laptop.log`.
Read through it to see if you can debug the issue yourself.

What it sets up
---------------

macOS tools:

* [Homebrew] for managing operating system libraries.

[Homebrew]: http://brew.sh/

Unix tools:

* [Git] for version control
* [iTerm2] replacement for Terminal
* [OpenSSL] for Transport Layer Security (TLS)
* [The Silver Searcher] for finding things in files
* [Tmux] for saving project state and switching between projects
* [reattach-to-user-namespace] Reattach process (e.g., tmux) to background (Fix Copy & Paste in Tmux)
* [Universal Ctags] for indexing files for vim tab completion
* [Watchman] for watching for filesystem events
* [Zsh] as your shell
* [z] to navigate to your most used directories

[Git]: https://git-scm.com/
[iTerm2]: https://www.iterm2.com/
[OpenSSL]: https://www.openssl.org/
[The Silver Searcher]: https://github.com/ggreer/the_silver_searcher
[Tmux]: http://tmux.github.io/
[reattach-to-user-namespace]: https://github.com/ChrisJohnsen/tmux-MacOSX-pasteboard
[Universal Ctags]: https://github.com/universal-ctags/ctags
[Watchman]: https://facebook.github.io/watchman/
[Zsh]: http://www.zsh.org/
[z]: https://github.com/rupa/z

Image tools:

* [ImageMagick] for cropping and resizing images

Testing tools:

* [ChromeDriver] for headless JavaScript testing via [Capybara] and [Selenium Webdriver]

[ChromeDriver]: https://sites.google.com/a/chromium.org/chromedriver/
[Capybara]: https://github.com/teamcapybara/capybara
[Selenium Webdriver]: https://github.com/teamcapybara/capybara#selenium

Programming languages, package managers, and configuration:

* [ASDF] for managing programming language versions
* [Bundler] for managing Ruby libraries
* [Java]: for writing Android applications
* [Node.js] and [NPM], for running apps and installing JavaScript packages
* [Ruby] stable for writing general-purpose code
* [Yarn] for managing JavaScript packages

[Bundler]: http://bundler.io/
[ImageMagick]: http://www.imagemagick.org/
[Node.js]: http://nodejs.org/
[NPM]: https://www.npmjs.org/
[ASDF]: https://github.com/asdf-vm/asdf
[Ruby]: https://www.ruby-lang.org/en/
[Java]: http://www.oracle.com/technetwork/java/
[Yarn]: https://yarnpkg.com/en/

Databases:

* [Postgres] for storing relational data
* [MySQL] for storing relational data
* [SQLite] for storing relational data
* [Redis] for storing key-value data

[Postgres]: http://www.postgresql.org/
[MySQL]: https://www.mysql.com/
[SQLite]: https://www.sqlite.org
[Redis]: http://redis.io/

Editors:

* [Visual Studio Code]: Microsoft hackable text editor
* [Vim]: Vi "workalike" with many additional features

[Visual Studio Code]: https://code.visualstudio.com/
[Vim]: http://www.vim.org/

Mobile development tools:

* [Android Platform Tools]: Tools for the Android SDK
* [Android Studio]: Official IDE for Android

[Android Platform Tools]: https://developer.android.com/sdk
[Android Studio]: https://developer.android.com/studio/index.html

Source code management:

* [GitX-dev]: fork of GitX with some nice improvements

[GitX-dev]: https://rowanj.github.io/gitx/

Virtualization & Containerization:

* virtualbox
* vagrant

Graphics & Design:

* sketch
* sketch-beta

Media

* spotify

Team & Chat:

* Discord
* Mattermost
* Skype
* Slack

Sync & Cloud:

* Dropbox
* Google-drive
* Resilio-sync
* Sparkleshare

Firewall:

* little-snitch

Fonts:

* fontforge
* font-source-code-pro
* font-source-code-pro-for-powerline

It should take less than 15 minutes to install (depends on your machine).

Customize in `~/.laptop.local`
------------------------------

Your `~/.laptop.local` is run at the end of the Laptop script.
Put your customizations there.
For example:

```sh
#!/bin/sh

brew bundle --file=- <<EOF
brew "Caskroom/cask/dockertoolbox"
brew "go"
brew "ngrok"
brew "watch"
EOF

default_docker_machine() {
  docker-machine ls | grep -Fq "default"
}

if ! default_docker_machine; then
  docker-machine create --driver virtualbox default
fi

default_docker_machine_running() {
  default_docker_machine | grep -Fq "Running"
}

if ! default_docker_machine_running; then
  docker-machine start default
fi

fancy_echo "Cleaning up old Homebrew formulae ..."
brew cleanup
brew cask cleanup

if [ -r "$HOME/.rcrc" ]; then
  fancy_echo "Updating dotfiles ..."
  rcup
fi
```

Write your customizations such that they can be run safely more than once.
See the `mac` script for examples.

Laptop functions such as `fancy_echo` and
`gem_install_or_update`
can be used in your `~/.laptop.local`.

See the [wiki](https://github.com/thoughtbot/laptop/wiki)
for more customization examples.

.laptop.local.example
---------------------

In the `.laptop.local.example` file, you'll find how to customize your `.laptop.local` file to install:

Programming languages, package managers, and configuration:

* [Elixir] and [Erlang] stable
* [Go] stable

[Elixir]: http://elixir-lang.org/
[Erlang]: https://www.erlang.org/
[Go]: https://golang.org/

Contributing
------------

Edit the `mac` file.
Document in the `README.md` file.
Follow shell style guidelines by using [ShellCheck] and [Syntastic].

```sh
brew install shellcheck
```

[ShellCheck]: http://www.shellcheck.net/about.html
[Syntastic]: https://github.com/scrooloose/syntastic

Thank you, [contributors]!

[contributors]: https://github.com/thoughtbot/laptop/graphs/contributors

By participating in this project,
you agree to abide by the thoughtbot [code of conduct].

[code of conduct]: https://thoughtbot.com/open-source-code-of-conduct

License
-------

Laptop is © 2011-2017 thoughtbot, inc.
It is free software,
and may be redistributed under the terms specified in the [LICENSE] file.

[LICENSE]: LICENSE

About thoughtbot
----------------

![thoughtbot](http://presskit.thoughtbot.com/images/thoughtbot-logo-for-readmes.svg)

Laptop is maintained and funded by thoughtbot, inc.
The names and logos for thoughtbot are trademarks of thoughtbot, inc.

We are passionate about open source software.
See [our other projects][community].
We are [available for hire][hire].

[community]: https://thoughtbot.com/community?utm_source=github
[hire]: https://thoughtbot.com?utm_source=github
