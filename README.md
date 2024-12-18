# Fresh (Fork from: [gravityblast/fresh](https://github.com/gravityblast/fresh))

Fresh is a command line tool that builds and (re)starts your web application everytime you save a Go or template file.

If the web framework you are using supports the Fresh runner, it will show build errors on your browser.

## Fork changes
- Update [fsnotify](https://github.com/fsnotify/fsnotify) to latest version.
- Move `runner` and `miniassert` into project.
- Support passing arguments to the application(by adding `run_args` in `runner.conf`).
- Fix `config` package fail to read last line with EOF.

## Installation

    go install github.com/xxoommd/fresh@latest

## Usage
    cd /path/to/myapp

Start fresh(make sure GOBIN is in your PATH):

    fresh

Fresh will watch for file events, and every time you create/modify/delete a file it will build and restart the application.
If `go build` returns an error, it will log it in the tmp folder.

[Traffic](https://github.com/pilu/traffic) already has a middleware that shows the content of that file if it is present. This middleware is automatically added if you run a Traffic web app in dev mode with Fresh.
Check the `_examples` folder if you want to use it with Martini or Gocraft Web.

`fresh` uses `./runner.conf` for configuration by default, but you may specify an alternative config filepath using `-c`:

    fresh -c other_runner.conf

Here is a sample config file with the default settings:

    root:              .
    tmp_path:          ./tmp
    build_name:        runner-build
    build_log:         runner-build-errors.log
    valid_ext:         .go, .tpl, .tmpl, .html
    no_rebuild_ext:    .tpl, .tmpl, .html
    ignored:           assets, tmp
    build_delay:       600
    colors:            1
    log_color_main:    cyan
    log_color_build:   yellow
    log_color_runner:  green
    log_color_watcher: magenta
    log_color_app:
    run_args: