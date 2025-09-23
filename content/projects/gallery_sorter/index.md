---
title: "Gallery Date Sorter"
summary: "GUI tool to organize photos and videos into YYYY‑MM folders by creation date."
tags: ["Python", "Utilities", "EXIF", "FFmpeg", "Tkinter"]
cover: "cover.png" 
thumbnail: "thumbnail.png" 
weight: 100
showToc: false
---

This project is a simple cross‑platform utility that sorts images and videos into date named folders based on their creation dates. With my ever growing photo library I needed a dead simple and free way to sort my photos from several sources. From that small pain I've created this project.

Great for cleaning up large, messy photo libraries!

# Implementation details

{{< button href="https://github.com/jofragotre/gallery-date-sorter" >}}Code on GitHub{{< /button >}}

## Features
- Automatically organizes images and videos by creation date into `YYYY‑MM` folders
- Choose to **copy** or **move** files
- Option to **skip existing files** in the destination
- Set a **custom output folder**
- **Progress bar** to track sorting
- Works on **Windows, macOS, Linux**

## Tech stack
- Python 3.8+
- GUI: **Tkinter**
- Images: **Pillow (PIL)**
- Video metadata: **FFmpeg**
- EXIF/metadata helpers in utilities

## Installation

Clone and install dependencies:
```bash
git clone https://github.com/jofragotre/gallery-date-sorter.git
cd gallery-date-sorter
pip install -r requirements.txt
```

Run the app:
```bash
python gui.py
```

## Usage (GUI)
1. Select the source folder with your images/videos
2. (Optional) Select a different output folder
3. Configure options:
   - Copy instead of move
   - Don’t move if file already exists
4. Click “Sort Files” and watch the progress bar

## Command‑line / programmatic use
The core sorting logic can be imported from the `utils` module for integration
into scripts or automations.

## Project structure
- `main.py` — GUI entrypoint (Tkinter)
- `utils/` — file operations, EXIF/date extraction, helpers
- `requirements.txt` — dependencies
- `LICENSE` — MIT License

## Roadmap / TODO
- HEIC support
  - Evaluate `exiftool` or `exifreader` for more robust metadata vs FFmpeg
- Distribute **standalone executables** (Windows/macOS/Linux)

## Acknowledgments
- [Pillow (PIL)](https://pillow.readthedocs.io/)
- [FFmpeg](https://ffmpeg.org/)
- [Tkinter](https://docs.python.org/3/library/tkinter.html)