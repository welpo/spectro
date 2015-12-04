# About
`spectro` is a bash script which provides BBCode formatted text with the spectrograms of audio files (Ogg, MP3, FLAC, AAC, ape, WMA, MP4 or WAV).

To process an entire directory: `spectro Path/To/Directory/`

Or to process specific files: `spectro <file1> <file2> ...`

The output will look like:
```
[hide=Spectrograms][size=3]
[url=https://i.imgur.com/ClzzbP8.png]01. Jardin Du Sommeil.flac[/url]

[url=https://i.imgur.com/YPFZA1A.png]02. Chant D'Amour.flac[/url]

[url=https://i.imgur.com/sqdQfMd.png]03. Sur La Nuit Grandissante.flac[/url]
[/size][/hide]
```

# Install
* Place `spectro` somewhere in your PATH, like `~/bin`
* Make it executable: `chmod +x spectro`

**Optional**:

* Set up the first lines of the script (where the configuration is stored) to your liking.

# Dependencies
To run `spectro` you will need:

- `sox` which creates the spectrograms (with MP3 support if you want to use `spectro` with such files): http://sox.sourceforge.net
- `curl` to upload the images to imgur (not necessary if only used locally).

**Optional dependencies**:

- `ffmpeg` or `avconv` to process ape, WMA, MP4 and AAC files.
- `optipng` to optimise the spectrograms. Necessary more often than not to avoid imgur transcoding the images to `.jpg`: http://optipng.sourceforge.net
- `shasum` to include the file SHA on the output BBCode output as well as `sox`'s spectrogram title.

# Configuration
You can configure the following options for `spectro` by modifying the first lines on the script using your favourite text editor:

* `apikey` Imgur API key. Default value is the `spectro` public API key. You can change it to use your own (if it ever hits the limits, for example) - you can read about it and register one here: https://api.imgur.com/oauth2.
* `check_sha` Adds the SHA of the file to the BBCode output as well as the title in the `sox` spectrogram (Default is 0).
* `localdir` Local directory where files will be stored (e.g. your public_html folder).
* `offline` Create local spectrograms (saved in `localdir`), don't upload to imgur (Default is 0).
* `optipng` Use optipng on the spectrogram images to save space and avoid imgur compressing them to jpg (Default is 1).
* `text_only` Output [url][/url] tags with the filename as the clickable link to the spectrogram (Default is 1). The alternative is to output [img][/img] tags to embed the images.
* `urlformat` URL that directs to the directory set in `localdir`.

# Options
```
-d, --double           Take both zoomed in and full spectrogram for each file
-h, --help             Show the help output
-l, --local            Reverse the setting to output the spectrograms locally
-o, --optipng          Reverse the optipng option set in the script
-p, --parallel         Play nicely with parallel (won't ouput the [hide] or [size] tags)
-q, --quiet            Don't show 'Uploading' text (necessary if you want to pipe)
-s, --sha              Reverse the check_sha option (to show SHA value)
-t, --text             Reverse the setting to use [url] tags or [img]
-z, --zoom             Create only zoomed in screenshot (3 seconds)
```
