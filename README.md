Fork of https://github.com/yasushi-saito/cloudflare-zlib

## Changes from upstream

- Remove inlined zlib
  - You should install zlib yourself
  - From brief testing it should be compatible with normal zlib as well.
- Added Flush method
- Added Version method
- Added Reset method
  - To accommodate this change, the Close method no longer call deflateEnd. Instead, it is done using finalizer. 

## Using this with cloudflare-zlib

This module *does not* ship with Cloudflare's implementation of zlib. Instead, it will link with any zlib you have installed.

To use it with cloudflare-zlib, you should install it

**WARNING** This instruction is tested on Docker - it MAY or may not break your system if you replace the original zlib.

```sh
git clone https://github.com/cloudflare/zlib
cd zlib
CFLAGS="-march=native -mtune=native -O3" ./configure
make
cp libz.so* /usr/lib/
```

Then build your app accordingly:

```sh
CGO_CFLAGS="-I/path/to/zlib" CGO_LDFLAGS="-I/path/to/zlib -lz" go build ./...
```
