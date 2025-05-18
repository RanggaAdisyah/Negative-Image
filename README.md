## Workflow of the Negative‐Image Conversion

1. **Load the Original Image**

   * Use PIL to open your source file:

     ```python
     from PIL import Image
     CITRA = Image.open('Foto\\gambar.jpeg')
     ```
   * Now `CITRA` holds the full-color image in memory.

2. **Read Image Dimensions**

   * `ukuran_horizontal = CITRA.size[0]` → width (number of columns).
   * `ukuran_vertikal   = CITRA.size[1]` → height (number of rows).

3. **Access the Pixel Array**

   * Call `PIXEL = CITRA.load()` to get a pixel‐access object.
   * You can now read or write any pixel by its (x, y) coordinates.

4. **Loop Over Every Pixel**

   * Two nested loops cover every row (`x` from 0 to height−1) and column (`y` from 0 to width−1):

     ```python
     for x in range(ukuran_vertikal):
         for y in range(ukuran_horizontal):
             # process pixel at (y, x)
     ```
   * Note the order: first over vertical (rows), then horizontal (columns).

5. **Compute the Negative Color**

   * For each pixel you get a 3-tuple `(R, G, B)`.
   * Invert each channel by subtracting from 255:

     ```python
     R_new = 255 - old_R
     G_new = 255 - old_G
     B_new = 255 - old_B
     ```
   * This “flips” bright to dark and vice versa.

6. **Write Back the Inverted Pixel**

   * Replace the old pixel with the new one:

     ```python
     PIXEL[y, x] = (R_new, G_new, B_new)
     ```

7. **Save the Result**

   * After all pixels are processed, write out the negative image:

     ```python
     CITRA.save('hasil_negatif.jpeg')
     ```
   * You’ll get a file named `hasil_negatif.jpeg` containing the color-inverted version.

---

### Full Example in Context

```python
from PIL import Image

# 1. Load image
CITRA = Image.open('Foto\\gambar.jpeg')

# 2. Get dimensions
ukuran_horizontal = CITRA.size[0]
ukuran_vertikal   = CITRA.size[1]

# 3. Access pixel data
PIXEL = CITRA.load()

# 4–6. Invert every pixel
for x in range(ukuran_vertikal):
    for y in range(ukuran_horizontal):
        r, g, b = PIXEL[y, x]
        PIXEL[y, x] = (255 - r, 255 - g, 255 - b)

# 7. Save the negative image
CITRA.save('hasil_negatif.jpeg')
```
