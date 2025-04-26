# gmartiblog.com

This project hosts content for my blog.

The [gmartiblog.com](https://gmartiblog.com) blog mainly uses [Markdown](https://commonmark.org/help/) but explores [AsciiDoc](https://asciidoc.org/), as well. Both formats use plain text to add structure to documents. Markdown, though, almost always needs help from HTML. The format doesn't have the ability to make complex tables, collapsible sections, or definition lists. AsciiDoc doesn't need the added HTML. It can make all those features with only AsciiDoc markers. This keeps the raw code behind the rendered documents easy to read.

To create my blog, this project uses [Jekyll](https://jekyllrb.com/) and [Vale](https://vale.sh/). Jekyll renders all Markdown and AsciiDoc documents into static blog pages. This controls how the documents look to viewers in their browser. Vale lints these documents to keep them error-free. It checks for spelling issues, grammatical errors, over-complicated content, and more. Together, they convert the plain text documents in this repository into a vibrant, well-structured blog for my technical writing projects.

The rest of this README page describes how to build this project on your local computer and add changes to the gmartiblog.com platform.

## How to build this project locally

Build the site on your local computer to see how Jekyll renders your document. Check, or lint, your document for grammatical or spelling errors before committing it.

### Install dependencies

Follow the instructions for your operating system to install Jekyll and [Bundler](https://bundler.io/).

<details>
<summary>Linux, Ubuntu, or Debian</summary>

To install Jekyll and Bundler on Linux, Ubuntu, or Debian:

1. Install Ruby and prerequisites:

    ```console
    sudo apt-get install ruby-full build-essential zlib1g-dev
    ```

2. Add a gem installation directory for your user account to your `~/.bashrc` file.

    ```console
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
    echo 'export PATH="$PATH:$HOME/gems/bin"' >> ~/.bashrc
    source ~/.bashrc
    ```

3. Install Jekyll and Bundler.

    ```console
    gem install jekyll bundler
    ```

To learn more about installing Jekyll on Ubuntu, see [Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/).

</details>

<details>
<summary>macOS</summary>

To install Jekyll and Bundler on macOS:

1. Install [HomeBrew](http://brew.sh/).

    ```console
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

2. Install `chruby` and the latest Ruby version.

    ```console
    brew install chruby ruby-install
    ```

    ```console
    ruby-install ruby 3.4.1
    ```

3. Configure your shell to use `chruby`.

    ```console
    echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.bash_profile
    echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.bash_profile
    echo "chruby ruby-3.4.1" >> ~/.bash_profile
    source ~/.bash_profile
    ```

4. Install Jekyll and Bundler

    ```console
    gem install jekyll bundler
    ```

To learn more about installing Jekyll on macOS, see [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/).

</details>

For a complete list of installation methods, see [Installing Ruby](https://www.ruby-lang.org/en/documentation/installation/).

### Install gems from `Gemfile`

This project's `Gemfile` lists all the gems that this project needs. You only need to install these gems the first time you build the site.

To install the needed gems:

1. In your terminal, go to the project's root folder.

    ```console
    git clone https://github.com/gmarti-web/gmarti-web.github.io.git
    cd gmarti-web.github.io.gi
    ```

2. Set the local gem folder.

    This keeps the gems you install for this project scoped to this folder.

    ```console
    bundle config path 'vendor/bundle' --local
    ```

3. Install the project's required gems from the `Gemfile`.

    ```console
    bundle install
    ```

This installs this project's gems to a local folder called `vendor/bundle`.

### Start the server

After you install the gems, use `bundle` to start the Jekyll server:

```console
bundle exec jekyll serve
```

To see the rendered site, go to [http://localhost:4000](http://localhost:4000).

### Install Vale

This project uses Vale to check, or lint, for any writing errors.

To install Vale, use your operating system's package manager.

<details>
<summary>macOS</summary>

To install Vale on macOS:

1. Install [HomeBrew](http://brew.sh/).

    ```console
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

1. Install Vale

    ```console
    brew install vale
    ```

This installs Vale and adds it to your `$PATH` variable.

</details>

<details>
<summary>Linux, Ubuntu, or Debian</summary>

To install Vale on Linux:

1. Install [Snapcraft](https://snapcraft.io/).

    1. Remove the `nosnap.pref` file from your native package manager's preference folder.

        ```console
        sudo mv /etc/apt/preferences.d/nosnap.pref ~/Documents/nosnap.bkp
        ```

    1. Update `apt`.

        ```console
        sudo apt update
        sudo apt upgrade -y
        ```

    1. Install `snapd`.

        ```console
        sudo apt install snapd
        ```

    To test the installation, install and run the [hello-world](https://snapcraft.io/hello-world) snap.

    ```console
    snap install hello-world
    hello-world
    ```

    If the installation was successful, the `hello-world` command prints:

    ```console
    Hello World!
    ```

## How to contribute to the project

