# Generating interferograms to be used as input to FSH:

## There are three steps: 

1. Run ROI_PAC or ISCE (see parameter notes below)
2. Crop the ROI_PAC/ISCE output to eliminate the image margins (run standalone CROP_ROIPAC.py or CROP_ISCE.py)
3. Geocode the ROI_PAC/ISCE output

In step 1, users may find online support and guidance running ROI_PAC (the command "process_2pass.pl"). Since it only supports ALOS-1 data and has been deprecated, we do not cover the details for running it. Instead, we provide the details along with the scripts for running ISCE, with the precursor being ROI_PAC. ISCE supports JAXA's ALOS-1 and ALOS-2 data and also NASA's future NISAR mission. ISCE's application "insarApp.py" is valid for ISCE v2.0, v2.1 and v2.2, while deprecated for v2.3. "insarApp.py" uses the amplitude cross-correlation (ampcor) to coregister the two radar images. In contrast, starting from v2.2, ISCE started to replace the role of "insarApp.py" with "stripmapApp.py", which uses the radar observing geometry along with dense ampcor + rubbersheeting (to apply the ampcor-determined offsets) for image coregistration. As each method has its own merit, and so far neither is absolutely better than the other, we include both options and leave the quality assessment to the users. Since ISCE v2.2 is the only version of ISCE that supports both "insarApp.py" and "stripmapApp.py", we tested the following scripts with this version only. However, the scripts are meant to work with all versions of ISCE v2+.

### All the ISCE preprocessing scripts can be found under the folder "ISCE_processing_scripts/".

### Below are the steps for using the ISCE applications "insarApp" and "stripmapApp" to process radar data for FSH.

## Setting up ISCE for generating PALSAR interferograms (requires replacing existing ISCE scripts):

### Copy updated applications scripts,
	0) Copy the 7 scripts (CROP_ISCE_insarApp.py, CROP_ISCE_stripmapApp.py, format_insarApp_xml.py, format_stripmapApp_xml.py, MULTILOOK_FILTER_ISCE.py, single_scene_insarApp.py, single_scene_stripmapApp.py) under "ISCE_processing_scripts" to any local folder that is on the environmental variables PATH and PYTHONPATH

### For using ISCE's insarApp, 

	1) Replace ISCE/isce/components/isceobj/InsarProc/runCoherence.py with ISCE_processing_scripts/insarApp_substitute/runCoherence.py
	
### For using ISCE's stripmapApp,

	2) Replace ISCE/isce/components/isceobj/StripmapProc/runCoherence.py with ISCE_processing_scripts/stripmapApp_substitute/runCoherence.py

	3) Replace ISCE/isce/components/isceobj/StripmapProc/runGeocode.py with ISCE_processing_scripts/stripmapApp_substitute/runGeocode.py

	4) Replace ISCE/isce/components/isceobj/StripmapProc/runPreprocessor.py with ISCE_processing_scripts/stripmapApp_substitute/runPreprocessor.py

	5) Replace ISCE/isce/applications/stripmapApp.py with ISCE_processing_scripts/stripmapApp_substitute/stripmapApp.py

## Running ISCE

To run the scripts for actual processing (with ALOS-1 data as an example), we need to put two unzipped ALOS-1 data folders (with the folder name formatted as "ALPSRP*-L1.0") in the same directory, e.g. test_data. For running insarApp, one only needs to type the following command line:
	
	single_scene_insarApp.py -f test_data

and for running stripmapApp, one can type:

	single_scene_stripmapApp.py -f test_data

***Note: some of the parameters in the 7 scripts of 0) are hardcoded for the ALOS data as an example of using the scripts, and needs to be adjusted for ALOS-2 and the future NISAR data.***

***Note: for better use of updated functions and also to be compatible with future ISCE releases, it is thus recommended not to simply replace those ISCE original files in 1-5) but to directly add the newly added lines into the ISCE original files. Those newly added lines start and end with the pattern shown below:***
