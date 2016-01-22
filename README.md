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
