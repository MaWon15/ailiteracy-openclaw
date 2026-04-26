# Chapter 25: Computer Vision
**Source:** Artificial Intelligence: A Modern Approach, 4th Edition — Russell & Norvig

## What Is Computer Vision?

**Computer vision** is the field of enabling machines to interpret and understand visual information from the world — images, video, and 3D scenes.

**Challenge:** An image is a 2D projection of a 3D world. Interpretation requires recovering:
- **What** is in the scene (recognition, classification).
- **Where** objects are (detection, segmentation, localization).
- **How** the scene is structured (3D reconstruction, depth estimation).
- **What is happening** (activity recognition, video understanding).

## Image Formation

### Camera Model
- **Pinhole camera:** A ray from a 3D point P through the pinhole projects to image point p.
- **Perspective projection:** P = (X, Y, Z) → p = (fX/Z, fY/Z) where f is focal length.
- **Intrinsic matrix K:** Camera calibration — maps 3D camera coordinates to 2D pixel coordinates.
- **Extrinsic matrix [R|t]:** Camera pose — maps world coordinates to camera coordinates.

### Image Features
- **Pixel:** Intensity or (R, G, B) triple.
- **Edges:** Rapid intensity changes; detected by gradient (Sobel, Canny operators).
- **Corners:** Intersections of edges; detected by Harris corner detector.
- **Blobs and interest points:** Detected at multiple scales (SIFT, SURF, ORB).

**SIFT (Scale-Invariant Feature Transform):**
- Keypoints detected at characteristic scale (Difference of Gaussians).
- Descriptor: Gradient histogram in local neighborhood.
- Invariant to rotation, scale, illumination changes.

## Classic Image Processing

### Filtering
- **Convolution:** Apply a kernel to each pixel and its neighborhood.
- **Gaussian blur:** Smooth image; reduce noise. σ controls amount of smoothing.
- **Sobel/Prewitt:** Edge detection via gradient computation.
- **Laplacian of Gaussian (LoG):** Edge detection at multiple scales.

### Morphological Operations
- **Erosion:** Shrink bright regions.
- **Dilation:** Expand bright regions.
- Applications: noise removal, shape analysis in binary images.

## Image Classification

Assign a label to an entire image.

### Deep Learning Era
- **AlexNet (2012):** 8-layer CNN; won ILSVRC with 15.3% top-5 error vs 26.2% for second place. Launched deep learning revolution in vision.
- **VGGNet:** Deeper with 3×3 filters.
- **Inception (GoogLeNet):** Multi-scale convolutions in parallel.
- **ResNet (2015):** Residual connections; 152 layers; 3.57% top-5 error.
- **EfficientNet:** Systematic compound scaling.
- **Vision Transformers (ViT, 2020):** Apply Transformer directly to patches of an image. State-of-the-art with sufficient data.

**Transfer learning:** Fine-tune ImageNet-pretrained models on small datasets. Dramatically reduces data requirements.

## Object Detection

Locate and classify multiple objects in an image.

### Two-Stage Detectors
- **R-CNN (Girshick et al., 2014):** Generate region proposals (Selective Search); classify each with CNN. Slow.
- **Fast R-CNN:** Share convolutions; classify proposals from shared feature map.
- **Faster R-CNN:** Add **Region Proposal Network (RPN)** — fully end-to-end. Standard architecture.

### Single-Stage Detectors (faster, slightly less accurate)
- **YOLO (You Only Look Once):** Predict bounding boxes and classes in a single pass. Real-time capable.
- **SSD (Single Shot MultiBox Detector):** Multi-scale predictions.

### Detection Metrics
- **IoU (Intersection over Union):** Overlap between predicted and ground-truth box.
- **mAP (mean Average Precision):** Area under the precision-recall curve; averaged over classes.

## Semantic Segmentation

Assign a class label to every pixel.

- **FCN (Fully Convolutional Network):** Replace classification head with deconvolution for pixel-wise prediction.
- **U-Net:** Encoder-decoder with skip connections; popular in medical imaging.
- **DeepLab:** Dilated convolutions for large receptive field without downsampling.

## Instance Segmentation

Detect individual object instances and segment each.

- **Mask R-CNN:** Faster R-CNN + a mask prediction head for each detected instance.

## 3D Vision

### Stereo Vision
- Two cameras at different positions; **disparity** (horizontal offset) encodes depth.
- **Disparity map → depth map** via triangulation.

### Structure from Motion (SfM)
- Recover 3D structure and camera poses from multiple 2D images.
- Feature matching → fundamental matrix → pose estimation → bundle adjustment.

### Depth Estimation
- **Monocular depth estimation:** Predict depth from a single image using CNNs.
- **LiDAR:** Active depth sensor; provides accurate point clouds.

### NeRF (Neural Radiance Fields)
- Represent a 3D scene as a neural network mapping (x, y, z, θ, φ) → (RGB, density).
- Novel view synthesis: render the scene from any viewpoint.

## Generative Models for Vision

- **VAEs:** Generate new images by sampling from latent space.
- **GANs:** Generator vs discriminator; produce photorealistic images.
- **Diffusion models (DALL-E 2, Stable Diffusion):** Denoise from Gaussian noise; state-of-the-art image synthesis.
- **CLIP:** Jointly train image and text encoders; enables zero-shot classification and image-text retrieval.

## Video Understanding

- **Optical flow:** Dense correspondence between frames — estimates apparent motion.
- **Action recognition:** Classify the action in a video clip (3D CNNs, Two-Stream, Video Transformers).
- **Object tracking:** Follow an object across frames; SORT, DeepSORT.

## Key Terms

- **CNN:** Convolutional Neural Network — standard architecture for image understanding.
- **Object detection:** Locate and classify multiple objects; Faster R-CNN, YOLO.
- **Semantic segmentation:** Pixel-level classification.
- **Instance segmentation:** Detect and segment individual object instances.
- **SIFT:** Scale-invariant feature descriptor for matching image patches.
- **Stereo vision:** Recover depth from two cameras via disparity.
- **NeRF:** Neural representation of 3D scenes for novel view synthesis.
- **Diffusion model:** State-of-the-art generative model for images (DALL-E 2, Stable Diffusion).
- **ViT:** Vision Transformer — applies self-attention to image patches.
