# BLOODMONEY - Web Port

This is an **Unofficial Web Port** of the free RPG Maker MV horror game [**BLOODONEY by SHROOMYCRIST**](https://shroomychrist-studios.itch.io/bloodmoney). This port allows the game to be played directly in a web browser without needing any downloads/installations.

## How to play

*Note: Fullscreen is recommended!*

There's 2 methods:

### Github Pages
Go to https://nick088official.github.io/BLOODMONEY-Web-Port/www/

### Local Server
1. Click Code -> Download ZIP -> Extract the Zip.
2. [Get Python](https://www.python.org/downloads/) installed and added to your system's PATH.
3. Open a CMD/Terminal **inside the root project folder** (the one that contains the `www` folder).
4.  Run the following command to start a simple web server:
    ```bash
    python -m http.server
    ```
5.  Open your web browser and go to the following address:
    **http://localhost:8000/www/**


## How did you make it?

This guide provides step-by-step instructions for modifying the game to run correctly in a web browser.

### Prerequisites

1. **Get the Game Files:** [Download the original game from the creator's itch.io page](https://shroomychrist-studios.itch.io/bloodmoney) and extract the files.
2. **Python (for running):** Having [Python](https://www.python.org/downloads/) installed and added to your system's PATH, to run the local game server.
3. **FFmpeg (Optional, for mobile audio):** For the mobile audio fix, you will need [FFmpeg](https://ffmpeg.org/download.html) installed and added to your system's PATH.


### Part A: Remove Unused Files

Delete everything else except the `www` folder in the game files.

Inside the `www` folder, you can delete the `package.json`.

### Part B: Mobile Audio Compatibility Fixes (Optional)

On mobile, the game tries to load `.m4a` audio files, but the project only contains `.ogg` files, causing a crash. So you have to create the `.m4a` audio files for maximum compatibility.

1.  Ensure you have **FFmpeg installed and added to your system's PATH**.
2.  Open a CMD/Terminal in your **root game folder** (the one containing the `www` folder).
3.  Paste and run the following one-liner command. It will find every `.ogg` file and create an `.m4a` copy next to it:
- For Windows:
    ```cmd
    for /R "www\audio" %F in (*.ogg) do ffmpeg -i "%F" -v quiet -stats "%~dpnF.m4a"
    ```
- For macOS & Linux:
    ```bash
    find www/audio -type f -name "*.ogg" -exec sh -c 'ffmpeg -i "$0" -v quiet -stats "${0%.ogg}.m4a"' {} \;
    ```

### Part C: Fix Game Scaling on Mobile (Optional)

You need to modify a to your `index.html` file to ensure proper game scaling on mobile.

1.  Open `www/index.html` in your text editor.
2.  Before the `</head>` tag, Replace the previous `<meta name="viewport"...` with:
    ```html
    <!-- This tag ensures the game scales correctly on mobile devices -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    ```

### Part D: Running the Game Locally

Once you have made the modifications, you need to run them using a local web server. Simply opening the `index.html` file directly will not work due to browser security restrictions.

1.  Open a CMD/Terminal **inside the root project folder** (the one that contains the `www` folder).
2.  Run the following command to start a simple web server:
    ```bash
    python -m http.server
    ```
3.  Open your web browser and go to the following address:
    **http://localhost:8000/www/**

The game should now start and be fully playable.


## Why did you make it?

For pure educational purposes, fun, and to make this game accessible on more platforms.


## Credits
- **Game:** All credit for the game's creation goes to **SHROOMYCRIST**. Please support the original creator by visiting the [official itch.io page](https://shroomychrist-studios.itch.io/bloodmoney).
- **Web Port:** This web-based version was ported by [Nick088](https://linktr.ee/nick088).
- **Game Engine:** RPG Maker MV.