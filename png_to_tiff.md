## PNG to TIFF Conversion Script

This R script converts **PNG images into high-resolution TIFF files (600 dpi)** using the `magick` package.  
It is useful when preparing figures for **scientific manuscripts, theses, or journal submissions** where TIFF format is required or recommended to preserve image quality.

### What the script does

- Reads all PNG images from a specified directory
- Converts each image to TIFF format
- Applies a resolution of **600 dpi**
- Disables compression to preserve image fidelity
- Saves the converted images into a dedicated output folder

## Usage

1. Modify the input path to your image directory:

```r
files <- list.files("~/path/to/your/images", pattern = "png$", full.names = TRUE)
```

2. Run the script in R.

3. Converted TIFF files will be saved in:

```
~/Desktop/images/tiff_files
```

---

## Requirements

The script requires the following R package:

- **magick**

Install it with:

```r
install.packages("magick")
```

### Script

```r
library(magick)

# List all PNG images in the input directory
files <- list.files("~/path/to/your/images", pattern = "png$", full.names = TRUE)

# Create output directory if it does not exist
dir.create("~/Desktop/immages/tiff_files", showWarnings = FALSE)

# Convert each PNG file to TIFF
for (f in files) {

  img <- image_read(f)

  name <- tools::file_path_sans_ext(basename(f))

  image_write(
    img,
    path = paste0("~/Desktop/immages/tiff_files/", name, ".tiff"),
    format = "tiff",
    density = "600x600",
    compression = "none"
  )

}
