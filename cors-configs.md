# M3U8 / HLS CORS Server Configuration Snippets

When an `.m3u8` URL plays in VLC or FFmpeg but fails in Chrome, Firefox, or Safari, missing CORS headers on playlists or `.ts` / `.m4s` segments are the usual cause.

> Full guide & troubleshooting checklist: **[Fix M3U8 CORS Errors](https://m3u8play.net/help/m3u8-cors-errors/)**

## Quick `curl` Check
```bash
curl -I -H "Origin: https://m3u8play.net" \
  "https://your-cdn.example.com/hls/master.m3u8"
```

## Nginx
```nginx
location ~* \.(m3u8|ts|m4s|mp4|vtt|key)$ {
    add_header 'Access-Control-Allow-Origin' '*' always;
    add_header 'Access-Control-Allow-Methods' 'GET, HEAD, OPTIONS' always;
    add_header 'Access-Control-Allow-Headers' 'Origin, Range, Accept-Encoding, Referer' always;
    add_header 'Access-Control-Expose-Headers' 'Content-Length, Content-Range' always;

    if ($request_method = 'OPTIONS') {
        add_header 'Access-Control-Max-Age' 1728000;
        return 204;
    }
}
```

## Apache (`.htaccess`)
```apache
<IfModule mod_headers.c>
  <FilesMatch "\.(m3u8|ts|m4s|vtt|key)$">
    Header set Access-Control-Allow-Origin "*"
    Header set Access-Control-Allow-Methods "GET, HEAD, OPTIONS"
    Header set Access-Control-Allow-Headers "Origin, Range, Accept-Encoding"
    Header set Access-Control-Expose-Headers "Content-Length, Content-Range"
  </FilesMatch>
</IfModule>
```

## AWS S3 / Cloudflare R2 (CORS JSON)
```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "HEAD"],
    "AllowedOrigins": ["*"],
    "ExposeHeaders": ["Content-Length", "Content-Range"],
    "MaxAgeSeconds": 3600
  }
]
```

After updating your CDN or origin headers (and adding `Vary: Origin` if restricting to specific domains), test playback live at **[m3u8play.net](https://m3u8play.net/)**.
