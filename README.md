# Controlling-the-Impression-of-Robots-via-GAN-based-GestureGeneration

## Introduction

Official implementation for "Controlling the Impression of Robots via GAN-based GestureGeneration"

## To reproduce
1. Clone the repository
2. Execute 'conda env create -f environment.yml' to create a conda environment
3. Download the dataset from https://www.dropbox.com/sh/j419kp4m8hkt9nd/AAC_pIcS1b_WFBqUp5ofBG1Ia?dl=0
4. Download the extracted speech features https://drive.google.com/drive/folders/1eISYiVAeRunO4CEXD47GxqPw3bmwJ7fr?usp=sharing
5. Create a directory `./data/takekuchi/source` and put downloaded data into three directories `motion/`, `speech/` and `speeche_features/`, separately.

```
.
data
--takekuchi
   --source
      --motion
      --speech
      --speech_features
```

6. Split train, dev, and test, `python datasets/takekuchi_ext/data_processing/prepare_data.py`
7. Preprocess dataset `python datasets/takekuchi_ext/data_processing/create_vector.py`
8. Train model `python main.py wgan takekuchi hparams/defaults.json`
9. Evaluate the model on test set (which was not used during training)
   1. Copy saved model checkpoint path (in `results/log_date/chkpt`) to `Infer: pre_trained` inside `results/defaults.json`
      ```
      "Infer": {
        "pre_trained": "results/log_{date}/chkpt/generator_{timestep}k.pt"
      },
      ```
   2. Execute `python main.py wgan takekuchi hparams/wgan/paper_version.json` to obtain the generated motion in 'synthesized/' and the KDE results.

## Visualization
See https://github.com/wubowen416/unity_gesture_visualizer.

## Contact
For any questions, please contact wu.bowen@irl.sys.es.osaka-u.ac.jp
