# DamageSurvey

<details>
<summary>Background</summary>

In 2022, the Federal Emergency Management Agency (FEMA) responded to over 100 officially declared disasters within the U.S. and it's territories.  One of the most time-sensitive post-disaster activities is the Preliminary Damage Assessment, to determine the level and extent of damage before restoration activities can begin.  In theory, if some or all of this process could be automated, the faster PDA's are performed, the quicker individuals can obtain insurance reimbursement or disaster management officials are able to accurately prioritize restoration activities.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://www.dhs.gov/sites/default/files/images/PLCY/19_0703_plcy_strat-plan_goal-5-1.jpg">
  <source media="(prefers-color-scheme: light)" srcset="https://www.dhs.gov/sites/default/files/images/PLCY/19_0703_plcy_strat-plan_goal-5-1.jpg">
  <img alt="Arial view of a coastline with badly damaged houses" src="https://www.dhs.gov/sites/default/files/images/PLCY/19_0703_plcy_strat-plan_goal-5-1.jpg">
</picture>
Photo Source: DHS.gov
</details>

<details>
<summary>Project Description</summary>

This project is a proof-of-principle demonstration of whether the resnet-18 model for image recognition shows promise to differentiate between smoke, fire, damage, flooded and undamaged structures.
</details>

<details>
<summary>Instructions</summary>

### Download and unpack the data
cd ./jetson-inference/python/training/classification

wget https://www.dropbox.com/s/5d03a2n4klgkmfx/DamageSurvey_Data.tar?dl=0 -O DamageSurvey.tar

tar -xvf DamageSurvey.tar

### Train the model
python3 train.py --model-dir=models/DamageSurvey data/DamageSurvey

### Generate a model called resnet18.onnx
python3 onnx_export.py --model-dir=models/DamageSurvey

### Create a data directory to capture outputs
rm -r data/DamageSurvey/test/output

mkdir data/DamageSurvey/test/output

### Process a single test file
imagenet --model=models/DamageSurvey/resnet18.onnx 
         --input_blob=input_0 --output_blob=output_0 
         --labels=data/DamageSurvey/labels.txt 
           data/DamageSurvey/test/001.jpg 
           data/DamageSurvey/test/output/output_001.jpg

### Process all test files
imagenet --model=models/DamageSurvey/resnet18.onnx 
         --input_blob=input_0 --output_blob=output_0 
         --labels=data/DamageSurvey/labels.txt 
           data/DamageSurvey/test 
           data/DamageSurvey/test/output
</details>

<details>
<summary>Downloads</summary>

### Video
[Click here to download](https://www.dropbox.com/s/mdml3lra4qmr39t/DamageSurvey.mov?dl=0)

### Data
[Click here to download](https://www.dropbox.com/s/5d03a2n4klgkmfx/DamageSurvey_Data.tar?dl=0)

### Model
[Click here to download](https://www.dropbox.com/s/utz4msu0s8e5n5k/DamageSurvey_Model.tar?dl=0)

### "Getting Started with AI on Jetson Nano" Certificate
[Click here to download](https://www.dropbox.com/s/q1ldws8e1aznflo/NVIDIA%20Certificate%20%28Getting%20Started%20on%20Jetson%20Nano%29.pdf?dl=0)

### Reflash instructions for a dead NVIDIA Jetson Nano 2GB Developer Kit card
[Click here to download](https://www.dropbox.com/s/awcbqkyni0gvbbt/Step-by-Step%20Instructions%20to%20Flash%20a%20Dead%20Jetson%20Nano%20Board.txt?dl=0)
</details>

@NVIDIA/Training  Thanks to the Jetson Nano training and support teams for putting the material together to jumpstart projects! 


