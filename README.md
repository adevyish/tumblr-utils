# tumblr-utils

This is a collection of utilities dealing with Tumblr blogs, forked from [bbolli's tumblr-utils](https://github.com/bbolli/tumblr-utils/).

- `tumble.py` creates new posts from RSS or Atom feeds
- `tumblr_backup.py` makes a local backup of posts and images
- `mail_export.py` mails tagged links to a recipient list

## Instructions

- [Tumblr backup](blob/master/_tumblr_backup.md)
- [Tumblr backup 101 (Windows)](blob/master/_tumblr_backup_101_windows.md)
- [Tumblr backup 101 (Mac)](blob/master/_tumblr_backup_101_mac.md)

## Requirements

The utilities run under Python 2.7.

For `tumblr_backup.py`, you'll need `youtube-dl` for audio/video archival, and `unicode-slugify` to generate tag pages.

## License

[GPL3](http://www.gnu.org/licenses/gpl-3.0.txt).
