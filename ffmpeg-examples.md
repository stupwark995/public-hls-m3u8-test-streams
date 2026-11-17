# FFmpeg M3U8 (HLS) to MP4 Cheatsheet

Quick, reliable local FFmpeg commands for converting authorized M3U8 / HLS playlists into MP4 or audio files.

> Interactive command builder: **[M3U8 to MP4 FFmpeg Command Generator](https://m3u8play.net/m3u8_to_mp4/)**

## 1. Fastest Lossless Stream Copy (H.264 + AAC)
```bash
ffmpeg -i "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8" \
  -c copy -bsf:a aac_adtstoasc output.mp4
```

## 2. Universal Re-encode (Fix Audio / QuickTime / Mobile Compatibility)
```bash
ffmpeg -i "https://example.com/hls/master.m3u8" \
  -c:v libx264 -preset medium -crf 20 \
  -c:a aac -b:a 128k -movflags +faststart output.mp4
```

## 3. Pass Custom Referer, User-Agent, and Cookies (Fix 403 Forbidden)
```bash
ffmpeg -user_agent "Mozilla/5.0" \
  -headers "Referer: https://your-site.example.com/\r\nCookie: session=your_token\r\n" \
  -i "https://your-cdn.example.com/hls/index.m3u8" \
  -c copy -bsf:a aac_adtstoasc output.mp4
```

## 4. Record Live HLS Stream for Fixed Duration (30 Minutes)
```bash
ffmpeg -i "https://cph-p2p-msl.akamaized.net/hls/live/2000341/test/master.m3u8" \
  -t 00:30:00 -c copy live-clip.mp4
```

## 5. Extract Audio Only (MP3)
```bash
ffmpeg -i "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8" \
  -vn -c:a libmp3lame -q:a 2 audio.mp3
```

Need to verify your stream plays cleanly in a browser first? Test it on **[m3u8play.net](https://m3u8play.net/)**.
