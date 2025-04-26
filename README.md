# gmartiblog.com

This project hosts content for my blog.

The [gmartiblog.com](https://gmartiblog.com) blog mainly uses [Markdown](https://commonmark.org/help/) but explores [AsciiDoc](https://asciidoc.org/), as well. Both formats use plain text to add structure to documents. Markdown, though, almost always needs help from HTML. The format doesn't have the ability to make complex tables, collapsible sections, or definition lists. AsciiDoc doesn't need the added HTML. It can make all those features with only AsciiDoc markers. This keeps the raw code behind the rendered documents easy to read.

To create the blog, this project uses [Jekyll](https://jekyllrb.com/) and [Vale](https://vale.sh/). Jekyll renders all Markdown and AsciiDoc documents into static blog pages. This controls how the documents look to viewers in their browser. Vale lints these documents to keep them error-free. It checks for spelling issues, grammatical errors, over-complicated content, and more. Together, they convert the plain text documents in this repository into a vibrant, well-structured blog for my technical writing projects.

The rest of this README page describes how to build this project on your local computer and add changes to the gmartiblog.com platform. The page assumes you work in either a Linux-based or macOS environment.

## How to build this project locally

Build the site on your local computer to see how Jekyll renders your document. Check, or lint, your document for grammatical or spelling errors before committing it.

### Install dependencies

Follow the instructions for your operating system to install Jekyll and [Bundler](https://bundler.io/).

<details>
<summary>Linux, Ubuntu, or Debian</summary>

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
    cd gmarti-web.github.io.git
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
<summary>Linux, Ubuntu, or Debian</summary>

1. For Linux and Debian, you must install the [Snapcraft](https://snapcraft.io/) daemon. For Ubuntu, which has the daemon pre-installed, skip to step two.

    1. For Linux, remove the `nosnap.pref` file from your native package manager's preference folder. For Debian, skip to step ii.

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

1. Install Vale

    ```console
    snap install vale
    ```

This installs Vale and adds it to your `$PATH` variable.

To lint AsciiDoc files, install the `asciidoc` and `asciidoctor` packages, as well.

```console
sudo apt install asciidoc asciidoctor -y
```

</details>

<details>
<summary>macOS</summary>

1. Install [HomeBrew](http://brew.sh/).

    ```console
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

1. Install Vale

    ```console
    brew install vale
    ```

This installs Vale and adds it to your `$PATH` variable.

To lint AsciiDoc files, install the `asciidoc` and `asciidoctor` packages, as well.

```console
brew install asciidoc asciidoctor
```

</details>

To learn more about installing Vale, see [Install–Vale CLI](https://vale.sh/docs/install).

After you install Vale, install the packages listed in the `.vale.ini` file:

```console
vale sync
```

To lint a single file, run the following command:

```console
vale path/to/document.{md,adoc}
```

To lint all the files in a folder, run the following command:

```console
vale path/to/folder/
```

## How to contribute to the project

To contribute to the project:

1. [Find an issue](https://github.com/gmarti-web/gmarti-web.github.io/issues) you want to work on. If one doesn't exist, [create one](https://github.com/gmarti-web/gmarti-web.github.io/issues/new?template=feature-request.yml).
1. Check out the repository.
1. Create a new branch that describes your work.

    ```console
    git checkout -b my-branch
    ```

1. [Build the project on your local computer](#how-to-build-this-project-locally).
1. Make your changes, test them on your local server, and then lint for writing errors.
1. Push your changes to a new remote branch.
1. Create a new pull request.

The code owner reviews the pull request. If approved, they'll merge the changes into the main branch. If not, they'll add their feedback to the pull request.

