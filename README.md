# quickfix

`quickfix` turns the text in your Bash command line into an editable shell
command when you press Alt+O. It does not execute the result.

That is the whole tool.

## Install

Install the [Codex CLI](https://developers.openai.com/codex/cli), sign in with
your ChatGPT subscription, then run:

```sh
codex login
./install
exec bash
```

The default installation targets Bash. For Zsh instead:

```sh
./install zsh
exec zsh
```

Quickfix supports Arch Linux, Debian, and Ubuntu. It requires Bash and Codex;
Zsh is optional. Quickfix itself adds no Python, Node.js, package manager, or
distro-specific package. The installer uses standard GNU userland tools present
on all three distributions.

Type `show the ten largest files here`, press Alt+O, inspect the generated
command, and press Enter only if it is what you wanted. While Codex works,
Quickfix leaves your request in place and animates a throbber on the next line.
If generation fails, your original line stays untouched.

The default installer writes:

```text
~/.local/bin/quickfix
~/.config/quickfix/quickfix.bash
```

It adds one managed source block to `~/.bashrc`. Re-running the installer
updates the files without duplicating the block. The optional Zsh installation
writes `quickfix.zsh` and updates `${ZDOTDIR:-$HOME}/.zshrc` instead.

## Defaults

`quickfix` uses the saved Codex login, `gpt-5.6-luna`, and low reasoning. The
only knobs are environment variables:

```sh
export QUICKFIX_MODEL=gpt-5.6-terra
export QUICKFIX_REASONING=medium
```

There is no config file, API client, model registry, chat mode, JSON mode,
clipboard mode, cache, database, package manager, or runtime dependency beyond
Bash and Codex.

## Remove

Delete `~/.local/bin/quickfix`, the installed widget, and the managed quickfix
block from `.bashrc` or `.zshrc`.

## Test

```sh
./tests/run
```

The test suite uses a fake `codex`; it does not spend tokens. It checks the
default Bash path and optional Zsh path. Set `QUICKFIX_LIVE_TEST=1` to include
one real generation using your current Codex login.

MIT licensed.
