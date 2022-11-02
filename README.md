# [DeepPulse: An Uncertainty-aware Deep Neural Network for Heart Rate Estimations from Wrist-worn Photoplethysmography](https://ieeexplore.ieee.org/document/9871813)
<p align="center">
  <img src="https://github.com/danielray54/DeepPulse/blob/main/Resources/Dray23_Scientific_Multi-wavelength_Photoplethysmography_Cardiov_a7e8c3ad-2052-4e3f-9316-41fcb32237ef.png" data-canonical-src="https://github.com/danielray54/DeepPulse/blob/main/Resources/Dray23_Scientific_Multi-wavelength_Photoplethysmography_Cardiov_a7e8c3ad-2052-4e3f-9316-41fcb32237ef.png" width="400" height="400" />
</p>

>2022 44th Annual International Conference of the IEEE Engineering in Medicine & Biology Society (EMBC)

## Datasets:
1. IEEE Train & Test
  - [Z. Zhang, Z. Pi, B. Liu, TROIKA: A general framework for heart rate monitoring using wrist-type photoplethysmographic signals during intensive physical exercise, IEEE Transactions on Biomedical Engineering, vol. 62, no. 2, pp. 522-531, February 2015, DOI: 10.1109/TBME.2014.2359372](https://ieeexplore.ieee.org/document/6905737)
  - [Original Source](https://zenodo.org/record/3902710#.Y2ErK3YUVD8)
  - [IEEE Test Preprocessed](https://drive.google.com/file/d/174KyqOiuhl3Prsrn29KgeMmIJVgYLSQK/view?usp=share_link)
  - [IEEE Train Preprocessed](https://drive.google.com/file/d/1PSciZgnXPlsYBMzR1Oj4TjcTk_LjL7TQ/view?usp=share_link)
2. BAMI
  - [H. Lee, H. Chung, and J. Lee. "Motion artifact cancellation in wearable photoplethysmography using gyroscope." IEEE Sensors Journal 19.3 (2018): 1166-1175.](https://ieeexplore.ieee.org/abstract/document/8529266)
  - [Original Source](https://github.com/hooseok/BAMI1)
  - [BAMI Preprocessed](https://drive.google.com/file/d/1g5gqh6vekEdi3ZT21Cdu_1fkfNjBeUOA/view?usp=share_link)
3. Dalia
  - [A. Reiss, I. Indlekofer, P. Schmidt, and K. Van Laerhoven, “Deep PPG: Large-Scale Heart Rate Estimation with Convolutional Neural Networks,” Sensors, vol. 19, no. 14, p. 3079, Jul. 2019, doi: 10.3390/s19143079](http://dx.doi.org/10.3390/s19143079)
  - [Original Source](https://archive.ics.uci.edu/ml/datasets/PPG-DaLiA)
  - [Dalia Preprocessed](https://drive.google.com/file/d/12DnrzMCV_otfU5_YUbedwRRcIyiHShIm/view?usp=share_link)

## Preprocessing:
  1. 2nd order Butterworth band-pass filter with cutoff frequencies of 0.5 Hz - 4.5 Hz
  2. Sliding window (8 second window 2 second shift)
  3. Resample to 64Hz
  4. Z-normalisation

## Cross-validation Scheme:
  - Leave one subject out

## Architecture:
  - Sensing modality fusion convoulutional architecture with bidirectional LSTM units.
  - Output is a normal distribution with $\mu$ and $\sigma$.
  - Samples from predictive distribution using MC dropout
  	<p align="center">
		  <img src="https://github.com/danielray54/DeepPulse/blob/main/Resources/arch-1.png" data-canonical-src="https://github.com/danielray54/DeepPulse/blob/main/Resources/arch-1.png" width="400" height="550" />
	</p>
    
## Results
- All results are from unseen data, i.e. the test sets of each fold. 
- To get a deeper look at model performance, view the png files in each experiment folder. There is a training and calibration image for each fold plus an overall image with lots of graphs :)

| Dataset | Mean Abs Err | Mean Max Abs Err | Miscalibration Area | Sharpness | Bias | Variance |
|---------|-----|--------|---------------------|-----------|-----------|-----------|
| IEEE    | 1.160 ± 0.475 BPM | 9.994 ± 9.943 BPM | 0.177 ± 0.067 | 3.199 ± 0.469 | 319.629 ± 212.662 | 316.208 ±	213.480 |
| BAMI    | 1.652 ± 0.402 BPM | 15.963 ± 9.040 BPM | 0.056 ± 0.034 | 2.389 ± 0.259 | 356.309 ± 194.847 | 354.717 ± 192.778 |
| DaLiA   |     |        |                     |           |  |  |
					
## Comments:
- If you see anything wrong, please get in contact with me! I appreciate any feedback :)
