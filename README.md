# **SAIVT Building Monitoring Database**

## **Overview**
The SAIVT-BuildingMonitoring database contains footage from 12 cameras capturing a single work day at a busy university campus building. A portion of the database has been annotated for crowd counting and pedestrian throughput estimation, and is freely available for download. Contact Dr Simon Denman (s dot denman at qut dot edu dot au) for more information

## **Licensing** 
The SAIVT-BuildingMonitoring database is © 2015 QUT, and is licensed under the [Creative Commons Attribution-ShareAlike 3.0 Australia License] (http://creativecommons.org/licenses/by-sa/3.0/).

## **Attribution**
To attribute this database, use the citation provided on our publication at [eprints] (http://eprints.qut.edu.au/85118/): 

> S. Denman, C. Fookes, D. Ryan, & S. Sridharan (2015) Large 
> scale monitoring of crowds and building utilisation: A new 
> database and distributed approach. In 12th IEEE International 
> Conference on Advanced Video and Signal Based Surveillance, 
> 25-28 August 2015, Karlsruhe, Germany.

## **Acknowledgement in publications**
In addition to citing our paper, we kindly request that the following text be included in an acknowledgements section at the end of your publications:

> 'We would like to thank the SAIVT Research Labs at Queensland University of Technology (QUT) for freely supplying us with the SAIVT-BuildingMonitoring database for our research'.

## **Installing the SAIVT-BuildingMonitoring Database**
Download and unzip the following archives:
- [Annotated Data (8 GB)](https://Q0102-RO:Vieyae3G@q0102-webdav.qcloud.qcif.edu.au/SAIVT-BuildingMonitoring-AnnotatedData.tar.gz)
- [Full Sequences (29 GB)](https://Q0102-RO:Vieyae3G@q0102-webdav.qcloud.qcif.edu.au/SAIVT-BuildingMonitoring-FullSequences.tar.gz)
- [Pre-processed Motion Segmentation (47 GB)](https://Q0102-RO:Vieyae3G@q0102-webdav.qcloud.qcif.edu.au/SAIVT-BuildingMonitoring-MotionSegmentation.tar.gz)

At this point, you should have the following data structure and the SAIVT-BuildingMonitoring database is installed:
```
SAIVT-BuildingMonitoring 
+-- AnnotatedData 
  +-- P_Lev_4_Entry_Way_ip_107 
    +-- Frames 
      +-- Entry_ip107_00000.png 
      +-- Entry_ip107_00001.png 
      +-- ... 
    +-- GroundTruth.xml 
    +-- P_Lev_4_Entry_Way_ip_107-20140730-090000.avi 
    +-- perspectivemap.xml 
    +-- ROI.xml 

  +-- P_Lev_4_external_419_ip_52 
    +-- ... 

  +-- P_Lev_4_External_Lift_foyer_ip_70 
    +-- Frames 
      +-- Entry_ip107_00000.png 
      +-- Entry_ip107_00001.png 
      +-- ... 
    +-- GroundTruth.xml 
    +-- P_Lev_4_External_Lift_foyer_ip_70-20140730-090000.avi 
    +-- perspectivemap.xml 
    +-- ROI.xml 
    +-- VG-GroundTruth.xml 
    +-- VG-ROI.xml 

  +-- ... 

+-- Calibration 
  +-- Lev4Entry_ip107.xml 
  +-- Lev4Ext_ip51.xml 
  +-- ... 

+-- FullSequences 
  +-- P_Lev_4_Entry_Way_ip_107-20140730-090000.avi 
  +-- P_Lev_4_external_419_ip_52-20140730-090000.avi 
  +-- ... 

+-- MotionSegmentation 
  +-- Lev4Entry_ip107.avi 
  +-- Lev4Entry_ip107-Full.avi 
  +-- Lev4Ext_ip51.avi 
  +-- Lev4Ext_ip51-Full.avi 
  +-- ... 

+-- Denman 2015 - Large scale monitoring of crowds and building utilisation.pdf 
+-- LICENSE.txt 
+-- README.txt
```

Data is organised into two sections, AnnotatedData and FullSequences. Additional data that may be of use is provided in Calibration and MotionSegmentation.
AnnotatedData contains the two hour sections that have been annotated (from 11am to 1pm), alongside the ground truth and any other data generated during the annotation process. Each camera has a directory, the contents of which depends on what the camera has been annotated for.
All cameras will have:
- a video file, such as "P_Lev_4_Entry_Way_ip_107-20140730-090000.avi", which is the 2 hour video from 11am to 1pm
- a "Frames" directory, that has 120 frames taken at minute intervals from the sequence. There are the frames that have been annotated for crowd counting. Even if the camera has not been annotated for crowd counting (i.e. P_Lev_4_Main_Entry_ip_54), this directory is included.

The following files exist for crowd counting cameras:
- "GroundTruth.xml", which contains the ground truth in the following format: 
```
<qutcrowd-count-gt interval-scale="1800"> 
<frame id="0"> 
<ped x="175" y="112" /> 
</frame> 
<frame id="1"> 
<ped x="149" y="97" /> 
<ped x="187" y="97" /> 
</frame> 
.... 
<qutcrowd-count-gt> 
```
The file contains a list of annotated frames, and the location of the approximate centre of mass of any people within the frame. The "interval-scale" attribute indicates the distance between the annotated frames in the original video.
- "perspectivemap.xml", a file that defines the perspective map used to correct for perspective distortion. Parameters for a bilinear perspective map are included along with the original annotations that were used to generate the map.
- "ROI.xml", which defines the region of interest as follows:
```
<ROI num-points="8" image-width="768" image-height="576"> 
<point x="0" y="152" /< 
<point x="239" y="117" /> 
<point x="341" y="107" /> 
<point x="428" y="110" /> 
<point x="519" y="116" /> 
<point x="763" y="159" /> 
<point x="760" y="575" /> 
<point x="0" y="575" /> 
</ROI> 
```
This defines a polygon within the image that is used for crowd counting. Only people within this region are annotated.

For cameras that have been annotated with a virtual gate, the following additional files are present:
- VG-GroundTruth.xml, which contains ground truth in the following format: 
```
<qutcrowd-flow-gt both-directions="0"> 
<ROI num-points="4" image-width="856" image-height="480"> 
<point x="622" y="91" /> 
<point x="837" y="242" /> 
<point x="837" y="282" /> 
<point x="622" y="131" /> 
</ROI> 
<doi>0<doi> 
<ped frame="1889" x="662" y="144" direction="1" /> 
<ped frame="3615" x="667" y="137" direction="0" /> 
<ped frame="4851" x="770" y="212" direction="1" /> 
<ped frame="5153" x="659" y="129" direction="1" /> 
<ped frame="6317" x="655" y="147" direction="1" /> 
... 
</qutcrowd-flow-gt> 
```
The ROI is repeated within the ground truth, and a direction of interest (the ```<doi>``` tag) is also included, which indicates the primary direction for the gait (i.e. the direction that denotes a positive count. Each pedestrian crossing is represented by a ```<ped>``` tag, which contains the approximate frame the crossing occurred in (when the centre of mass was at the centre of the gait region), the x and y location of the centre of mass of the person during the crossing, and the direction (0 being the primary direction, 1 being the secondary).
- VG-ROI.xml, which contains the region of interest for the virtual gate

The Calibration directory contains camera calibration for the cameras (with the exception of ip107, which has an uneven ground plane and is thus difficult to calibrate). All calibration is done using Tsai's method.

FullSequences contains the full sequences (9am - 5pm) for each of the cameras.

MotionSegmentation contains motion segmentation videos for all clips. Segmentation videos for both the full sequences and the 2 hour annotated segments are provided. Motion segmentation is done using the ViBE algorithm. Motion videos for the entire sequence have "Full" in the file name before the extension (i.e. Lev4Entry_ip107-Full.avi).

Further information on the SAIVT-BuildingMonitoring database in our paper: 

> S. Denman, C. Fookes, D. Ryan, & S. Sridharan (2015) Large 
> scale monitoring of crowds and building utilisation: A new 
> database and distributed approach. In 12th IEEE International 
> Conference on Advanced Video and Signal Based Surveillance, 
> 25-28 August 2015, Karlsruhe, Germany.

This paper is also available alongside this document in the file: 'Denman 2015 - Large scale monitoring of crowds and building utilisation.pdf'.