# Text Encode Transformations

## Overview

This is a prollyfill for the transform streams TextEncoderStream and
TextDecoderStream. It is based on the draft changes to the Encoding Standard
here:

http://htmlpreview.github.io/?https://github.com/ricea/encoding-streams/blob/master/patch.html

However, it may be out-of-sync with that document.

This is intended for experimentation and development of the standard.

## Requirements

You need implementations of TextEncoder, TextDecoder, ReadableStream,
WritableStream and TransformStream, either natively or via polyfill.

## How to use

Include the prollyfill in the page:

```javascript
<script src="text-encode-transform.js">
```

It can also be used in a Worker environment:

```javascript
importScripts('text-encode-transform.js');
```

Then you can use it in a pipe like this:

```javascript
byteSource
  .pipeThrough(new TextDecoderStream())
  .pipeTo(textDestination);
```

Any arguments that the TextDecoder constructor normally accepts will also work
when used as a stream transform.

TextEncoderStream works the same way:

```javascript
textSource
  .pipeThrough(new TextEncoderStream())
  .pipeTo(byteDestination);
```

## Tests

Tests in web-platform-test format are included in the tests/ directory. The
tests use infrastructure from the https://github.com/w3c/web-platform-tests
repository. You will need to run the tests under the web-platform-tests HTTP
server.

The tests expect the TransformStream polyfill to be installed in a parallel
directory to this one named transform-stream-polyfill. You can get the polyfill
from
https://github.com/whatwg/streams/blob/transform-stream-polyfill/reference-implementation/contrib/transform-stream-polyfill.js

The tests import the polyfills from tests/resources. By default symbolic links
are used; if they don't work in your environment they can just be copied
there. If your browser supports TransformStream natively then replacing
tests/releases/transform-stream.js with an empty file should work.

### See also

 - [Encoding Living Standard][]
 - [Streams Living Standard][]

[Encoding Living Standard]: https://encoding.spec.whatwg.org/
[Streams Living Standard]: https://streams.spec.whatwg.org/

### Disclaimer

This is not an official Google product.
