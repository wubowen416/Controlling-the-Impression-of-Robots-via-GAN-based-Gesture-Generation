# Controlling-the-Impression-of-Robots-via-GAN-based-GestureGeneration

## To reproduce
1. Clone the repository
2. Download the dataset from https://www.dropbox.com/sh/j419kp4m8hkt9nd/AAC_pIcS1b_WFBqUp5ofBG1Ia?dl=0
3. Download the extracted speech features https://drive.google.com/drive/folders/1eISYiVAeRunO4CEXD47GxqPw3bmwJ7fr?usp=sharing
4. Create a directory `./data/takekuchi/source` and put downloaded data into three directories `motion/`, `speech/` and `speeche_features/`, separately.

```
.
data
--takekuchi
   --source
      --motion
      --speech
      --speech_features
```

5. Split train, dev, and test, `python datasets/takekuchi_ext/data_processing/prepare_data.py`
6. Preprocess dataset `python datasets/takekuchi_ext/data_processing/create_vector.py`
7. Train model `python main.py wgan takekuchi_ext hparams/defaults.json`
8. Evaluate the model on test set (which was not used during training)
   1. Copy saved model checkpoint path (in `results/log_date/chkpt`) to `Infer: pre_trained` inside `results/defaults.json`
      ```
      "Infer": {
        "pre_trained": "results/log_{date}/chkpt/generator_{timestep}k.pt"
      },
      ```

## Visualization
See https://github.com/wubowen416/unity_gesture_visualizer.
