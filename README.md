# homebrew-clocwork

A [Homebrew](https://brew.sh) tap for
[clocwork](https://github.com/wojciechpolak/clocwork), which counts lines of
code across a list of projects with [cloc](https://github.com/AlDanial/cloc)
and renders one combined report as text, Markdown, HTML and SVG.

## Install

```sh
brew install wojciechpolak/clocwork/clocwork
```

That taps this repository and installs the command. `cloc` comes with it, since
clocwork runs cloc once per project and does nothing without it.

## Upgrade and uninstall

```sh
brew upgrade wojciechpolak/clocwork/clocwork
brew uninstall wojciechpolak/clocwork/clocwork
brew untap wojciechpolak/clocwork
```

## What gets installed

clocwork is a Python program with no third-party runtime dependencies, and the
formula keeps it that way. It downloads the `py3-none-any` wheel from the
matching GitHub release, checks its SHA-256, and puts it in a virtualenv of its
own under the Homebrew prefix, with `clocwork` linked into `bin`. Nothing is
built and nothing is fetched from PyPI. The same wheel carries GitHub build
provenance on the release it came from.

Two other formulae come along. `cloc` counts the lines. `git` is what clocwork
clones and fetches a remote project with, and what it asks for the file list of
a local one when `vcs = "git"`.

## Pointing it at your projects

clocwork counts the projects listed in a `projects.toml`. An installed copy has
none of its own, so give it yours:

```sh
clocwork --config ~/code/projects.toml --out ~/code/report
```

Recent versions look for `projects.toml` in the directory you run them from and
write `out/` beside it, which makes both flags optional. The
[clocwork README](https://github.com/wojciechpolak/clocwork) documents the file
and every other flag.

Questions about counting, configuration or the reports belong in the
[clocwork issue tracker](https://github.com/wojciechpolak/clocwork/issues).
Only packaging problems belong here.

## About `Formula/clocwork.rb`

The formula is generated. Publishing a stable clocwork release renders it from
that release's version and the checksum of its wheel, installs it on macOS and
Linux, and pushes the result here, so an edit made directly to this repository
is gone at the next release. The renderer is
[`scripts/render-homebrew-formula`](https://github.com/wojciechpolak/clocwork/blob/main/scripts/render-homebrew-formula)
in the main repository. Change it there.

CI here audits the formula and installs it on both platforms on every push,
then makes the installed command count a file and checks the version it reports
against the version the formula claims.

## License

GPL-3.0-or-later, matching clocwork itself. See [LICENSE](LICENSE).

The reports clocwork writes are not covered by that licence. Its `LICENSE`
opens with an additional permission under section 7 of the GPL, so a generated
card or table can be embedded under any terms.
