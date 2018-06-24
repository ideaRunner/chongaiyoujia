# Android app for real-time pet detection.

This project is developed by TensorFlow android example.

### Requisite
  
Android 5.0 (API 21) or higher is required.
  
### Downloading and Running App

- Install Android Studio from [android.com](https://developer.android.com/studio/)

- Clone this repo.

  `git clone https://github.com/ideaRunner/chongaiyoujia.git`

- Download trained neural network model from release.

  ```
  cd assets
  wget https://github.com/ideaRunner/chongaiyoujia/releases/download/1.0.0/yolov2-tiny-pet_40000.pb
  ```
  
- Open android studio, open this project, follow it's instruction to download those libraries you need. (If you are in Chinese, you will need to setup proxy to download from google)

- Build (or Rebuild) project.

- Connect your mobile phone, make sure you have turned on USB debugging mode.

- Click the green run button on Android Studio, find your connected device and click OK.

- Wait one minute and the app could be installed on your phone, you can run it to detect 37 classes pets.

### Pet Breeds

12 cat and 25 dog breeds from Oxford-IIIT [Pet Dataset](http://www.robots.ox.ac.uk/~vgg/data/pets/)

- Cat
  
  ```
  Abyssinian
  Bengal
  Birman
  Bombay
  British_Shorthair
  Egyptian_Mau
  Maine_Coon
  Persian
  Ragdoll
  Russian_Blue
  Siamese
  Sphynx
  ```
- Dog
  
  ```
  american_bulldog
  american_pit_bull_terrier
  basset_hound
  beagle
  boxer
  chihuahua
  english_cocker_spaniel
  english_setter
  german_shorthaired
  great_pyrenees
  havanese
  japanese_chin
  keeshond
  leonberger
  miniature_pinscher
  newfoundland
  pomeranian
  pug
  saint_bernard
  samoyed
  scottish_terrier
  shiba_inu
  staffordshire_bull_terrier
  wheaten_terrier
  yorkshire_terrier
  ```
 
### Generate Your Own App

#### Train YOLO 

For how to train yolo to detect pets or detect your own objects, follow this [page](https://github.com/ideaRunner/yolo-pet).

#### Convert YOLO model to Tensorflow model

- Clone and install [DarkFlow.](https://github.com/thtrieu/darkflow)

- Convert.
  `./flow --model cfg/your-tiny-yolo.cfg --load bin/your-tiny-yolo.weights --savepb --verbalise`

  After running the command two files will appear in the ./built_graph directory:

  ```
  your-tiny-yolo.meta;
  your-tiny-yolo.pb;
  ```
  
#### Implement trained model

- Modify `DetectorActivity`

  `private static final String YOLO_MODEL_FILE = "file:///android_asset/your-yolo-model.pb";`
  `private static final DetectorMode MODE = DetectorMode.YOLO;`
- Modify `TensorFlowYoloDetector`

  Change `NUM_CLASSES` and `LABELS` to what you have trained.
  
#### Run
  After completing the above, you can run and download to your mobile device.

### Quick Troubleshooting

#### Q1: Convert model by darflow AssertionError: 
`AssertionError: expect 63820056 bytes, found 63820060`

Modify the line self.offset = 16 in the ./darkflow/utils/loader.py file and replace with self.offset = 20.

[^_^]:
  Probelm remains:
  NMS algorithm has not been implemented yet. 
  Overfitting due to lack of large dataset and average class.
  No label for human.
  UI design.
