# quickfix

`quickfix` turns the text in your Zsh command line into an editable shell
command when you press Alt+O. It does not execute the result.

That is the whole tool.

## Install

Install the [Codex CLI](https://developers.openai.com/codex/cli), sign in with
your ChatGPT subscription, then run:

```sh
codex login
./install
exec zsh
```

Quickfix supports Arch Linux, Debian, and Ubuntu. It requires Bash, Zsh, and
Codex; quickfix itself adds no Python, Node.js, package manager, or
distro-specific package. The installer uses standard GNU userland tools present
on all three distributions.

Type `show the ten largest files here`, press Alt+O, inspect the generated
command, and press Enter only if it is what you wanted.

The installer puts two files on the system:

```text
~/.local/bin/quickfix
~/.config/quickfix/quickfix.zsh
```

It adds one managed source block to `${ZDOTDIR:-$HOME}/.zshrc`. Re-running the
installer updates the files without duplicating the block. It also removes the
old managed `cmdsmith` block.

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

Delete the two installed files and this block from your Zsh startup file:

```zsh
# quickfix begin
source /home/you/.config/quickfix/quickfix.zsh
# quickfix end
```

## Test

```sh
./tests/run
```

The test suite uses a fake `codex`; it does not spend tokens. Set
`QUICKFIX_LIVE_TEST=1` to include one real generation using your current Codex
login.

MIT licensed.
