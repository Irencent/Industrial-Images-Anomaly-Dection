## weakness of previous study

High-level features learned from a dataset like the ImageNet doesn't align well with abstract features in a industrial setting.

## Patch's strategy

divide the image into patches

Using mid-level features and aggregate features **from its local neighbor**.

## Related work

**SPADE:** store multi-layer features of the pretrained network.

**PaDiM:** Using more statistc methods. It calculated the mean and variance of the features. And using Mahalonious Distance to detect the anomaly.

**Patchcore vs SPADE:**

Storing neighborhood-aware patch features

Using coreset sampling

**Patchcore vs PaDiM:**

PaDiM: A top-left patch can only be compared to the model of what a top-left corner is supposed to be like. This requires the test image should be aligned.

Patchcore: creates a large memory bank that is accessible to all patches.

## Locally aware patch features

Select feature maps from two layers from Resnet, usually 2nd or 3nd.

One point on the feature map stands for the feature of a patch from the original image. Average the features from an area center  ed with (a, b), which is taken as the feaure of (a, b)

Do upsampling for the second feature map to match the size of the first one.

Aggregate the two feature map.

## Coreset downsampling

* It starts with an empty coreset.
* It finds the feature in the full library that is **farthest away** from any feature currently in the coreset.
* It adds this "most isolated" feature to the coreset.
* It repeats this process, always adding the feature that best covers a poorly represented area, until the coreset reaches the desired size (e.g., 1% of the original)

## Anomaly Detection with PatchCore

It breaks the test image into a set of locally-aware patch features just as it did for the trainning images.

For each single patch of the test image, it find the closest match in the memory bank. This gives a distance for each patch.

For all the closet distances, take the maxium as the initial anomaly score.

Then it uses a formula to eliminate the influence of the "rare" normal patch.

**From scoring to Localizing**

PatchCore calculates scores for all the patches. Take all the individual scores and arrange them into a grid. Then it creates a heatmap for the original image.

## Dataset

### MVTec-AD

包含 15 个类别：主要描述物体或者纹理

标注：异常类型划分清晰，每个类不超过 8 种异常

### Magnetic Tile Defects (MTD)

The specialist dataset

### Beyond the Factory: Mini Shanghai Tech Campus (mSTC)

A video surveillance dataset showing pedestrians on a campus.
