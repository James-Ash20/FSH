1. Download the directory “test_example_ISCE_insarApp” from the [link](https://drive.google.com/file/d/1za9J2Jt3lKFPS7NZW7gGISeXJhT5EdDH/view?usp=sharing).

2. Under test_example_ISCE_insarApp/, you will find the flag_file (`flagfile.txt`), link_file (`linkfile.txt`), ref_file (`Howland_LVIS_NaN.tif`), mask_file (`Maine_NLCD2011_nonwildland.tif`). All of the associated files for three ALOS PALSAR HV-pol InSAR coherence scenes are grouped by their ALOS (`f$frame_o$orbit`) and their acquisition dates (under the subfolder `int_$date1_$date2`). For each scene, there are five associated files outputted by ISCE: `insarProc.xml`, `resampOnlyImage.amp.geo`, `resampOnlyImage.amp.geo.xml`, `topophase.cor.geo`, `topophase.cor.geo.xml`. This page serves as the instructions for running the FSH software over this test example directory. Finally, an image `ISCE.png` shows the final output of 3-scene mosaic map (GeoTiff format) overlaid on Google Earth in a QGIS window.

***Note: all of the ALOS images files have already been margin-cropped and geocoded in the pre-processing by ISCE (Step 2 & 3 of the general workflow in Section II on the GitHub webpage, i.e. "README.md" file).***

3. Run the 1-command FSH auto-inversion (Step 4 of the general workflow in Section II on the GitHub webpage, i.e. "README.md" file)
              
       python <full_path_to_directory_of_scripts>forest_stand_height.py 3 2 2 5 \
       "linkfile.txt" \
       "flagfile.txt" \
       "Howland_LVIS_NaN.tif" \
       "Maine_NLCD2011_nonwildland.tif" \
       ".../test_example_ISCE_insarApp/" \
       "gif json kml mat tif" \
       --flag_diff=1 --flag_error=1  --flag_proc=1



4. Run the 1-command FSH mosaicking (Step 5 of the general workflow in Section II on the GitHub webpage, i.e. "README.md" file)

       python <full_path_to_directory_of_scripts>create_mosaic.py "<full_path_to_directory_of_test_example>test_example_ISCE_insarApp/" "3sc_mosaic.tif" 

5. Open the final output `3sc_mosaic.tif` in QGIS.
