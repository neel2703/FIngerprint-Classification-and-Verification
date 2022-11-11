## Problem Statement
Classifying fingerprints such that different impressions from the same finger fall into the same
group reduces the number of comparisons to the database during fingerprint matching. There are
5 significant types of human fingerprints to classify into (with 1 rare type), hence this is a
multiclass classification problem.

## Metadata
### NIST-SD4 Database
The NIST-SD4 is a freely available fingerprint collection, compiled and curated by NIST
(National Institute of Standards and Technology). It is the benchmark dataset for fingerprint
classification tasks. It contains 2000 8-bit grayscale fingerprint image pairs (totaling 4000
images). The database is evenly distributed over each of the five classifications with 400
fingerprint pairs from each class.
● Sensor type: optical, solid-state, touch-free
● Image Size: 512x512
● Resolution: 500 dpi

## Preprocessing Pipeline
To label the NIST-SD4 data, a script is run to rename each file according to the class mentioned
in the corresponding text file.
For the baseline models, the images will simply be flattened into a one-dimensional array and fed
without any feature extraction. To improve these results, feature extraction methods will be
implemented to obtain global characteristics (orientation map and singular points) before feeding
the images into the models.
The preprocessing pipeline will contain multiple steps:
● Normalization: It is used to standardize the intensity values due to sensor noise and finger
pressure in an image by adjusting the range of gray level values so that they extend in a
desired degree of values and improve the contrast of the image. The primary purpose is to
improve the computations by getting the pixel values between a small range.
● Segmentation: In this, a mask is created using blockwise coherence to segment the ridges
from the background. There are more robust methods for segmentation[1] however the
method I used is based on the calculation of the variance of gray levels. Image is divided
into sub-blocks of (W × W) size and for each block, the variance is calculated. Image
normalization is calculated based on the segmented image.
● Orientation Map: Orientation Map consists of obtaining a representation of the local ridge
flow for every subregion (commonly named block) in the fingerprint. Obtaining a ridge
structure is important in the preprocessing pipeline to improve the model performance.
Sobel filters were used to obtain the direction of the field.
● Frequency Map: Calculation of a frequency block In addition to the directional map we
must have the local estimation of the frequency map to be able to construct the Gabor
filter. The frequency map of the image consists of estimating the local frequency of the
streaks in each pixel.
● Gabor Filter: Gabor filters have both frequency-selective and orientation-selective
properties and have an optimal joint resolution in both spatial and frequency domains.
The principle of filtering is to modify the value of the pixels of an image, generally in
order to improve its appearance. In practice, it is a matter of creating a new image using
the pixel values of the original image, in order to select in the Fourier domain the set of
frequencies that make up the region to be detected.
● Skeletonization: To facilitate the extraction of minutiae the image must be skeletonized; a
sequence of morphological erosion operations are used to eliminate the redundant pixels
of ridges until the ridges are just one pixel wide.
● Minutiae Extraction: Crossing Number method is used for this step. The crossing number
method is a really simple way to detect ridge endings and ridge bifurcations. The crossing
number algorithm will look at 3x3 pixel blocks.
● Singularity Points: Singular Points are defined as the locations in the fingerprint with the
greatest ridge orientation variance, i.e., where the ridges vary more abruptly. The
Poincare index method is used for locating the Singular points of the fingerprints. There
are two types of points: Core and Delta. These points are used to classify the fingerprints.
