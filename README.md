# bookmarks

bookmarks is a concept of keeping bookmarks in plain text files.

## Principals

- Bookmarked URLs are stored in files named `bookmarks.txt`. The format is described below.
- A "global" bookmarks file is located in the home directory (`$HOME/bookmarks.txt`).
- "Local" bookmarks files could exist in different directories as well.

## Format

URLs are stored one per line and could be accompanied with optional titles. Titles are separated from URLs with one space character.

```
URL [title]
```

Examples:

- a URL without any title

  ```
  https://www.example.com
  -----------------------
  ^
  URL
  ```
- a URL with a title
  ```
  https://sul.im personal website
  -------------- ----------------
  ^              ^
  URL            Optional title
  ```

## Tools

The plain text nature of bookmark files allows to use any program to manage URLs. The `bin/` directory of this repository contains `bookmarks` script that could be used to list existing and add new URLs. However nothing should stop you from building your own tools.

## Setup

Currently, this fork is setup to be used on WSL with your default brower. Follow these steps to correctly install this tool:

1. Clone this repo into your ~ folder
2. Add these aliases to your .bashrc file:
   ```
   alias add='~/bookmarks/bin/bookmarks'
   alias bm='cd ~/bookmarks && ./bin/bookmarks | fzf | cut -d " " -f 1 | xargs -r wslview'
   ```
3. Install wslu using sudo apt install
4. Install fzf sudo apt install
5. Test that it works by typing `bm`. You should see two example urls
6. To add a url you can type:
```
add https://example.com "Example site"
```

## Usage

Use [fzf] to select a URL and open it in the default browser:

```ShellSession
./bin/bookmarks | fzf | cut -d ' ' -f 1 | xargs open
```

Add a new URL:

```ShellSession
./bin/bookmarks https://github.com/soulim/bookmarks.txt
```

This is how I use bookmarks.txt:

- `$HOME/bookmarks.txt` contains URLs useful in any context. These are "global" addresses.
- Each project directory has "local" `bookmarks.txt` files with URLs pointing to tools specific to each project (repositories, monitoring tools, dashboards, and so on).
- A symbolic link `$HOME/bin/bookmarks` point to `bin/bookmarks` from this directory.
- With help of [fzf] I have a nice menu with fuzzy search to select URLs and open them automatically.

## Contributing

bookmarks.txt is open to code contributions for bug fixes only. As features might carry a long-term maintenance burden, they will not be accepted at this time. Please submit an issue if you have a feature you would like to request.

## License

See [LICENSE](LICENSE) for license text.


[fzf]: https://github.com/junegunn/fzf
