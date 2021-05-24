# above
This project is part of NASA's Arctic Boreal and Vulnerability Experiment (ABoVE).
<br><br>
<b>Name:</b> Darko Radakovic (PhD)<br>
<b>Title:</b> An integrated CANAPANI and Deep-learning based approach for mapping of tall shrubs in Arctic tundra<br>
<b>Supervisor:</b> Dr. M.J. Chopping<br><br>
Montclair State University<br><br>

<h1>Abstract</h1>
The Arctic is changing rapidly with climate warming (Zhang et al., 2018). Observational studies have detected a recent increase in aboveground biomass consisting mainly of grasslands and shrubs. The implications of a changing vegetation and shrub cover in the Arctic is complex and shows signs of both an increase and a decrease in cover as a result of increasing temperatures. The effect of the changing Arctic vegetative surface on the Albedo is difficult to measure. This proposal will investigate shrub surface change over a period of around 15 years in Northern Alaska and Canada by the use of state-of-the-art deep learning algorithms to auto detect shrubs in high resolution satellite imagery. These will be obtained and orthorectified from NASA's Arctic Boreal Vulnerability Experiment (ABoVE) project and analysed to find specific imagery that contains shrubs. This research will then use a Machine Learning (ML) approach (Region Based Convolutional Neural Networks, Mask R-CNN) to train a model’s ability to auto-detect tall shrubs from around 2004 and around 2016. Training datasets will be obtained from Canopy Analysis with Panchromatic and Normalized difference vegetation index (NDVI) Imagery (CANAPANI) that provides tall shrub locations from panchromatic and NDVI imagery and would enhance the detection accuracy of the ML model. Eventually, the difference in the surface area of shrubs will be a good indicator of the Albedo change for the same period of time (around 10-15 years). The importance of this study will show signs of how global temperature increases affect the amount of solar radiation (albedo) with an Arctic vegetative surface consisting mainly of tall and low-shrubs. Eventually, the algorithm can be used in other locations and the outcomes of this research will provide data that can be used to validate ecological models.



<h1>Methods</h1>

Study area
Our study area encompasses two domains, the Northern Alaskan and Canadian arctic zone.
Imagery
Applying deep learning algorithms to detect shrubs in the Northern Alaska territories will require high resolution satellite images. In order to be able to obtain the effects of climate change on the shrub area (increase or decrease), a time period of 15-20 years will be necessary. Quickbird panchromatic (0,65 m resolution) and multispectral satellite images from 2003-2006 and Worldview 2 (0.46 m resolution), 3 (0.31 m resolution) and 4 (0.31 m resolution) are cloud-free available from the ABoVE Science Cloud (2021) and will be chosen based on the availability for a certain location containing shrubs visually inspected in Google Earth Pro and the commercial Maxar’s Digitalglobe (used for finding high resolution imagery identifiers). Orthorectification is applied with a Geospatial Data Abstraction Library (GDAL, https://www.gdal.org), a translator library for raster and vector geospatial data formats, and used with Esri's ArcGIS suite to assess the shrub cover visually. Pansharpening will be applied on multispectral imagery to improve resolution
CANAPANI model for annotating data
Subsets with dimensions of 500 x 500m grids from Panchromatic, NDVI and Multispectral imagery of the Northern Alaskan and Canadian arctic will be selected for annotation. The dimension is chosen based on two considerations: (1) maximum number of shrubs per subset; and (2) to minimize false positives. NDVI maps are produced and used in CANAPANI together with Panchromatic imagery. CANAPANI uses the input through several steps to identify crowns (Chopping et al., 2018), while the ML algorithm will use Joint Photographic Experts Group (.jpg) formats derived from Multispectral imagery. The rapid and accurate output of CANAPANI is converted into a JavaScript Object Notation (JSON) file format with a one class shrub and used as training, validation and testing data for the ML algorithm. Training will be tested on both one class and multiple shrub classes, which will be manually identified from the CANAPANI produced JSON annotated file to see if multiple shrub classes can improve the ML accuracy.
Finally, the annotated dataset will be randomly splitted into three sub datasets based on an 80:10:10 split in training, validation and testing sets(Zhang et al., 2018b)

Machine Learning model
The Mask R-CNN algorithm is a fast and effective algorithm for object detection and is built upon the Faster R-CNN by including a function for predicting masks for unique objects (He et al., 2017; Zhang et al., 2018b). This ML algorithm consists of two stages: (1) it generates proposed objects regions from scanned images; (2) it predicts classes, bounding boxes and binary masks for regions of interest (RoI). The backbone architecture works on the Residual Learning Network (ResNet, He et al., 2016) The basic Mask R-CNN algorithm written in open sourced package Keras and Tensorflow can be acquired from Github (https://github.com/matterport/Mask_RCNN) and trained in the open sourced Google Colab that offers free, but time limited 12 GPUs. This proposal will make use of the new Prism Graphic Processing unit (GPU) Cluster from NASA Center for Climate Simulation offering ML capabilities of a 22-node GPU cluster, with NVIDIA v100 GPUs and increasing training time for large datasets. 
The ML algorithm workflow consists of 3 key steps: (1) loading the imagery with the associated annotated datasets; (2) object instance segmentation and classification based on the class from the dataset; (3) mask-to-polygon conversion; and (4) eliminating duplicate polygons.
The training will be carried out using ResNet50 (capable to classify up to a 1000 classes). Parameter, such as the Detection confidence and Kernel sizes, will be explored to find an optimal training scheme for large datasets produced from CANAPANI.




<h1>References:</h1><br>
ABoVE Science Cloud (ASC). (2021). NASA Center for Climate Simulation (NCCS). https://above.nasa.gov/sciencecloud.html

Chopping, M., Duchesne, R., Erb, A, Wang, Z., Schaaf, C., and Chopping, C. (2018), CANAPANI: A New Version of CANAPI for Mapping Tall Shrub Canopies in Arctic Tundra, NASA Arctic Boreal Vulnerability Experiment (ABoVE) Science Team Meeting, Seattle, WA, January 22 – 26, 2018.

He K., Gkioxari G., Dolll´ar P., Girshick R. (2017). Mask R-CNN. In International Conference on Computer Vision (ICCV): 2, 8.

NASA Arctic Boreal Vulnerability Experiment (ABoVE) Science Team Meeting, Seattle, WA, January 22 – 26, 2018.

Zhang, Y., Sherstiukov, A. B., Qian, B., Kokelj, S. V., Lantz, T. C. (2018a). Impacts of snow on soil temperature observed across the circumpolar north. Environmental Research Letters. 13(4), 044012. doi: 10.1088/1748-9326/aab1e7

Zhang, W., Witharana, C., Liljedahl, A.K., Kanevskiy, M. (2018b). Deep Convolutional Neural Networks for Automated Characterization of Arctic Ice-Wedge Polygons in Very High Spatial Resolution Aerial Imagery. Remote Sens. 10, 1487. https://doi.org/10.3390/rs10091487

Built upon Matterplot Mask R-CNN:
https://github.com/matterport/Mask_RCNN
