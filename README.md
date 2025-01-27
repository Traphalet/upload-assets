# upload-assets

GitHub Action to upload multiple assets to a release

## Features

This action aims to resolve several outstanding user requests with [@actions/upload-release-asset](https://github.com/actions/upload-release-asset).

* Getting the latest release tag for upload
* Globbing i.e. `./bin/*`
* Succinct - no need to populate content_type and a separate path input

## Requirements:

You can run into a "socket hangup", if you do, then add permissions for the action to write to contents.

```yaml
    permissions:
      contents: write

      actions: read
      checks: write
      issues: read
      packages: write
      pull-requests: read
      repository-projects: read
      statuses: read
```

## Built for developers by developers

<a href="https://github.com/sponsors/alexellis/">
<img alt="Sponsor this project" src="https://github.com/alexellis/alexellis/blob/master/sponsor-today.png" width="65%" height="65%">
</a>

If you're using this action, <a href="https://github.com/sponsors/alexellis/">consider becoming a sponsor</a> so that I can continue to dedicate time to maintaining it.

## Input variables

You must provide:

* `asset_paths` - the paths to the assets you want to upload as a JSON array. You can use a glob pattern. For example `asset_paths: '["bin/*", "dist/js/*"]'`

## Output variables

*  `browser_download_urls` - the paths to download the uploaded assets

## Example

```yaml
name: publish

on:
  push:
    tags:
      - '*'

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@master
        with:
          fetch-depth: 1
      - name: Make all
        run: make all
      - name: Upload release binaries
        uses: alexellis/upload-assets@0.2.2
        env:
          GITHUB_TOKEN: ${{ github.token }}
        with:
          asset_paths: '["./bin/release-it*"]'
```

Example taken from [this sample project](https://github.com/alexellis/release-it/blob/master/.github/workflows/publish.yaml).

## Creating a new version

Getting started:

```bash
npm i -g  @vercel/ncc
```

Build:

```bash
npm i
npm run build
```

## License

MIT


## Contribution guide

1) Any contributions must be proposed via a GitHub issue for discussion before being worked on.
2) You should also use `git commit -s` and follow the [DCO](https://developercertificate.org).
