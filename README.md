# gmartiblog.com

This repository hosts content for my blog.

The [gmartiblog.com](https://gmartiblog.com) blog mainly uses [Markdown](https://commonmark.org/help/) but explores [AsciiDoc](https://asciidoc.org/), as well. Both formats use plain text to add structure to documents. Markdown, though, almost always needs help from HTML. The format doesn't have the ability to make complex tables, collapsible sections, or definition lists. AsciiDoc doesn't need the added HTML. It can do all that with only AsciiDoc markers. This keeps the raw code behind the rendered documents easy to read.

[Jekyll](https://jekyllrb.com/) renders all Markdown and AsciiDoc documents into static blog pages.

## How to build

Build the site on your local computer to see how Jekyll renders your document.

Follow the instructions for your operating system to install Jekyll and [Bundler](https://bundler.io/).

### Install dependencies

<details>
<summary>Ubuntu or Debian</summary>

1. Install Ruby and prerequisites:

  ```console
  sudo apt-get install ruby-full build-essential zlib1g-dev
  ```

1. Add a gem installation directory for your user account to your `~/.bashrc` file.

  ```console
  echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
  echo 'export PATH="$PATH:$HOME/gems/bin"' >> ~/.bashrc
  source ~/.bashrc
  ```

1. Install Jekyll and Bundler.

  ```console
  gem install jekyll bundler
  ```

To learn more about installing Jekyll on Ubuntu, see [Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/).

</details>

{% capture MacOs %}

1. Install [HomeBrew](http://brew.sh/)).

  ```console
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  ```

1. Install `chruby` and the latest Ruby version.

  ```console
  brew install chruby ruby-install
  ```

  ```console
  ruby-install ruby 3.4.1
  ```

1. Configure your shell to use `chruby`.

  ```console
  echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.bash_profile
  echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.bash_profile
  echo "chruby ruby-3.4.1" >> ~/.bash_profile
  source ~/.bash_profile
  ```

1. Install Jekyll and Bundler

  ```console
  gem install jekyll bundler
  ```

To learn more about installing Jekyll on macOS, see [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/).

{% endcapture %}

<details>
<summary>macOS</summary>
{{ MacOs | markdownify }}
</details>

For a complete list of installation methods, see [Installing Ruby](https://www.ruby-lang.org/en/documentation/installation/).

<details>
<summary>Install Ruby and download the <code>bundle</code> package manager</summary>

</details>

<details>
<summary>Download `jekyll`</summary>
</details>

### Jekyll serve

## How to contribute

