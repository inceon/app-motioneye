# Changelog

## 0.45.0-optimized.4

- Merge upstream app updates through dc6bb99.
- Update the Home Assistant base image to 21.0.10.
- Update Python to 3.14.10-r1, FFmpeg to 8.1.3-r0, curl-dev to 8.23.0-r0,
  and rsync to 3.5.2-r1.
- Preserve the optimized motionEye source and Telegram video notifications.

## 0.45.0-optimized.3

- Add an optional Send Videos switch to Telegram camera notifications.
- Send each completed recording to Telegram: MP4 as video, other formats as files.
- Reject recordings larger than Telegram's 50 MB upload limit with a clear log message.
- Add Ukrainian and English translations for the video notification setting.

## 0.45.0-optimized.2

- Schedule camera snapshots at the configured FPS and pause requests in hidden tabs.
- Preserve slow-request retries and native MJPEG streaming.
- Fix displayed FPS and update camera aspect ratios when frames load.
- Improve mobile settings, login, camera setup, and recording browser layouts.
- Add touch slider dragging and larger touch targets.
- Keep dialogs within the visible viewport, including when a keyboard is open.
- Invalidate changed frontend assets by content hash.

## 0.45.0-optimized.1

- Introduce the optimized fork with movie-player cleanup, nonblocking previews,
  bounded thumbnail generation, and background MP4 faststart.
