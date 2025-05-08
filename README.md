# YoutubeVideoBookmark

A lightweight Chrome extension that helps you save and manage important moments in YouTube videos.

## Overview

YoutubeBookmark allows you to easily bookmark timestamps while watching YouTube videos. Whether you're following a tutorial, studying educational content, or simply want to remember your favorite moments, this extension provides a seamless way to mark and return to specific points in any video.

## Key Features

- **One-Click Bookmarking**: Save any video moment instantly
- **Easy Bookmark Management**: View or delete bookmarks in a dedicated popup
- **YouTube Integration**: Appears directly in the video player interface
- **Cross-Device Sync**: Uses chrome.storage.sync for automatic backup and access across all your devices

## Installation Guide

### Manual Setup

1. **Clone the Repository**:
   ```
   git clone https://github.com/Kun-Alexandru/ytb-bookmark.git
   ```

2. **Open Chrome Extensions Settings**:
   - Navigate to `chrome://extensions/`

3. **Enable Developer Mode**:
   - Toggle it on in the top-right corner

4. **Load the Unpacked Extension**:
   - Click "Load unpacked" and select the project folder

## How to Use

1. Open any video on YouTube
2. A bookmark button will appear on the video interface
3. Click it to save the current timestamp
4. Open the extension popup to view, jump to, or delete bookmarks

## Important files

### contentScript.js
- Injected into YouTube pages
- Adds a bookmark button to the video player
- Extracts video ID and current time
- Sends data to storage via messaging

### popup.js
- Reads current video bookmarks
- Displays and manages saved entries

### background.js
- Handles communication between the popup and content script
- Interfaces with chrome.storage.sync

## Manifest Configuration

```json
{
  "manifest_version": 3,
  "name": "YoutubeBookmark",
  "version": "1.0",
  "permissions": ["storage", "scripting", "activeTab"],
  "background": {
    "service_worker": "background.js"
  },
  "content_scripts": [
    {
      "matches": ["*://www.youtube.com/*"],
      "js": ["contentScript.js"]
    }
  ],
  "action": {
    "default_popup": "popup.html"
  }
}
```

## Bookmark Storage Format

```json
{
  "ID": [
    {
      "time": 300,
      "desc": "something descriptive"
    }
  ]
}
```

## Technologies Used

- JavaScript, HTML and CSS
- Chrome Extensions API – Manifest V3
- chrome.storage.sync to save and sync the data
