# DamageSurvey

<details>
<summary>Background</summary>

In 2022, the Federal Emergency Management Agency (FEMA) responded to over 100 officially declared disasters within the U.S. and it's territories.  One of the most time-consuming post-disaster activities is the Preliminary Damage Assessment, to determine the level and extent of damage before restoration activities can begin.  In theory, if some or all of this process could be automated, the faster PDA's are performed, the quicker individuals can obtain insurance reimbursement or disaster management officials are able to accurately prioritize restoration activities.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://www.dhs.gov/sites/default/files/images/PLCY/19_0703_plcy_strat-plan_goal-5-1.jpg">
  <source media="(prefers-color-scheme: light)" srcset="https://www.dhs.gov/sites/default/files/images/PLCY/19_0703_plcy_strat-plan_goal-5-1.jpg">
  <img alt="Arial view of a coastline with badly damaged houses" src="https://www.dhs.gov/sites/default/files/images/PLCY/19_0703_plcy_strat-plan_goal-5-1.jpg">
</picture>
Source: DHS.gov
</details>

<details>
<summary>Project Description</summary>

This project is a proof-of-principle demonstration of whether the resnet-18 model for image recognition shows promise to differentiate between smoke, fire, damage, flooded and undamaged structures.
</details>

<details>
<summary>Instructions</summary>

### Train the model
cd ./jetson-inference/python/training/classification
python3 train.py --model-dir=models/DamageSurvey data/DamageSurvey

### Generate a model called resnet18.onnx
python3 onnx_export.py --model-dir=models/DamageSurvey

### Create a data directory to capture outputs
mkdir DamageSurvey/test/output

### Process a single test file
imagenet --model=models/DamageSurvey/resnet18.onnx /
         --input_blob=input_0 --output_blob=output_0 /
         --labels=data/DamageSurvey/labels.txt  /
           data/DamageSurvey/test/01.jpg /
           data/DamageSurvey/test/output/output_01.jpg

### Process all test files
mkdir data/DamageSurvey/test/output

imagenet --model=models/DamageSurvey/resnet18.onnx /
         --input_blob=input_0 --output_blob=output_0 /
         --labels=data/DamageSurvey/labels.txt  /
           data/DamageSurvey/test /
           data/DamageSurvey/test/output
</details>

<details>
<summary>Downloads</summary>

Data
[LIST URL HERE]

Model
[LIST URL HERE]

Getting Started with AI on Jetson Nano Certificate
[LIST URL HERE]
</details>

@NVIDIA/Training  Thanks to the Jetson Nano team, support team and Dusty for putting the material together to jumpstart projects! 


