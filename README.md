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
- Sensor type: optical, solid-state, touch-free
- Image Size: 512x512
- Resolution: 500 dpi

## EDA
![EDA](![image](https://user-images.githubusercontent.com/82512279/201339135-d5ed6faa-26f9-42b3-a346-e78da8f30844.png)

<br/>

The number of fingerprint images in each class:
- Arch – 800
- Left Loop – 800
- Right Loop – 800
- Tented Arch – 800
- Whorl – 800
<br/>
There is no class imbalance in the NIST-4 dataset.
