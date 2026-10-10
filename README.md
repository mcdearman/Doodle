# Doodle

Drawing in a terminal, a cell at a time, for
[Meadow](https://github.com/meadow-lang/meadow).

A buffer is a grid of cells, each a character and how it is styled.
Everything that draws takes a buffer and answers one, so what is drawn is a
value: it can be compared in a test, and turned into the text that shows it
only when there is a terminal to write that to. Nothing here reads a key or
writes to a terminal.

```meadow
use Doodle

fun picker (names : [String]) (chosen : Int) : Buffer =
  let b = blank 40 8 in
  let b = border b (area b) style "find" in
  list b (inside (area b)) (V.map (\n -> (n, style)) names) chosen (bold style)

-- under the line the cursor is on, the cursor left where it was
writeOutput (below (picker ["length", "lines", "last"] 1))
```

- **Where**: `rect x y w h`; `inside` is what a border leaves; `columns` and
  `rows` divide a rectangle among sizes: `Cells n`, `Percent p`, `Share`.
- **Drawing**: `write`, `writeIn` a rectangle, `writeSpans` of several
  styles, `fill`, `border` with a title, `paragraph` wrapped between words,
  `list` with one item chosen and kept in view.
- **Showing**: `shown` is the whole buffer; `below` puts it in the lines
  under the cursor's; `changed` is only the cells that differ from the buffer
  before; `plain` is the text alone, for tests.
- **The terminal's own words**: `moveTo`, `up`, `down`, `toColumn`,
  `clearLine`, `clearDown`, `hideCursor`, `showCursor`, `enterScreen`,
  `leaveScreen`.

A character is as wide as a terminal shows it: one cell, two, or none for a
mark that goes on the character before. Widths are
[UnicodeWidth](https://github.com/meadow-lang/UnicodeWidth)'s and styles
are [Anstyle](https://github.com/meadow-lang/Bloom)'s; the ones a caller
starts from -- `style`, `bold`, `dimmed`, `withFg`, the colours -- are handed
on from here, so drawing needs only this package.

## AI disclosure

Doodle is written with AI coding agents: Anthropic's Claude, through Claude
Code. Most of the code, the tests, the documentation and the commit messages in
this repository were written by an agent, under the direction of the project's
author, who decides the design and what goes in. Read it, and rely on it, with
that in mind.

## Install

```sh
meadow add meadow-lang/Doodle
```

## Licence

BSD 3-Clause: see [LICENSE](LICENSE).
