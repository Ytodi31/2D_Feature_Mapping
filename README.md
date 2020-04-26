#  2D Feature Tracking
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview
The idea of this project is to benchmark the various available key point detectors and descriptors. The performance of all the combinations of detector + descriptor pairs is provided in the results section.

<img src="images/keypoints.png" width="820" height="248" />

.

## Dependencies
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)

* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros

* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)

## Pipeline
  * **Data Buffer** : A ring buffer was created to manage memory in case the number of images to be processes is high. This was done by removing the oldest image and keeping the youngest image
  * **Key-point detection** : Various detectors were implemented to detect key points. The detectors implemented were HARRIS, FAST, BRISK, ORB, AKAZE, SIFT and can be selected by user input. Separate functions were implemented for each detector and called based on user-input.
  * **Key-point removal** : Since the region of interest is the tailgate of the preceding vehicle, key points present in a bounding box is extracted.
  * **Key-point Descriptor** : Various descriptor methods were implemented to extract a descriptor. The descriptors implemented were BRIEF, FREAK, SIFT, AKAZE, ORB, BRISK. Based on user input, an object is created and a common extractor is used to get the descriptor.
  * **Descriptor Matching** : Descriptor matching is available using Brute Force and FLANN method along with nearest neighbor and k-nearest neighbor selection. These can be set as strings in the main function.
  * **Descriptor Distance Ratio** : A comparison is made between the best and second best match between source and reference image features. Bad matches are removed by comparing the descriptor distance with a threshold of 0.8. Good matches which are within the threshold are returned.
  * **Performance Evaluation** :
1. The number of keypoints were counted for each detector and was stored in a vector for 10 images. and summed using the accumulate function.
2. The number of matches were counted for each detector-descriptor pair and was stored in a vector for 10 images. and summed using the accumulate function.
3. The efficiency of each pair was calculated by taking a ratio of matches and time taken for detection and extraction.

## Basic and Run

1. Clone this repo.
`git clone https://github.com/Ytodi31/2D_Feature_Mapping `
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.

### User input
The program will ask for the key-point detector and descriptor you wish to use.

Detector options : SHITOMASI, HARRIS, FAST, BRISK, ORB, AKAZE, SIFT \
Descriptor options : BRIEF, ORB, GREAK, AKAZE, SIFT, BRISK

## Results
The top 3 detector-descriptors are :
1. FAST + ORB
2. FAST + BRIEF
3. FAST + BRISK

|    | DETECTOR  | DESCRIPTOR | MATCHES | TIME \(MS\) | MATCHES/MS   |
|----|-----------|------------|---------|-------------|--------------|
| 1  | FAST      | ORB        | 4049    | 0\.032837   | 123306\.0267 |
| 2  | FAST      | BRIEF      | 4552    | 0\.0448405  | 101515\.3711 |
| 3  | FAST      | BRISK      | 3077    | 0\.108974   | 28236\.09301 |
| 4  | SHITOMASI | BRIEF      | 3100    | 0\.199145   | 15566\.54699 |
| 5  | SHITOMASI | ORB        | 2798    | 0\.185312   | 15098\.8603  |
| 6  | ORB       | BRIEF      | 1396    | 0\.092814   | 15040\.83436 |
| 7  | BRISK     | BRIEF      | 6979    | 0\.474268   | 14715\.30864 |
| 8  | ORB       | BRISK      | 1314    | 0\.1121     | 11721\.67707 |
| 9  | FAST      | SIFT       | 5989    | 0\.530568   | 11287\.90278 |
| 10 | ORB       | ORB        | 1288    | 0\.127863   | 10073\.28156 |
| 11 | SHITOMASI | SIFT       | 3344    | 0\.355983   | 9393\.707003 |
| 12 | SHITOMASI | BRISK      | 2220    | 0\.252312   | 8798\.630267 |
| 13 | BRISK     | ORB        | 4234    | 0\.484699   | 8735\.318208 |
| 14 | BRISK     | BRISK      | 4809    | 0\.573512   | 8385\.177642 |
| 15 | FAST      | FREAK      | 2941    | 0\.483746   | 6079\.636834 |
| 16 | BRISK     | FREAK      | 4520    | 9\.27E\-01  | 4\.88E\+03   |
| 17 | AKAZE     | BRIEF      | 3939    | 0\.920139   | 4280\.874955 |
| 18 | BRISK     | SIFT       | 7237    | 1\.84853    | 3915\.002732 |
| 19 | SHITOMASI | FREAK      | 2105    | 0\.574998   | 3660\.882299 |
| 20 | AKAZE     | BRISK      | 3165    | 0\.966529   | 3274\.60428  |
| 21 | AKAZE     | SIFT       | 3777    | 1\.16517    | 3241\.587065 |
| 22 | AKAZE     | ORB        | 3007    | 0\.94207    | 3191\.907183 |
| 23 | AKAZE     | FREAK      | 3092    | 1\.24091    | 2491\.719786 |
| 24 | AKAZE     | AKAZE      | 3382    | 1\.43942    | 2349\.557461 |
| 25 | SIFT      | BRIEF      | 3136    | 1\.34188    | 2337\.019704 |
| 26 | SIFT      | BRISK      | 2478    | 1\.38702    | 1786\.564001 |
| 27 | ORB       | SIFT       | 1615    | 0\.932923   | 1731\.118217 |
| 28 | HARRIS    | ORB        | 252     | 0\.169518   | 1486\.567798 |
| 29 | HARRIS    | BRIEF      | 250     | 0\.169781   | 1472\.485143 |
| 30 | SIFT      | FREAK      | 2371    | 1\.73277    | 1368\.329322 |
| 31 | SIFT      | SIFT       | 2595    | 1\.9932     | 1301\.92655  |
| 32 | ORB       | FREAK      | 604     | 0\.482829   | 1250\.960485 |
| 33 | HARRIS    | BRISK      | 211     | 0\.18473    | 1142\.207546 |
| 34 | HARRIS    | SIFT       | 263     | 0\.269673   | 975\.2552165 |
| 35 | HARRIS    | FREAK      | 195     | 0\.52878    | 368\.7734029 |
