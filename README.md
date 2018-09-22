# mediawiki-PortableInfobox
Port of FANDOM's https://github.com/Wikia/app/tree/dev/extensions/wikia/PortableInfobox extension to the MediaWiki 1.31+

## Installation
Grab the latest release from [GitHub](https://github.com/Luqgreg/mediawiki-PortableInfobox/releases/latest) and unpack it into `extensions\PortableInfobox` directory in your MediaWiki installation or clone this repository, by using these commands:
```bash
cd extensions
git clone https://github.com/Luqgreg/mediawiki-PortableInfobox.git PortableInfobox --branch master --depth 1
```

and add the following code at the bottom of [LocalSettings.php](https://www.mediawiki.org/wiki/Manual:LocalSettings.php):
```php
wfLoadExtension( 'PortableInfobox' );
```

## Configuration
You can use several variables to modify extension's behaviour:
- `$wgAllInfoboxesMiserMode` (bool) - force AllInfoboxes query to be cached, even if `$wgMiserMode` is disabled. (default: true)
- `$wgAllInfoboxesSubpagesBlacklist` (array) - list of subpages in template namespace to omit by AllInfoboxes query. (default: [ "doc", "draft", "test" ])
- `$wgPortableInfoboxCustomImageWidth` (int) - size of image thumbnails used in infoboxes. (default: 300)

## Usage
See: https://community.wikia.com/wiki/Help:Infoboxes

### `<media />` tag
In the dev version, the `<media/>` tag was introduced in favor of `<image/>`, which still works (see (#aliases)). It allows users to embed images, videos, and audio files in the infobox, in the same way as `<image />` tag does in the original version.

#### Attributes
- `source` - name of the parameter
- `audio` - If set to `false`, it ignores all audio files
- `image` - If set to `false`, it ignores all images
- `video` - If set to `false`, it ignores all videos

#### Child tags
- `<default>`
- `<caption>`

#### Aliases
- `<audio />` - variation of `<media />` tag that allows only audio files
- `<image />` - variation of `<media />` tag that allows only images and videos (for backwards compatibilty, can be disabled with `video="false"`)
- `<video />` - variation of `<media />` tag that allows only videos

## User-facing differences from the original version
- It's based on Wikia/app@b9fcbe5d6db928e318d64ad0568ec2d09a3f406e and there might be some features, that were introduced in the original version at a later date, but they're absent here
- Europa theme was removed.
- `.pi-theme-default` class is applied instead of `.pi-theme-wikia` to the infobox, when no theme is specified.
- When a `<gallery>` tag is passed to the infobox with images without captions, file name is used instead of not showing the image.
- When embedding a video in the infobox additional class `.pi-video` is added to the `<figure>` tag.
- Videos use `<video>` tags instead of showing video in a modal after clicking a thumbnail.
- `.pi-image` class is no longer present in the `<figure>` tag with a video, instead `.pi-media` class is applied to **all** media elements.
- `.pi-image-collection` classes were changed to `.pi-media-collection`.
- Mobile skin doesn't get separate styling.
- It may be *a little* more buggy :)