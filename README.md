Task items

1. Get [DeepEraser](https://github.com/fh2019ustc/deeperaser) model running locally. They have a `demo.py` [file (here)](https://github.com/fh2019ustc/DeepEraser/blob/master/demo.py) and we need to figure out how to format the mask image. We also want to understand what the model's parameters are (e.g., what do they resize each image to, etc.). We also want to test the model on some real data from RVL-CDIP. Also play around with their live hosted demo [here](https://deeperaser.doctrp.top:20443/). Compare this method to OpenCV's inpainting tool.

2. Common PII entity pattern categorizer. See below.
   
3. Text line orientation estimation. [Pytesseract](https://pypi.org/project/pytesseract/) [seems to have some functionality](https://stackoverflow.com/a/55302299) for estimating the angle or orientation of text lines. 

### 1. Mimicing Page Background
The page background color/texture behind the de-identified text must be preserved, if possible.
For documents with dark text on white page background, this is easy. But for documents with
page backgrounds that aren't white (or a solid color), this is harder. We can experiment with 
[DeepEraser](https://github.com/fh2019ustc/deeperaser) and similar tools to see if we can mimic page background.

### 2. Entity Pattern Categorizer
We want to mimic the format of PII entities. For instance, if a date appears in a document as `June 18, 1999`
then we'll want to replace it with a new date in the same format (e.g., `May 19, 1997`).
There are several common date formats, like `Month DD, YYYY`, `MM/DD/YYYY`, etc.).
We desire a model/algorithm to bin dates into several of these categories.
I.e., 
```
"June 18, 1999" --> model --> "Month DD, YYYY"
```
Additionally, there are several other entities where we want something similar.
These include names (`firstname lastname`, `lastname, first_initial`, `first_initial lastname`, etc.).

### 3. Text line orientation estimation
An entity may appear rotated in a document. Or, a document may be rotated. We want a way to determine how much rotation an entity or document has.
It looks like Tesseract/Pytesseract has functionality for estimating this, but we will want to determine how accurate their functionality is.
