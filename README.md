# Reflex Python client

Reflex is an image manipulation tool built for the Web

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
