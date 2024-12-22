# imgutils

[![GitHub license](https://img.shields.io/github/license/deepghs/imgutils)](https://github.com/deepghs/imgutils/blob/master/LICENSE)

A convenient and user-friendly anime-style image data processing library that integrates various advanced anime-style
image processing models.

This python package is based on [deepghs/imgutils](https://github.com/deepghs/imgutils) work.

## Installation

You can simply install it with `pip` command line from the official PyPI site.

```shell
pip install -e .
```

<!-- If your operating environment includes a available GPU, you can use the following installation command to achieve higher
performance:

```shell
pip install dghs-imgutils[gpu]
``` -->

For more information about installation, you can refer
to [Installation](https://deepghs.github.io/imgutils/main/tutorials/installation/index.html).

### Object Detection

Currently, object detection is supported for anime heads and person, as shown below

- Face Detection

<!-- ![face detection](https://github.com/deepghs/imgutils/blob/gh-pages/main/_images/face_detect_demo.plot.py.svg) -->

- Head Detection

<!-- ![head detection](https://github.com/deepghs/imgutils/blob/gh-pages/main/_images/head_detect_demo.plot.py.svg) -->

- Person Detection

<!-- ![person detection](https://github.com/deepghs/imgutils/blob/gh-pages/main/_images/person_detect_demo.plot.py.svg) -->

Based on practical tests, head detection currently has a very stable performance and can be used for automation tasks.
However, person detection is still being further iterated and will focus on enhancing detection capabilities for
artistic illustrations in the future.

The head detection model can be found at https://huggingface.co/deepghs/anime_head_detection .

### Truncated Image Check

The following code can be used to detect incomplete image files (such as images interrupted during the download
process):

```python
from imgutils.validate import is_truncated_file

if __name__ == '__main__':
    filename = 'test_jpg.jpg'
    if is_truncated_file(filename):
        print('This image is truncated, you\'d better '
              'remove this shit from your dataset.')
    else:
        print('This image is okay!')

```

### Character Extraction

When we need to extract the character parts from anime images, we can use
the [`segment-rgba-with-isnetis`](https://deepghs.github.io/imgutils/main/api_doc/segment/isnetis.html#segment-rgba-with-isnetis)
function for extraction and obtain an RGBA format image (with the background part being transparent), just like the
example shown below.

<!-- ![isnetis](https://deepghs.github.io/imgutils/main/_images/isnetis_trans.plot.py.svg) -->

```python
from imgutils.segment import segment_rgba_with_isnetis

mask_, image_ = segment_rgba_with_isnetis('hutao.png')
image_.save('hutao_seg.png')

mask_, image_ = segment_rgba_with_isnetis('skadi.jpg')
image_.save('skadi_seg.png')
```

This model can be found at https://huggingface.co/skytnt/anime-seg .
