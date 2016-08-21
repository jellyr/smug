# SMUG

The **S**heet **Mu**sic **G**enerator.

## Prerequisites

You will need [Leiningen][] 2.0.0 or above installed.

[leiningen]: https://github.com/technomancy/leiningen

## Running

To start a web server for the application, run:

```sh
lein run
# or with explicit overrides:
PORT=5000 OUTPUT_DIR=/tmp/my-scores lein run
```

### Lilypond Rendering

If you want to generate and render a score using Lilypond, run:

```clojure
user> (require '[smug.music :refer :all])
user> (require '[smug.render.lilypond :refer :all])
user> (-> (generate-score 64)
          (render-svg-to "/tmp/foo"))
; returns:
; #object[java.io.File 0x5c2bc22c "/tmp/foo.svg"]
```

This requires the `lilypond` executable to be on your `PATH`, and the given
path to be writable. Note that the path `/tmp/foo` results in `/tmp/foo.svg`,
or possibly paged paths (`/tmp/foo-page-1.svg`, `/tmp/foo-page-2.svg`, ...)
when the score doesn't fit in a single page.

You can also get the intermediate Lilypond markup by using `render-as-lilypond`:

```clojure
user> (-> (generate-score 64)
          render-as-lilypond)
; returns the markup as a string:
"\n\\header {\n  title = \"Sight Reading Exercise\"\n  tagline = \"Generated by SMUG\"\n}\n{\n  c'2 d'2 \\\n  c'2 d'2 \\bar \"|\" c'2 e'2 \\bar \"|\" d'2 c'2 \\bar \"|\" c'2 d'2 \\bar \"|\" c'2 d'2 ..."
```

### Abc4j Rendering

If you want to generate and render a score using abc4j and Swing, run:

```clojure
user> (require '[smug.music :refer :all])
user> (require '[smug.render.abc4j :refer :all])
user> (-> (generate-score 64)
          create-score-component
          render-in-window)
; a Java Swing window should appear
```

## License

Mozilla Public License, v. 2.0. See the [full LICENSE file](LICENSE).

Copyright © 2016 Oskar Wickström.
