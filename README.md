# 【CV_hw4】Feature Extraction 

## Outline
* [Goal](#Goal)
* [A sequence of moving-forward images](#A-sequence-of-moving-forward-images)
* [Feature extraction and matching](#Feature-extraction-and-matching) 
  * [Implement different feature extrators](#Implement-different-feature-extrators)
  * [Result](#Result)
* [Image alignment and infinite zooming effect](#Image-alignment-and-infinite-zooming-effect)
* [Reference](#Reference)

## Goal
  在清大校園內以不同視角拍攝同一個場景的兩張照片。用不同的方法對兩張圖片做特徵提取，並將其結果進行比較，並合成出一張無限縮放效果的動圖。
  
## A sequence of moving-forward images
我們選取了台達館的陽台，從較高樓層向下到較低樓層向下來進行拍攝。
希望通過infinite zoom的一些方法可以給人帶來一種不斷下墜的感覺的圖片。

| Where | Images  |
| :--------: | :--------: | :------: |:------: |
| 台達館陽台(上)    | ![](https://i.imgur.com/EnJIRmL.jpg)| 
|台達館陽台(下)|![](https://i.imgur.com/G1zNR93.jpg)|


## Feature extraction and matching

**ORB ( ORiented Brief )**

ORB結合FAST（Features from Accelerated Segment Test）和BRIEF（Binary Robust Independent Elementary Features）的方法，並在此基礎上加以改進，提高準確度和速度。

 Steps：
1.  通過FAST的方法來找特征點：
   選取圖像中的某一個像素點p，設定threshold value `t`，將p與它周圍的`N`個像素點相比較，當兩點的gray scale value大於`t`則認為兩點不相同，p點不同於周圍大部分的點則認為p點為特征點。
2. 通過Intensity Centroid的方法來推測角點方向<br>
   ![](https://i.imgur.com/KLXXNWe.png)<br>
   *<p align="center">The moments of a patch</p>*<br>
![](https://i.imgur.com/yx0vUDs.png)<br>
*<p align="center">Find the centroid</p>*<br>
![](https://i.imgur.com/pYqF5DY.png)<br>
*<p align="center">The orientation of the patch</p>*<br>
3. 旋轉相關BRIEF來更好的描述特征<br>
![](https://i.imgur.com/xunPFqv.png)<br>
*<p align="center">The definition of a smoothed image patch's binary test</p>*<br>
![](https://i.imgur.com/KMOg9OP.png)<br>
*<p align="center">A vector of n binary tests ( p(x)：the intensity of p at a point x )</p>*<br>
![](https://i.imgur.com/Beev6o3.png)
*<p align="center">The steered BRIEF operator</p>*<br>

### Implement different feature extrators
* SIFT ( Scale-Invariant Feature Transform )
* SURF ( Speeded Up Robust Features )



### Result

| Image | Feature matching | 
| :--------: | :--------: | 
|Original| ![](https://i.imgur.com/cLhcpEr.jpg)  |
|  ORB   | ![](https://i.imgur.com/dR0HjOx.jpg)  | 
|  SIFT  | ![](https://i.imgur.com/MAsfWwP.jpg)  | 
|  SURF  | ![](https://i.imgur.com/fh589qM.jpg)  |


## Image alignment and infinite zooming effect

![Alt Text](https://media.giphy.com/media/KbSZcqC434Dd1imFYf/giphy.gif)<br>
我們用台達一樓木板凳做infinite zoom。理想上木板凳上面木條的接縫可以帶來很好的視覺效果，但是接起來後會有很明顯的邊界。


## Reference
[1] Ethan Rublee, Vincent Rabaud, Kurt Konolige, Gary Bradski, 'ORB: an efficient alternative to SIFT or SURF', IEEE, 6-13 Nov. 2011.