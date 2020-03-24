# Aseprite TGA Library

> Distributed under [MIT license](LICENSE.txt)

Library to read/write [Truevision TGA/TARGA files](https://en.wikipedia.org/wiki/Truevision_TGA).

Example:

```c++
#include "tga/tga.h"

#include <cstdio>
#include <vector>

int main(int argc, char* argv[])
{
  if (argc < 2)
    return 1;

  FILE* f = std::fopen(argv[1], "rb");
  tga::StdioFileInterface file(f);
  tga::Decoder decoder(&file);
  tga::Header header;
  if (!decoder.readHeader(header))
    return 2;

  tga::Image image;
  image.bytesPerPixel = header.bytesPerPixel();
  image.rowstride = header.width * header.bytesPerPixel();

  std::vector<uint8_t> buffer(image.rowstride * header.height);
  image.pixels = &buffer[0];

  if (!decoder.readImage(header, image, nullptr))
    return 3;

  return 0;
}
```
