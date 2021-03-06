---
title: Using TinyTeX from a Flash Drive
subtitle: Bye, IT! I no longer need you to install LaTeX for me.
date: '2018-08-31'
slug: tinytex-flash-drive
---

One nice fact about [TinyTeX](/tinytex/), the custom LaTeX distribution I created last year, is that once you install it, it is just a self-contained folder that can be moved elsewhere, even across computers of the same operating system. That is what "portable" means.

Yesterday I pushed a new version (v0.8) of the R package **tinytex** [to CRAN](https://cran.rstudio.com/package=tinytex) mainly to address the issue of using TinyTeX from a portable device such as a flash drive. I added two new functions in this version:

1. `tinytex::copy_tinytex()` copies your existing TinyTeX installation to another location, such as your flash drive or a Dropbox folder (this could take a minute or two depending on the I/O speed of your devices). Of course, this means you have installed TinyTeX before (e.g., via `tinytex::install_tinytex()`). By default, it will pop up a dialog box asking you to choose the destination folder to copy to, if you don't want to explicitly provide a path like:

    ```r
    tinytex::copy_tinytex('E:/Software/')
    ```

1. `tinytex::use_tinytex()` asks you the location of TinyTeX, so that **tinytex** can find it later when compiling LaTeX documents. By default, it also pops up a dialog asking you to choose the TinyTeX folder, which can be on your flash drive.

    Under the hood, it runs the command `tlmgr path add` to add TinyTeX to the environment variable `PATH` of your system (or create symlinks of TinyTeX's executables that can be found via `PATH`). If this fails, you still have the fallback plan. That is, set the global option `tinytex.tlmgr.path` and point it to the executable `tlmgr` in your system, e.g.,

    ```r
    # Windows
    options(tinytex.tlmgr.path = 'E:/Software/TinyTeX/bin/win32/tlmgr.bat')
    
    # macOS
    options(tinytex.tlmgr.path = '~/Dropbox/TinyTeX/bin/x86_64-darwin/tlmgr')
    ```

    You can do this in your `~/.Rprofile` or a code chunk of an R Markdown document that generates PDF output.

One folder to rule them all. No dependency hell. No waste of disk space. No IT support. Just help yourself.

![Help yourself](https://slides.yihui.name/gif/car-transform.gif)
