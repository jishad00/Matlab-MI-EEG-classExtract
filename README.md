# Matlab-MI-EEG
Matlab code for preprocessing EEG data.
We will use the public motor imagery dataset - BCI competition IV dataset IIa.
You can download it from http://www.bnci-horizon-2020.eu/database/data-sets.
The code class_extract.mat will load the data, bandpass filter it between 8 Hz and 30 Hz and then seperate out the epochs specific to each class asper the label.
