## mkv internal subs to hls.js streaming , uses mpv, ffmpeg, hls.js  + python3

this works with any torrent to http server, such as https://github.com/omgbox/rsd

This Python code creates a web application that allows multiple users to simultaneously stream a single video source using HLS (HTTP Live Streaming). Here's a breakdown of what it does:

**1. Core Functionality:**

*   **Takes a Video URL:**  The user provides a URL (or magnet link) to a video.
*   **Processes the Video:** It uses `mpv` to decode the video and `ffmpeg` to convert it into an HLS stream (a series of small video chunks and a playlist file).
*   **Serves the Stream:** The application serves the HLS playlist (`.m3u8`) and video chunks (`.ts`) to clients.
*   **Multi-User Support:** Multiple users can connect and watch the same stream concurrently.
*   **Session Management:** Each stream is assigned a unique session ID for tracking and management.
*   **Automatic Cleanup:**  Inactive streams are automatically stopped and their files are deleted after a period of time.
*   **Dependency Check:** Checks if `ffmpeg` and `mpv` are installed.

**2. Key Components:**

*   **`aiohttp`:**  A Python library for building asynchronous web applications.  Handles incoming requests and serves the HLS stream.
*   **`ffmpeg` & `mpv`:** Command-line tools for video processing. `mpv` decodes the video, and `ffmpeg` converts it to the HLS format.
*   **HLS (HTTP Live Streaming):** A video streaming protocol that breaks the video into small chunks, making it suitable for streaming over the internet.
*   **Threading & Asynchronous Programming:**  Uses threads and `asyncio` to handle multiple streams concurrently without blocking.
*   **Logging:**  Provides detailed logging for debugging and monitoring.
*   **HTML/JavaScript Frontend:** A simple web page with a form to enter the video URL and a video player to display the stream.  Uses `hls.js` to play the HLS stream in the browser.

**3.  Important Features:**

*   **Session Timeout:** Streams are automatically stopped if no users are watching for a certain period.
*   **Maximum Concurrent Streams:** Limits the number of simultaneous streams to prevent server overload.
*   **Error Handling:** Includes error handling to gracefully handle issues like invalid URLs or missing dependencies.
*   **Reaper Task:** A background task that periodically cleans up inactive streams.
*   **Heartbeat:** Clients send periodic "heartbeat" signals to keep their streams alive.



## How to Run the Code:

Here's a step-by-step guide to get it running:

**1. Prerequisites:**

*   **Python 3.7 or higher:** Make sure you have Python installed.
*   **`ffmpeg`:**  Install `ffmpeg`.  On Debian/Ubuntu: `sudo apt-get install ffmpeg`
*   **`mpv`:** Install `mpv`. On Debian/Ubuntu: `sudo apt-get install mpv`
*   **`aiohttp`:** Install the required Python packages: `pip install aiohttp`

**2. Save the Code:**

*   Save the code provided in the `encoder.txt` file as a Python file (e.g., `streamer.py`).

**3. Run the Application:**

*   Open a terminal or command prompt.
*   Navigate to the directory where you saved `streamer.py`.
*   Run the application using: `python streamer.py`

**4. Access the Web Interface:**

*   Open a web browser and go to `http://localhost:8000` (or the port you specified if you changed it).

**5. Start Streaming:**

*   Paste the URL of the video you want to stream into the input field.
*   Click "Start Stream".
*   The application will process the video and start the HLS stream.  The video player should appear and start playing the stream.

**6. Multiple Users:**

*   Other users can access the same stream by going to `http://localhost:8000` in their web browsers.  They will all be watching the same video simultaneously.

**Important Notes:**

*   **RAM Disk (tmpfs):** For best performance, it's highly recommended to mount a RAM disk (tmpfs) to the `streams` directory. This will significantly speed up the streaming process.  The code includes a warning if it detects that `streams` is not a RAM disk and provides a command to create one.
*   **Firewall:**  Make sure your firewall allows access to the port you're using (default is 8000).
*   **URL Support:** The application supports direct URLs to video files and magnet links for torrents.
*   **Dependencies:** If `ffmpeg` or `mpv` are not found, the application will display an error message.  Install them before running the application.
*   **Port Conflicts:** If the default port (8000) is already in use, the application will prompt you to enter a different port.
*   **Error Messages:** Pay attention to the console output for any error messages.  They can help you troubleshoot problems.
*   **Resource Usage:** Streaming video can be resource-intensive.  Make sure your server has enough CPU and memory to handle the load.
*   **Security:** This is a basic streaming application and does not include advanced security features.  Do not use it to stream sensitive content.



This outline and the instructions should give you a good understanding of what the code does and how to get it up and running.  Let me know if you have any other questions.
