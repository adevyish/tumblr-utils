# Tumblr Backup 101 (Mac)

## 1. Setup Python

If you’re on Mac, you're already set.

If you want to download audio or video, also do this:

1. Install PIP: [follow these instructions](https://pip.pypa.io/en/stable/installing/)
2. Run

		sudo pip install --upgrade youtube_dl

## 2. Download tumblr-utils

1. Go to this page: https://github.com/adevyish/tumblr-utils
2. Click the green button at right that says **Clone or download** then click **Download ZIP**
3. Unzip it

## 3. Run tumblr-utils

1. Open a terminal window and go to your unzipped folder.

	1. Command-Space, type `Terminal`, hit enter. A new window should open.
	2. Type `cd ` (note the space) then drag the folder you unzipped into the window. It should automatically give you something like

		```> cd your/folder/here```

	3. Hit enter

2. Type:

		python tumblr_backup.py blogname

	where ***blogname*** is the person's username, for example ***blogname**.tumblr.com*

3. It'll show a progress bar. Wait. Make some lunch.
4. Posts will be saved to a folder named ***blogname*** inside your unzipped folder.

	There are some options available if you want to save/not save certain things. For example:

	* Generate tag pages:

			python tumblr_backup.py --tag-index blogname

	* Save audio and video from posts:

			python tumblr_backup.py --save-video --save-audio blogname
		
		As mentioned above, you'll need to have the python module for youtube-dl installed.

	* Don't save images from posts:

			python tumblr_backup.py --skip-images blogname

	* Don't save reblogged posts:

			python tumblr_backup.py --no-reblog blogname

	* Save only posts tagged with certain tags:

			python tumblr_backup.py --tags=tag1,tag2 blogname

	You can combine the above options.

	You can also save only likes:

		python tumblr_backup.py --likes blogname

### BONUS: Re-archive an already saved blog

Assuming you haven't moved where you saved the posts originally, you can only save new posts by running:

	python tumblr_backup.py --incremental blogname

(Don't forget to include any custom flags you used above to save audio, generate tag pages, and such!)

If you moved the archive folder, do this instead:

	python tumblr_backup.py --incremental blogname --outdir=path/to/folder

* Again, if you're on Mac, just type the whole thing up to `outdir=` (no space at the end!) and drag your folder into Terminal.

## Caveats

* The HTML output by this is currently W3C non-compliant.
* This won't save custom styles, and if you have a custom style it will not work with it.
* This won't save custom pages. You'll have to save those yourself one by one. Using your browser's **Save As** function with format set to **Web Archive** (or similar) is good enough.
