# Reflex Python client

Reflex is an image manipulation tool built for the Web. This is the Python client.

## Installation

Install the `reflex-client` via pip:

`pip install reflex-client`

## Examples

400x400 crop:

```
>>> from reflex import transform
>>> transform("https://a.reflex.se.am/", "http://example.com/image.jpg", ["400x400"])
'http://a.reflex.se.am/400x400/http://example.com/image.jpg'
```

400x400 crop on a batch of images:

```
>>> from reflex import batch_transform
>>> images = [
...     "http://example.com/image1.jpg",
...     "http://example.com/image2.jpg",
...     "http://example.com/image3.jpg",
... ]
>>> batch_transform(
...     "https://a.reflex.se.am/",
...     images,
...     ["400x400"]
... )
['https://a.reflex.se.am/400x400/http://example.com/image1.jpg', 'https://a.reflex.se.am/400x400/http://example.com/image2.jpg', 'https://a.reflex.se.am/400x400/http://example.com/image3.jpg']
```

Sign a source URL

```
>>> from reflex import sign_transform
>>> sign_transform("http://example.com/image1.jpg", key="testkey")
'yclO5mOVIZLnvOIkEYj7b_jvXpyYyVCWAAgCQ-b0GyY='
```

This is helpful if you'd like to generate source-signed transforms using a client-side language like Javascript (i.e. using `reflex-js`), but wish not to (and definitely should not) expose your Reflex `key`. Instead, the signature for a given `source_url` and Reflex `key` can be generated server side and exposed via a RESTful API or bootstrapped with the page.


Using the Client

```
>>> from reflex import Client
>>> r = Client("https://a.reflex.se.am/", key="testkey")
>>> r.transform("http://example.com/image1.jpg", "400x400")
'https://a.reflex.se.am/400x400,syclO5mOVIZLnvOIkEYj7b_jvXpyYyVCWAAgCQ-b0GyY=/http://example.com/image1.jpg'
```

The `Client` can be used to persist credentials that are likely to be shared between multiple transformations, e.g. `proxy_url` and `key`.

## Operations

### Crop/resize

A crop/resize operation should be specified as `{width}x{height}`, `{width}x`, `x{height}` or simply a single value with no `x` separator if the value is to be used for both `width` and `height`. Integer values greater than 1 (e.g. `150x100`) are interpreted as exact pixel values and floats between 0 and 1 (e.g. `0.15x`) are interpreted as percentages of the original image size. Cropping will occur when both `width` and `height` values are provided, and they do not preserve the original aspect ratio of the image.

### Fit

The `fit` operation should be specified together with a crop/resize operation and will ensure resize operations fit within a containing box of the specified size whilst retaining the original aspect ratio.

### Rotate

The `r{degrees}` operation can be used in increments of 90 (`90`, `180` and `270`) degrees to rotate the image counter-clockwise. This operation has a lower precidence than crop/resize.

### Flip

The `fv` and `fh` operations flip an image vertically and horizontally, respectively. This has a lower precedence than the rotate operation.

### Quality

The `q{percentage}` operation is used to specify the output quality. If not specified, a default value of 95 is used. Currently only JPEG is supported.
