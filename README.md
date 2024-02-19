# Palmprint_Authentication

Biometric Authentication can be various types. One of them is palmprint authentication.


## Dataset:
Though there are multiple available datasets on the internet (e.g. PolyU multi-spectral palmprint database , PolyU 2D+3D palmprint database etc. ) But I found out a clear photograph working more accurate in this model . As the FAR and FRR of ROI has decreased with a clear picture. 


So,to test and train this model I created a dataset of 1050 palm images (both palm) , where a total of 26 people participated voluntarily in diffrent sessions. Since those data are sensitive I've not uploaded the dataset in the github repository.
I have uploaded here a sample picture for the reference.

![user_5_16](https://github.com/sinnie-pi/Palmprint_Authentication/assets/82073783/b8012d66-1852-40dc-8b48-929c704dfc98)


Note: All of the picture should contain palm center, principle lines, flexor liness, datum points, wrinkles , ridges and may contain fingers. Also all the picture should be taken in dark background, where anyother object is not visible.


## Model:
Region of Interest (ROI) Segmentation:

The acquired images often contain redundant information such as fingers and background. Palmprint ROI refers to the palm center that contains three flexor lines. 
Since the size and shape of every hand is generally different from each other , there may exists a rotation between them, it is necessary to correct the scale and angle of the palmprint image before ROI segmentation.

Scale Correction:

The key point lying in the original image with a size of 𝒘×𝒉 is denoted as 𝑷_𝒊 (𝒙_𝒊,𝒚_𝒊 )   [𝒊=𝟏,𝟐,𝟑] . The corresponding position for testing image is a size of 𝒘^′×𝒉^′  is denoted as 𝑷_𝒊^′ (𝒙_𝒊^′,𝒚_𝒊^′ )   [𝒊=𝟏,𝟐,𝟑] . Then, the transformation can be defined as
{█(𝑥_𝑖^′=𝑥_𝑖×(𝑤^′/𝑤)@𝑦_𝑖^′=𝑦_𝑖×(ℎ^′/ℎ) )┤

![image](https://github.com/sinnie-pi/Palmprint_Authentication/assets/82073783/b05f1c8a-5d90-4d31-a4c1-40b1f9a6f011)


Rotation Correction:

The purpose of the rotation is to place 𝑷_𝟏 and 𝑷_𝟑 on a horizontal line to facilitate ROI segmentation. The calculation of the rotation angle is shown as follows:

𝑎=  tan^(−1)⁡(((𝑦_3^′−𝑦_1^′))/((𝑥_3^′−𝑥_1^′)))

where (𝒙_𝟏^′,𝒚_𝟏^′) and (𝒙_𝟑^′,𝒚_𝟑^′) are the coordinates of  𝑷_𝟏^′   and  𝑷_𝟑^′, respectively. The corresponding coordinates after rotation are denoted as 𝑷_𝒊^′′ (𝒙_𝒊^′′,𝒚_𝒊^′′ )   [𝒊=𝟏,𝟐,𝟑]  . We define the rotation transformation as follows:

{█(𝑥_𝑖^′′=[(𝑥_1^′−𝑤^′/2)×cos⁡(𝑎/180×𝜋)+(𝑦_1^′−ℎ^′/2)×sin⁡(𝑎/180×𝜋)+𝑤^′/2]@𝑦_𝑖^′′=[−1×(𝑥_1^′−𝑤^′/2)×sin⁡(𝑎/180×𝜋)+(𝑦_1^′−ℎ^′/2)×cos⁡(𝑎/180×𝜋)+ℎ^′/2] )┤

![image](https://github.com/sinnie-pi/Palmprint_Authentication/assets/82073783/19a957a4-65b2-471a-9651-8b43a33bd6fd)

Where [ ] reserves the integer value, while the line  𝑷_𝟏^′′  𝑷_𝟑^′′   is set as the x-axis, and its vertical line is set as the y-axis. Then, the coordinate system is established in the palmprint image. The length of  𝑷_𝟏^′′  𝑷_𝟑^′′   is denoted as 𝒅 . Moving it down alongside the y-axis by 𝒅/𝟑 , a square is built up with the side length of 𝒅

![image](https://github.com/sinnie-pi/Palmprint_Authentication/assets/82073783/6cb657cb-3c4c-40f2-a70e-866fc90e6cb3)







