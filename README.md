# pdf-to-image-use-PyMuPDF
pdf转图片

```markdown

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
使用方法：
```bash
pip install PyMuPDF==1.22.5
pip install fitz
```
来源：[Stack Overflow](https://stackoverflow.com/a/47877930/21496440)
