## 0. What is this?

`tumblr_backup` is a Python script that backs up your
[Tumblr](http://www.tumblr.com) blog locally. The backup includes all
images from image posts. An index links to monthly pages, which contain
all the posts from the respective month, plus links to single post pages.
There are many options to select the posts to backup.

You can see an example of `tumblr_backup`’s output
[on my home page](http://drbeat.li/tumblr).


## 1. Installation

1. Download and unzip
   [xmltramp.zip](https://github.com/bbolli/xmltramp/zipball/master).
2. Install `xmltramp.py` somewhere on your Python path like
   `/usr/local/lib/python2.6/dist-packages`.
3. Download and unzip
   [tumblr_backup.zip](https://github.com/bbolli/tumblr_backup/zipball/bb).
4. Copy or symlink `tumblr_backup.py` to a directory on your `$PATH` like
   `~/bin` or `/usr/local/bin`.
5. Run `tumblr_backup.py` _blog-name_ as often as you like manually
   or from a cron job. The recommendation is to do a daily incremental backup
   and a weekly complete one to update the index.


## 2. Usage

### 2.1. Synopsis

    tumblr_backup.py [-qixtb] [-n post-count] [-s start-post] [-p y|m|d|YYYY[MM[DD]]] [blog-name] ...

### 2.2. Options

* `-q`: Suppress the progress display.
* `-i`: Incremental backup.
* `-x`: Include the original XML in the backup.
* `-t`: Include the theme in the backup.
* `-b`: Change the output format to [Blosxom](http://www.blosxom.com).
* `-n` _post-count_: Stop backing up after _post-count_ posts.
* `-s` _start-post_: Start backing up at the _start-post_’th post.
* `-p` _period_: Limit the backup to the given period.
  These are ways to define the period:
  * `y`: the current year
  * `m`: the current month
  * `d`: the current day (i.e. today ;-)
  * _yyyy_: the given year
  * _yyyy-mm_: the given month
  * _yyyy-mm-dd_: the given day

### 2.3. Arguments

* _blog-name_: The name of your blog.

If your blog is under `.tumblr.com`, you can give just the first domain name
part; if your blog is under your own domain, give the whole domain name.
You can give more than one _blog-name_ to backup multiple blogs in one go.

The default blog name can be changed in the script.


## 3. Operation

By default, `tumblr_backup` backs up all posts.

The generated directory structure looks like this:

    ./ - the current directory
        <blog-name>/ - your blog backup
            index.html - table of contents with links to the monthly pages
            archive/
                <yyyy-mm>.html - the monthly pages
                …
                current.html - the index of the latest -p or -i backup
            posts/
                <id>.html - the single post pages
                …
            images/
                <image.ext> - the image files
                …
            xml/
                <id>.xml - the original XML posts
                …
            theme/
                _local.css - the local style sheet
                theme.html - the saved HTML template
                custom.css - the CSS customizations
                avatar.<ext> - your avatar image

The name of the single post pages is the numeric post id.  The modification
time of the single post pages is set to the post’s timestamp. `tumblr_backup`
applies a simple style to the saved pages. All generated pages are
[HTML5](http://www.whatwg.org/specs/web-apps/current-work/multipage/).

Tumblr saves most image files without extension. This probably saves a few
million bytes in their database. `tumblr_backup` restores the image extensions.
If an image is already backed up, it is not downloaded again.

In incremental backup mode, `tumblr_backup` saves only posts that have higher
ids than the highest id saved locally. `archive/current.html` is overwritten.
Any other index or archive pages are left alone.

In XML backup mode, the original XML source returned by the Tumblr API is saved
under the `xml/` folder in addition to the HTML format.

In Blosxom format mode, the posts generated are saved in a format suitable for
re-publishing in [Blosxom](http://www.blosxom.com) with the [Meta
plugin](http://www.blosxom.com/plugins/meta/meta.htm). Images are not
downloaded; instead, the image links point back to the original image on
Tumblr. The posts are saved in the current folder with a `.txt` extension.
The index is not updated.

In order to limit the set of backed up posts, use the `-n` and `-s` options.
The most recent post is always number 0, so the option `-n 200` would select
the 200 most recent posts. Calling `tumblr_backup -n 100 -s 200` would skip
the 200 most recent posts and backup the next 100. The generated index will
just contain links to the posts selected.

With option `-p`, `archive/current.html` is overwritten.  Any other index or
archive pages are left alone.

If you combine `-n`, `-s`, `-i` and `-p`, only posts matching all criteria
will be backed up.

In order to successfully backup your blog theme with `-t`, you need to define
your Tumblr login information in the file `~/.netrc` with an entry like this:

`machine www.tumblr.com login` _login-email_ `password` _tumblr-password_

This file should have mode 0600 (read/write by owner only).

All operations except `-t` use only public Tumblr APIs, so you can use the
program to backup blogs that you don’t own.

`tumblr_backup` is developed and tested on Linux and OS X. If you want to
run it under Windows, I suggest the excellent [Cygwin](http://cygwin.com)
environment.


## 4. Changelog

See [here](https://github.com/bbolli/tumblr_backup/commits/bb). There are no
formal releases; so check back often!


## 5. Author

Beat Bolli `<me+tumblr_backup@drbeat.li>`,
[http://drbeat.li/py/tumblr_backup/](http://drbeat.li/py/tumblr_backup/)