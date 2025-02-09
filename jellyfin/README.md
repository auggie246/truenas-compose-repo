## Important Notes

1. If you are unable to scrub the timeline when using jellyfin on a webrowser or with the media player. It is likely due to the use of Cloudflare Proxy.
You will need to create a cache rule with a custom filter expression using `URI Full` as the field and your Jellyfin URI e.g `jellyfin.domain.com/*` as the Value using `wildcard` as the Operator.

2. HDR Tone Mapping does not work on Firefox browsers. I do not know why yet.