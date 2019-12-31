# <img src="media/banner-transparent-small.png" height=150 alt="HNTerm : Hacker News in terminal" />

[![HNTerm v0.1 badge][changelog-badge]][changelog] [![Version 0.1 Badge][version-badge]][changelog] [![MIT License Badge][license-badge]][license]

Browse [Hacker News](https://news.ycombinator.com/news) interactively in your terminal

<a href="https://i.imgur.com/As9GT07.png" target="_blank">![hnterm-dark](https://i.imgur.com/As9GT07.png)</a>

[![hnterm-demo](https://asciinema.org/a/gJakwNnEcgmGzZYiYIzFA1n8R.svg)](https://asciinema.org/a/gJakwNnEcgmGzZYiYIzFA1n8R)

## Details

HNTerm is a small console application written in C++ for browsing [Hacker News](https://news.ycombinator.com/news). It queries the official [HN API](https://github.com/HackerNews/API) and interactively displays the current stories and comments. It uses `libcurl` to perform the GET requests to the API. The UI is rendered with [ImTui](https://github.com/ggerganov/imtui). HNTerm fetches only the content that is currently visible on the screen. The window splits allow browsing multiple stories/comment sections at the same time.

## Installing

[![Get it from the Snap Store](https://snapcraft.io/static/images/badges/en/snap-store-black.svg)](https://snapcraft.io/hnterm)

### Ubuntu

`sudo snap install hnterm --edge`

## Building from source

### Linux and Mac:

```bash
git clone https://github.com/ggerganov/hnterm --recursive
cd hnterm
mkdir build && cd build
cmake ..
make

./bin/hnterm
```

## Live demo in the browser

The Emscripten port of HNTerm uses Emscripten's Fetch API instead of `libcurl` to perform requests to the [HN API](https://github.com/HackerNews/API). 

Demo: [hnterm.ggerganov.com](https://hnterm.ggerganov.com/) *(not suitable for mobile devices)*

[changelog]: ./CHANGELOG.md
[changelog-badge]: https://img.shields.io/badge/changelog-HNTerm%20v0.1-dummy
[license]: ./LICENSE
[version-badge]: https://img.shields.io/badge/version-0.1-blue.svg
[license-badge]: https://img.shields.io/badge/license-MIT-blue.svg
