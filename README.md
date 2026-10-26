# Cross-domain Remaining Useful Life (RUL) prediction on NASA C-MAPSS turbofan engines

Author: Oluwapelumi Fagbayide

## Problem

Models trained on the C-MAPSS FD001 subset lose accuracy when applied to FD002, FD003 and FD004, which have different operating conditions and fault modes. This project studies how well LSTM and CNN-LSTM regressors transfer across these subsets and whether a lightweight adaptation pipeline helps.

## Approach

- Targets: piecewise linear RUL with a cap of 125 cycles.
- Inputs: sliding windows of 30 cycles over 14 sensor channels.
- Models: LSTM versus CNN-LSTM.
- Four-stage adaptation pipeline:
  1. Operating condition normalisation using K-Means.
  2. CORAL covariance alignment.
  3. Baseline (initial wear) correction.
  4. EWMA smoothing of predictions.

## Results

Saved numbers from the notebook (RMSE / PHM score, lower is better for both):

| Model    | FD001 (RMSE / PHM) | FD002 (RMSE / PHM) | FD003 (RMSE / PHM) | FD004 (RMSE / PHM) |
|----------|--------------------|--------------------|--------------------|--------------------|
| CNN-LSTM | 14.27 / 430.4      | 24.57 / 3172       | 33.06 / 3901       | 46.64 / 27008      |
| LSTM     | 13.44 / 366.1      | 23.75 / 2838.7     | 33.78 / 3699.3     | 33.95 / 10458      |

## Status

This is current work in progress. Further notebooks (a dedicated LSTM run, a TCN model and an ablation study) will be added.

## How to run

1. Download the NASA C-MAPSS data from the NASA prognostics data repository.
2. Place `train_FD00x.txt`, `test_FD00x.txt` and `RUL_FD00x.txt` (x = 1 to 4) next to the notebook.
3. Use Python 3 with TensorFlow, scikit-learn, pandas, matplotlib and openpyxl installed.
4. Open and run `notebooks/01_cnn_lstm_and_lstm_comparison.ipynb`.
