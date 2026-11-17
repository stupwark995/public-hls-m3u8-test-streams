# Public HLS / M3U8 Test Streams (VOD & Live)

A clean, maintained list of official, legally hosted public `.m3u8` HLS test streams for testing `hls.js`, Safari native HLS, ExoPlayer, AVPlayer, VLC, and FFmpeg.

> Full guide & browser tester: **[m3u8play.net/help/public-hls-test-streams/](https://m3u8play.net/help/public-hls-test-streams/)**

## Working Public M3U8 URLs

| Stream | Type | URL | Quick Browser Test |
| :--- | :--- | :--- | :--- |
| **Big Buck Bunny (Mux)** | VOD · Multi-bitrate · H.264/AAC | `https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8` | [Play Online](https://m3u8play.net/?url=https%3A%2F%2Ftest-streams.mux.dev%2Fx36xhzz%2Fx36xhzz.m3u8) |
| **Mux Test Stream 001** | VOD · Multi-rendition | `https://test-streams.mux.dev/test_001/stream.m3u8` | [Play Online](https://m3u8play.net/?url=https%3A%2F%2Ftest-streams.mux.dev%2Ftest_001%2Fstream.m3u8) |
| **Akamai Public Live** | 24/7 Live · Sliding Window | `https://cph-p2p-msl.akamaized.net/hls/live/2000341/test/master.m3u8` | [Play Online](https://m3u8play.net/?url=https%3A%2F%2Fcph-p2p-msl.akamaized.net%2Fhls%2Flive%2F2000341%2Ftest%2Fmaster.m3u8) |
| **Tears of Steel (Unified Streaming)** | VOD · Adaptive HLS | `https://demo.unified-streaming.com/k8s/features/stable/video/tears-of-steel/tears-of-steel.mp4/.m3u8` | [Play Online](https://m3u8play.net/?url=https%3A%2F%2Fdemo.unified-streaming.com%2Fk8s%2Ffeatures%2Fstable%2Fvideo%2Ftears-of-steel%2Ftears-of-steel.mp4%2F.m3u8) |
| **Apple BipBop (fMP4 / CMAF)** | VOD · Apple Reference · fMP4 | `https://devstreaming-cdn.apple.com/videos/streaming/examples/img_bipbop_adv_example_fmp4/master.m3u8` | [Play Online](https://m3u8play.net/?url=https%3A%2F%2Fdevstreaming-cdn.apple.com%2Fvideos%2Fstreaming%2Fexamples%2Fimg_bipbop_adv_example_fmp4%2Fmaster.m3u8) |
| **Apple BipBop 4x3 (MPEG-TS)** | VOD · Apple Reference · TS | `https://devstreaming-cdn.apple.com/videos/streaming/examples/bipbop_4x3/bipbop_4x3_variant.m3u8` | [Play Online](https://m3u8play.net/?url=https%3A%2F%2Fdevstreaming-cdn.apple.com%2Fvideos%2Fstreaming%2Fexamples%2Fbipbop_4x3%2Fbipbop_4x3_variant.m3u8) |

## Quick Diagnostics

### Check manifest & CORS headers via curl
```bash
curl -I -H "Origin: https://m3u8play.net" \
  "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8"
```

### Convert an authorized VOD M3U8 to MP4 with FFmpeg
```bash
ffmpeg -i "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8" \
  -c copy -bsf:a aac_adtstoasc output.mp4
```

Need custom `Referer`, `User-Agent`, or `Cookie` flags? Use the **[M3U8 to MP4 FFmpeg Command Generator](https://m3u8play.net/m3u8_to_mp4/)**.

## Helpful Guides
- [Fix M3U8 CORS Errors (Nginx, Apache, S3 & Cloudflare)](https://m3u8play.net/help/m3u8-cors-errors/)
- [Diagnose M3U8 403 Forbidden Errors](https://m3u8play.net/help/m3u8-403-forbidden/)
- [Why Safari Plays HLS but Chrome Cannot](https://m3u8play.net/help/why-safari-plays-hls-but-chrome-cannot/)
