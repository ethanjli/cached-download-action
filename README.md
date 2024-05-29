# Cached Download GitHub Action

GitHub action for simpler cached downloading of individual files.

This action is just a convenience wrapper around [actions/cache](https://github.com/actions/cache)
which sets up appropriate file permissions for actions/cache and handles downloading of files for
the cache, so that a single action can be used instead of three separate actions (especially when
cached downloading of individual files is meant to be an implementation detail of a GitHub Actions
workflow).

## Basic Usage Examples

### URL as caching key

```yaml
- name: Download a Raspberry Pi OS image
  uses: ethanjli/cached-download-action@v0.1.0
  with:
    url: wget https://downloads.raspberrypi.com/raspios_lite_arm64/images/raspios_lite_arm64-2024-03-15/2024-03-15-raspios-bookworm-arm64-lite.img.xz
    destination: /tmp/downloads-cache/2024-03-15-raspios-bookworm-arm64-lite.img.xz
```

### Custom caching key

```yaml
- name: Download a Raspberry Pi OS image
  uses: ethanjli/cached-download-action@v0.1.0
  with:
    url: wget https://downloads.raspberrypi.com/raspios_lite_arm64/images/raspios_lite_arm64-2024-03-15/2024-03-15-raspios-bookworm-arm64-lite.img.xz
    destination: /tmp/downloads-cache/2024-03-15-raspios-bookworm-arm64-lite.img.xz
    cache-key: base-image-2024-03-15-raspios-bookworm-arm64-lite
```

## Usage Options

Inputs:

| Input         | Allowed values | Required?       | Description                                                        |
|---------------|----------------|-----------------|--------------------------------------------------------------------|
| `url`         | HTTP(S) url    | yes             | URL of the file to download.                                       |
| `destination` | file path      | yes             | Path to load the cached file from, or save the downloaded file to. |
| `cache-key`   | string         | no (default ``) | An explicit key for a cache entry.                                 |

- If `cache-key` is empty, then the `url` input will be used as the cache key instead.

Outputs:

- `destination` is the path of the downloaded file. This is literally just the same as the
  `destination` input.

## Credits

This action is just a simple usability wrapper around
[actions/cache](https://github.com/actions/cache), which does all of the caching-related work.
