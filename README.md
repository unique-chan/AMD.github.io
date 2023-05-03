# AMD: ARMA3 military target detection on remote sensing imagery
[![Python-3.8](https://img.shields.io/badge/python-3.8-blue?logo=python&logoColor=white)](#)
[![Game-ARMA3](https://img.shields.io/badge/game-ARMA3-red?logo=steam)](#)
[![Platform-Windows10-11](https://img.shields.io/badge/platform-Windows_10_|_11-orange?logo=microsoft)](#)
[![License-GPL-v3](https://img.shields.io/badge/license-GPL_v3-green?logo=gnu)](https://github.com/unique-chan/AMD/blob/main/LICENSE)

### Synthetic data generator for AMD (Beta preview)

[Yechan Kim](github.com/unique-chan) and [Jong Hyun Park](github.com/citizen135)

<p align="center">
    <img alt="Welcome" src="./figs/sample.png" />
</p>

## Updates
- (04/2023) This repo is being updated. Hope you understand and please stay tuned! 👀
- (04/2023) Beta version of our project released (v1.0.0)
  - Support to generate optical remote sensing images
  - Support to provide both oriented and rectangle bbox labels
  - Support to capture the region with multiple viewpoints (`look_angle_min`, `look_angle_max`)
  - Support to adjust weather and time conditions (`weather`, `start_hour`, `end_hour`)
  - Support to refine loose bbox labels (`invalid_bbox_path`)


## Quick start
- We assume that you have already finished setting up ARMA3 by our [tutorial]() in advance.
- For example, run the below command to generate **10** scenes of **sunny** day which covers all camera tilt cases between **-60** and **60** degrees, from **9AM** to **6PM**, on the map named **malden** for **training**:
```bashshell
python main.py  -weather 'sunny' -map_name 'malden' \
                -arma_root_path 'C:/Users/{user_name}/Documents/Arma 3' \
                -save_root_path 'C:/Users/{user_name}/Desktop' \
                -start_hour 9 -end_hour 18 \
                -n_times 10 -mode 'train' \
                -class_path 'classes/CLASSES.csv' \
                -invalid_bbox_path 'classes/INVALID_BBOX.csv' \ 
                -look_angle_min -60 -look_angle_max 60
```
- To create only on-nadir view scenes, set both `look_angle_min` and `look_angle_max` to 0.
- For details, please refer to the [tutorial]() we will provide soon.


## Dataset structure
- The directory structure of our dataset is as follows:
~~~
|—— 📁 {train or test}_{map_name}_{weather}_{start_hour}_{end_hour}_...
	|—— 📁 0000 (scene number)
		|—— 📁 -20  (look angle)
			|—— 🖼️ EO_0000_-20.png  
			|—— 📄 ANNOTATION_0000_-20.csv (including bbox labels)
		|—— 📁 +20 
			|—— 🖼️ ...
	|—— 📁 0001
		|—— 📁 -20
		|—— 📁 ... 
	|—— 📁 0002
		|—— 📁 -20
		|—— 📁 ...
	...
	|—— 📄 meta_..._.csv (including shooting time and weather condition per each scene)
	|—— 📄 log_..._.txt (including error logs)
~~~
- You may need to transform the above folder structure before training your own model.
- You can conveniently check the data using our [image viewer](https://github.com/Dodant/arma-rs-utils).
  - `*.exe` file available for [![MS Windows](https://img.shields.io/badge/Windows-orange?logo=microsoft)](#) users



## Citation
- Paper is coming soon!


## Contribution
- If you find any bugs for further improvements, please feel free to create issues on GitHub!
- All contributions and suggestions are welcome. Of course, stars (🌟) are always welcome.
