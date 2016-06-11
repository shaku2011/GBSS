# Gray-matter Based Spatial Statistics (NODDI-GBSS)
[![License](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/by-nc.svg)](LICENSE)
##Introduction
	 Gray matter-based spatial statistics (NODDI-GBSS) is a pipeline to perform voxel-wise statistical analysis on gray matter microstructure. 
##<i>gbss_1_reg.sh</i>	
	Gray matter fraction maps are estimated in the native diffusion space by subtracting CSF fraction (fCSF maps from NODDI) and white matter fraction (estimated by two-tissue class segmentation of FA images using Atropos) from 1 in each voxel. To increase tissue contrasts and enhance between-subject registration steps, partial volume estimation maps for each tissue class are multiplied by their corresponding contrast (0 for CSF, 1 for gray matter, and 2 for white matter) and summed together to generate images with similar contrast to T1-weighted images. The resulting images are then used to build a study-specific template using the <i>buildtemplateparallel.sh</i> script in the Advanced Normalization Tools (ANTs)32, 33. Gray matter fraction, ODI, and NDI images were warped to the template space using the warp fields estimated during the previous step (gbss_1_reg.sh script; Figure 1). To enhance between-subject alignment of gray matter voxels, GBSS adopts the tract-based spatial statistics (TBSS) algorithm34. The average gray matter fraction map was skeletonized and for each individual, diffusion metrics (i.e., ODI and NDI) and gray matter fraction were projected from local voxels with greatest gray matter fraction in the template space onto the skeleton. The final skeleton was generated by keeping only voxels with a gray matter fraction greater than 0.65 in more than 75% of the subjects (gbss_2_skell.sh script; Figure 1). The remaining voxels on the subjects’ skeletons with non-satisfactory gray matter fraction (below 0.65) were filled with the average of the surrounding satisfactory voxels on the skeleton (e.g. gray matter fraction>0.65) weighted by their closeness with a Gaussian kernel (σ=2 mm; gbss_3_fill.sh script). The GBSS pipeline scripts are freely available online.
