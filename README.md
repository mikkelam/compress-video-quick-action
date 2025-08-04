# Compress Video Quick Action

A macOS Quick Action that adds right-click video compression to Finder. Compresses videos using ffmpeg while preserving the original file (adds `_compressed` suffix).

![Quick Action Demo](https://github.com/mikkelam/compress-video-quick-action/assets/4174131/9ae2cb29-5094-4483-949d-96ba6297e515)

## Features

- Right-click any video file in Finder to compress
- Preserves original file (creates new `_compressed` version)
- Uses ffmpeg with default settings for fast compression
- Supports all common video formats (MP4, MOV, AVI, MKV, etc.)

## Prerequisites

- macOS with Automator (built-in)
- ffmpeg installed and available at `/opt/homebrew/bin/ffmpeg`

### Install ffmpeg via Homebrew

1. Install [Homebrew](https://brew.sh) if you don't have it
2. Install ffmpeg: `brew install ffmpeg`

## Installation

1. **Download the workflow**
   - Download or clone this repository
   - Locate `compress_video.workflow`

2. **Install the Quick Action**
   - Double-click `compress_video.workflow`
   - Click "Install" when prompted
   - The workflow will be added to `~/Library/Services/`

3. **Verify installation**
   - Right-click any video file in Finder
   - Look for "compress_video" in the context menu


## Customization

The workflow uses these default ffmpeg settings:
- Codec: H.264 (libx264)
- Preset: fast (good balance of speed/quality)
- Output format: MP4

### Modify Compression Settings

1. Open Automator
2. File → Open → Navigate to `~/Library/Services/compress_video.workflow`
3. Modify the shell script command:

```bash
# Current command
/opt/homebrew/bin/ffmpeg -i "$f" -c:v libx264 -preset fast "${f%.*}_compressed.${f##*.}"

# Higher quality (slower)
/opt/homebrew/bin/ffmpeg -i "$f" -c:v libx264 -preset slow -crf 20 "${f%.*}_compressed.${f##*.}"

# Smaller file size (lower quality)
/opt/homebrew/bin/ffmpeg -i "$f" -c:v libx264 -preset fast -crf 28 "${f%.*}_compressed.${f##*.}"

```

### Change ffmpeg Path

If ffmpeg is installed elsewhere, update the path in the workflow:

```bash
# Common alternative paths
/usr/local/bin/ffmpeg          # Intel Mac Homebrew
/opt/homebrew/bin/ffmpeg       # Apple Silicon Homebrew (default)
/usr/bin/ffmpeg                # System installation
```


## License

MIT License - feel free to modify and distribute

## Contributing

Found a bug or have a feature request? Open an issue or submit a pull request.
