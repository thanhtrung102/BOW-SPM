# Scene Recognition using Bag of Visual Words with Spatial Pyramid Matching

This software implements a bag of visual words model to classify images belonging to a subset of the SUN dataset into 8 classes.

## Methodology

- First a vocabulary of visual words is constructed by densely sampling SIFT features, and clustering them into visual words via K-means.
- The training images are then represented as histograms of these visual words, which are TF-IDF re-weighted to enhance the importance of discriminative features.
- One-vs-all linear SVM classifiers are then trained on these histograms.
- At query-time, the test image is sampled densely for features, which are mapped to words using K-means to construct the histogram. This histogram is identically re-weighted and then passed through the SVM classifiers.

**Spatial Pyramid Matching:**  
Bag of visual words does not account for the spatial locations of occurence of the visual words. To account for this, spatial pyramid matching divides the image into $4^l$ regions at each level $l=0, 1, 2, ...$, and concatenates a weighted version of the histograms from each level, paying more attention to deeper levels, which are more spatially focussed <a href="#ref1">\[1\]</a>.

**Experimentation:**  
The effect of variations and parameter tuning and an analysis of this effect is also presented.

## To run
*All commands to be run from the repository root.*  
1. Unzip the dataset.
   ```(shell)
   unzip dataset/SUN_data.zip -d dataset/
   ```
2. Install python packages from the Python Package Index (preferably in a virtual environment).
   ```(shell)
   python3 -m venv bovw-env && source bovw-env/bin/activate # optional
   pip install -r requirements.txt
   ```
3. Run the notebook on a jupyter server.
   ```(shell)
   jupyter notebook
   ```
   Open `src/bovw.ipynb` in the web browser window.

---
<a id="ref1">[1]</a> Lazebnik, Svetlana & Schmid, Cordelia & Ponce, J.. (2006). Beyond Bags of Features: Spatial Pyramid Matching for Recognizing Natural Scene Categories. In CVPR. 2. 2169 - 2178. 10.1109/CVPR.2006.68. 
