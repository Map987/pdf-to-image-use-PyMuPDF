# pdf-to-image-use-PyMuPDF
pdf转图片

## 使用方法：
首先，安装必要的库
```bash
pip install PyMuPDF==1.22.5
pip install fitz

```

## 代码示例
然后，使用以下 Python 代码提取 PDF 中的图像：
```
import fitz
doc = fitz.open("file.pdf")
for i in range(len(doc)):
    for img in doc.get_page_images(i):
        xref = img[0]
        pix = fitz.Pixmap(doc, xref)
        if pix.n - pix.alpha < 4:       # this is GRAY or RGB
            pix.save("p%s-%s.png" % (i, xref))
        else:               # CMYK: convert to RGB first
            pix1 = fitz.Pixmap(fitz.csRGB, pix)
            pix1.save("p%s-%s.png" % (i, xref))
            pix1 = None
        pix = None

```
来源：[Stack Overflow](https://stackoverflow.com/a/47877930/21496440)
## 在线运行
在 Google Colab 中运行此代码：
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Map987/pdf-to-image-use-PyMuPDF/blob/main/Untitled62.ipynb)

