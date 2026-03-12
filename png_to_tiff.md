PNG to TIFF converter for high-resolution figures

This R script converts PNG images into high-resolution TIFF files (600 dpi) using the magick package.
The purpose of the script is to prepare figures for manuscript submission or document preparation where TIFF format is required by journals or recommended to preserve image quality.

The script:
	•	reads all PNG images from a specified directory
	•	converts each image to TIFF format
	•	applies a resolution of 600 dpi
	•	disables compression to preserve image fidelity
	•	saves the converted files into a dedicated output folder.

Usage
	1.	Modify the input path to your image directory:

files <- list.files("~/path/to/your/images", pattern="png$", full.names=TRUE)

	2.	Run the script in R.
	3.	Converted TIFF files will be saved in:

~/Desktop/immages/tiff_files

Requirements

The script requires the R package:

magick

Install it with:

install.packages("magick")

Use case

This utility is particularly useful when preparing figures for:
	•	scientific manuscripts
	•	thesis documents
	•	journal submissions requiring TIFF figures
	•	workflows where PNG screenshots must be converted to publication-ready formats.


## Script

```r
library(magick)

files <- list.files("~/path/to/your/images", pattern="png$", full.names=TRUE)

dir.create("~/Desktop/immages/tiff_files", showWarnings=FALSE)

for(f in files){

  img <- image_read(f)

  name <- tools::file_path_sans_ext(basename(f))

  image_write(
    img,
    path=paste0("~/Desktop/immages/tiff_files/",name,".tiff"),
    format="tiff",
    density="600x600",
    compression="none"
  )

}
