# gmartiblog.com

This repo hosts content for my personal blog.

The [gmartiblog.com][1] blog uses [Markdown][2] and [AsciiDoc][3]. Both formats add structure to documents with plain text. However, Markdown needs help from HTML to make complex tables, collapsible sections, or definition lists, whereas AsciiDoc can make those features itself. By replacing the HTML code in Markdown files with plain text, AsciiDocs keep the raw code behind the rendered documents easy to read.

To create the blog, this project uses [Vale][5] and [Jekyll][4]. First, Vale checks each document for spelling issues, grammatical errors, and over-complicated sentences. Then, Jekyll renders the documents into static HTML pages. Together, Vale and Jekyll convert the plain text documents in this repository into a vibrant, well-structured blog for my technical writing projects.

This page describes how to build this project on your local computer and add changes to gmartiblog.com. The page assumes you work in either a Linux-based or macOS environment.

## How to contribute to this project

To contribute to the project:

1. [Find an issue][6] you want to work on. If one doesn't exist, [create one][7].
1. Check out the repository.

    ```console
    git clone https://github.com/gmarti-web/gmarti-web.github.io
    cd gmarti-web.github.io
    ```
1. Create a new branch that describes your work.

    ```console
    git checkout -b my-branch
    ```

1. Make your changes and lint for writing errors.

    ```console
    vale path/to/file.md
    ```

    * Lint for errors after each set of changes.

1. Commit your changes. Include a descriptive commit message.

    ```console
    git add path/to/file.md
    git commit -m 'your commit message'
    ```
1. Push your changes to GitHub.

    ```console
    git push -u origin my-branch
    ```

    * This command adds your changes to a new branch in GitHub.

1. Create a new pull request to merge your branch into the `main` branch.

The code owner reviews your request for consistency, clarity, and correctness. If they approve the request, they merge the changes into the `main` branch. If they reject the request, they add their feedback to the pull request and ask you to revise it.

## How to build this project locally

Build the site on your local computer to see how Jekyll renders your document. Check, or lint, your document for grammatical or spelling errors before committing it.

### Install dependencies

Follow the instructions for your operating system to install [Ruby][12], Jekyll, and [Bundler][8].

Bundler and Ruby manage the packages, called "gems," that Jekyll needs to render the site.

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

To learn more about installing Jekyll on Ubuntu, see [Jekyll on Ubuntu][9].

</details>

<details>
<summary>macOS</summary>

1. Install [HomeBrew][10].

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

4. Install Jekyll and Bundler.

    ```console
    gem install jekyll bundler
    ```

To learn more about installing Jekyll on macOS, see [Jekyll on macOS][11].

</details>

<details>
<summary>Windows</summary>

Jekyll doesn't officially support Windows. You can, though, install Jekyll with the [RubyInstaller][14].

1. Download and install the recommended Ruby+Devkit version from [RubyInstaller downloads][15].

  * Use the default options.

1. Run the `ridk install` step from the installation wizard. From the options, choose `MSYS2 and MINGW development toolchain`.
1. Open a new terminal and install Jekyll and Bundler.

  ```console
  gem install jekyll bundler
  ```

1. Run `jekyll -v` to check the installation.

To learn more about installing Jekyll on Windows, see [Jekyll on Windows][16].

</details>

### Install gems from `Gemfile`

The `Gemfile` lists all the gems that this project needs. You only need to install these gems the first time you build the site.

To install the gems:

1. In your terminal, go to the project's root folder.

    ```console
    cd gmarti-web.github.io
    ```

2. Set the local gem folder.

    ```console
    bundle config path 'vendor/bundle' --local
    ```

    * This keeps the gems you install for this project scoped to this folder.

3. Install the project's required gems from the `Gemfile`.

    ```console
    bundle install
    ```

This installs this project's gems to a local folder called `vendor/bundle`.

### Start the server

After you install the gems, start a local server to see your rendered changes.

Use `bundle` to start the Jekyll server:

```console
bundle exec jekyll serve
```

To see the rendered site, go to [http://localhost:4000][13].

### Install Vale

This project uses Vale to check, or lint, for any writing errors. To keep content error free, lint each change before you push it to GitHub.

To install Vale, use your operating system's package manager.

<details>
<summary>Linux, Ubuntu, or Debian</summary>

1. For Linux and Debian, you must install the [Snapcraft][20] daemon. For Ubuntu, which has the daemon pre-installed, skip to step two.

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

1. Install Vale.

    ```console
    snap install vale
    ```

1. Run `vale -v` to check that the installation succeeded.

This installs Vale and adds it to your `$PATH` variable.

</details>

<details>
<summary>macOS</summary>

1. Install [HomeBrew][10].

    ```console
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```

1. Install Vale.

    ```console
    brew install vale
    ```

1. Run `vale -v` to check that the installation succeeded.

This installs Vale and adds it to your `$PATH` variable.

</details>

<details>
<summary>Windows</summary>

1. Install [Chocolatey][17].

    1. [Open a PowerShell terminal as an administrator][19]. To install as a non-admin, see Chocolatey's documentation on [non-administrative installation][18]
    1. Run `Get-ExecutionPolicy`.

        * If it returns `Restricted`, run `Set-ExecutionPolicy Bypass -Scope Process`.

    1. Install Chocolatey.

        ```powershell
        Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
        ```

    1. Run `choco` to check that the installation succeeded.

1. Install Vale.

    ```console
    choco install vale
    ```

1. Run `vale -v` to check that the installation succeeded.

This installs Vale and adds it to your `%PATH%` variable.

</details>

To learn more about installing Vale, see [Install–Vale CLI][21].

After you install Vale, install the packages listed in the `.vale.ini` file:

```console
vale sync
```
To lint AsciiDoc files, install the `asciidoc` and `asciidoctor` packages, as well.

```console
gem install asciidoctor asciidoctor-pdf
```

To lint a single file, run the following command:

```console
vale path/to/document.{md,adoc}
```

To lint all the files in a folder, run the following command:

```console
vale path/to/folder/
```

The `vale` command prints any suggestions, warnings, or errors that it finds in the linted files.

[1]: https://gmartiblog.com
[2]: https://commonmark.org/help/
[3]: https://asciidoc.org/
[4]: https://jekyllrb.com/
[5]: https://vale.sh/
[6]: https://github.com/gmarti-web/gmarti-web.github.io/issues
[7]: https://github.com/gmarti-web/gmarti-web.github.io/issues/new?template=feature-request.yml
[8]: https://bundler.io/
[9]: https://jekyllrb.com/docs/installation/ubuntu/
[10]: http://brew.sh/
[11]: https://jekyllrb.com/docs/installation/macos/
[12]: https://www.ruby-lang.org/en/documentation/installation/
[13]: http://localhost:4000
[14]: https://rubyinstaller.org/
[15]: https://rubyinstaller.org/downloads/
[16]: https://jekyllrb.com/docs/installation/windows/
[17]: https://chocolatey.org/install
[18]: https://docs.chocolatey.org/en-us/choco/setup#non-administrative-install
[19]: https://learn.microsoft.com/en-us/powershell/scripting/windows-powershell/starting-windows-powershell?view=powershell-7.5#run-with-administrative-privileges
[20]: https://snapcraft.io/
[21]: https://vale.sh/docs/install
