# SFND_Radar
## Repository for the Radar project &amp; documentation of the Sensor Fuion Nanodegree

## Implementation of the 2D CFAR 

1. the number of training and guard cells in training and doppler dimension is picked as well as the threshold, a cluster matrix ```cluster_mat``` is initalized as 
zero with dimension of ```RDM``` 
2. The Cell under Test (CUT) is slid across the whole matrix. Herefore we use all the doppler cells (```Nd```) and half of the range cells (```Nr/2```)
3. Inside the loop the whole submatrix based on the properties of each cell type is saved as train matrix 
4. As the train matrix also includes CUT and Guard Cells these are set to 0 as we only want to sum train cells 
5. the cells of train are converted to linear with the ```db2pow``` function of the Signal Processing Toolbox
6. the cells are summed up and averaged based on the number of train cells 
7. the dynamic threshold is computed, in order to do that we nedd to convert back to logarithmic and add our offset
8. if the value of ```RDM``` in position (range_index,doppler_index) is above the threshold the cluster_mat value at this position is set to 1

## Selection of Training, Guard cells and offset
- I selected the values of the cells based on the ones we used before in the course, I made sure to have a higher number of cells in each of the range dimensions
- the threshold was adjusted to avoid false positives and is key in order to ensure a solid reliability

## Steps taken to suppress the non-thresholded cells at the edges 
- I initalized a CFAR cluster matrix ```cluster_mat``` with the dimensions of ```RDM``` and initalized the values as zero 
- The value of ```cluster_mat```at the given position is only adjusted if the corresponding value of ```RDM``` is above the dynamic threshold
