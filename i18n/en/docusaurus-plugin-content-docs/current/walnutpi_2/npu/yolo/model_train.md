---
sidebar_position: 8
---
# Online Model Training

The WalnutPi online model training website is designed for users who need to train their own visual models. Without any coding, simply drag and drop images to build a dataset, and with a few simple steps, you can generate a powerful YOLO11 visual model. Upon completion of training, model files and Python scripts are automatically generated and can be directly run on the development board.

Online training website link: https://ai.01studio.cc

Currently supported platform: WalnutPi 2B **(Please use Debian image v1.4 or above)**

Supported visual recognition types: Image Classification, Image Detection

## Registration and Login

Open https://ai.01studio.cc and click the login button in the top right corner.

![train](./img/train/train1.png)

You can register manually or use WeChat or Github account association for one-click login (currently, associated login still requires email or phone number verification).

![train](./img/train/train2.png)

After logging in, click [Avatar--Personal Homepage] in the top right corner to view or modify your personal information.

![train](./img/train/train3.png)

![train](./img/train/train4.png)

## Training a Classification Model

Visual classification is about identifying and classifying images, outputting what item the image most likely contains (without location bounding boxes).

Here is a simple dataset prepared for testing. Click to download: [Sample Dataset (Classification)](https://01studio-1258570164.cos.ap-guangzhou.myqcloud.com/train/%E7%A4%BA%E4%BE%8B%E6%95%B0%E6%8D%AE%E9%9B%86%EF%BC%88%E5%88%86%E7%B1%BB%EF%BC%89.zip). It contains dozens of images of apples and mice.

![train](./img/train/train5.png)

### Creating a Dataset

Click Model Training--Dataset--Create Dataset:

![train](./img/train/train6.png)

Enter the dataset name (custom), select classification, and click create.

![train](./img/train/train7.png)

You can see a new dataset has been created.

![train](./img/train/train8.png)

- `Dataset ID`: Unique number for all datasets;
- `Dataset Name`: The user-defined dataset name;
- `Type`: Visual recognition type, here it is classification;
- `Created Time`: The creation time of the dataset;
- `Last Updated`: The last editing time of the dataset;
- `Actions`: Includes edit and delete buttons (deletion is currently irreversible).

Click the `Edit` button in the right-side actions. On first entry, you will be prompted to create a new label. Here, we are training apple and mouse classification recognition. First, create the apple label **apple** **(Use English labels as much as possible to avoid issues on some development boards without Chinese library support)**.

![train](./img/train/train9.png)

After creation, the apple label appears in the left sidebar. Click the right button to edit or modify.

![train](./img/train/train10.png)

Click [Upload Images to Training Set]

![train](./img/train/train11.png)

Click [Add Images]

![train](./img/train/train12.png)

Select the apple images from the sample dataset downloaded earlier:

![train](./img/train/train13.png)

Click [Upload to Training Set]

![train](./img/train/train14.png)

Use the same method to upload a few images to the validation set. The training set is used for training, and the validation set is used for assessment after each training round. The number of validation set images should generally be about 10%~30% of the total dataset.

![train](./img/train/train15.png)

Click [Create Label], then create a mouse label.

Select the mouse label:

![train](./img/train/train16.png)

Use the same method as before to upload the mouse images from the sample dataset to the training set and validation set.

![train](./img/train/train17.png)

### Start Training

Click [Create Training Task] above the dataset:

![train](./img/train/train18.png)

Configure training parameters: **Generally, the default configuration is fine.**

![train](./img/train/train19.png)

- `Target Board`: Select WalnutPi 2B here;
- `Model Type`: Automatically selected based on the dataset;
- `Model Scale`: For development boards, generally choose n or s, as others may not run.
![train](./img/train/train20.png)
- `Training Epochs`: The platform allows a maximum of 500 epochs;
- `Model Size`: Larger values improve accuracy but increase runtime. Generally recommended 224 or 320.
- `Batch Size`: Default is 16. If there are many images (around a thousand), you can select 32 to improve training speed;
- `Max Learning Rate (lr0)`: Default is 0.01, usually no need to adjust;

After clicking [Submit], you will automatically be redirected to the training interface:

![train](./img/train/train21.png)

The left side shows project information, the top right shows training logs, and the bottom right shows training result charts. Taking the example below, the model achieved 100% recognition accuracy after the 5th iteration, with excellent results.

![train](./img/train/train22.png)

Click the left navigation bar--Training Records to see all training project information. Click the [Details] button on the right to enter:

![train](./img/train/train23.png)

After training is complete, you can click the [Download] button to download the model and code files.

![train](./img/train/train24.png)

### Deployment and Running

After downloading, copy the model file to WalnutPi 2B via USB drive or other methods. The desktop version system is recommended to conveniently observe camera or image recognition results.

You can also open https://ai.01studio.cc in the desktop version WalnutPi system browser, log in with the same account, and download the training result files from the training records.

![train](./img/train/train25.png)

Use the following command to decompress.

```bash
tar -xvf 3.tar
```

![train](./img/train/train26.png)

You can see there are 4 files:

![train](./img/train/train27.png)

They are:

- `best.nb`: Model file suitable for WalnutPi 2B (Allwinner T527)
- `val.jpg`: Image used for testing the picture demo
- `demo-picture.py`: Picture recognition demo, uses val.jpg
- `demo-camera.py`: USB camera recognition

#### Image-Based

Use the **python demo-picture.py** command in the terminal, or open and run it with Thonny.
You can see the recognition result is mouse, with a confidence of 0.97 (max 1). At the same time, result.jpg is returned in the current path, with recognition info in the top left corner of the image.

![train](./img/train/train28.png)

#### Camera-Based

Connect a USB camera to WalnutPi 2B:

![train](./img/train/train29.png)

Run the command in the terminal: **python demo-camera.py**. A camera image display window will appear, allowing real-time classification recognition of objects.

![train](./img/train/train30.png)

## Training a Detection Model

Image detection identifies the types of objects trained in the images and annotates them with bounding boxes.

Here is a simple dataset prepared for testing. Click to download: [Sample Dataset (Detection)](https://01studio-1258570164.cos.ap-guangzhou.myqcloud.com/train/%E7%A4%BA%E4%BE%8B%E6%95%B0%E6%8D%AE%E9%9B%86%EF%BC%88%E6%A3%80%E6%B5%8B%EF%BC%89.zip). It contains dozens of images of apples and bananas, each with an already annotated label.txt file.

The "train" folder contains the training set, and the "val" folder contains the validation set.

![train](./img/train/train31.png)

### Creating a Dataset

Click Model Training--Dataset--Create Dataset:

![train](./img/train/train6.png)

Enter the dataset name (custom), select detection, and click create.

![train](./img/train/train32.png)

You can see a new dataset has been created.

![train](./img/train/train33.png)

- `Dataset ID`: Unique number for all datasets;
- `Dataset Name`: The user-defined dataset name;
- `Type`: Visual recognition type, here it is classification;
- `Created Time`: The creation time of the dataset;
- `Last Updated`: The last editing time of the dataset;
- `Actions`: Includes edit and delete buttons (deletion is currently irreversible).

Click the [Edit] button to enter the dataset editing page, then click upload images:

![train](./img/train/train34.png)

First upload to the training set:

![train](./img/train/train35.png)

Add and upload all images from the "train" folder of the sample dataset.

![train](./img/train/train36.png)

![train](./img/train/train37.png)

Create a label on the right with the name apple and a custom color.

![train](./img/train/train38.png)

![train](./img/train/train39.png)

After creation, it looks like this:

![train](./img/train/train40.png)

Then create a banana label **banana**. **(Tip: After creating, click the small button on the right to re-edit)**

![train](./img/train/train41.png)

#### Image Annotation

Next, we can annotate the images. Start from the first image:

![train](./img/train/train42.png)

First select the apple label in the label bar, then use the mouse to draw a box around the apple. Once done, it looks like the image below: a box on the left with the number 1 inside, and annotation box info on the bottom right.

![train](./img/train/train43.png)

Use the same method to annotate the banana as well.

![train](./img/train/train44.png)

Finally, use the same method to annotate the apples and bananas in all images.

![train](./img/train/train45.png)

<br></br>

After the training set annotation is complete, upload the val folder images to the validation set. **The training set is used for training, and the validation set is used for assessment after each training round. The number of validation set images should generally be about 10%~30% of the total dataset.**

![train](./img/train/train46.png)

![train](./img/train/train47.png)

Then use the same method as the training set to annotate.

The following position allows you to filter the training set, validation set, and whether images have been annotated.

![train](./img/train/train48.png)

The detection dataset annotation is now complete.

::::tip Note
The platform currently supports uploading and exporting annotation files, only supporting YOLO TXT format. Each TXT file corresponds to all annotation targets of one image, with each line representing one target in the format:
**`&lt;class_index&gt; &lt;center_x&gt; &lt;center_y&gt; &lt;width&gt; &lt;height&gt;`**
::::

The sample detection dataset contains annotation info files with the same name as the images (txt files). They can be directly uploaded and imported.

![train](./img/train/train49.png)

Click upload annotation file:

![train](./img/train/train50.png)

After import, if the label names are inconsistent, manually modify them.

![train](./img/train/train51.png)

### Start Training

After completing annotation, click [Create Training Task] above the dataset:

![train](./img/train/train52.png)

Configure training parameters: **Generally, the default configuration is fine.**

![train](./img/train/train19.png)

- `Target Board`: Select WalnutPi 2B here;
- `Model Type`: Automatically selected based on the dataset;
- `Model Scale`: For development boards, generally choose n or s, as others may not run.
![train](./img/train/train20.png)
- `Training Epochs`: The platform allows a maximum of 500 epochs;
- `Model Size`: Larger values improve accuracy but increase runtime. Generally recommended 224 or 320.
- `Batch Size`: Default is 16. If there are many images (around a thousand), you can select 32 to improve training speed;
- `Max Learning Rate (lr0)`: Default is 0.01, usually no need to adjust;

After clicking [Submit], you will automatically be redirected to the training interface:

![train](./img/train/train53.png)

The left side shows project information, the top right shows training logs, and the bottom right shows training result charts. Taking the example below, after 100 epochs of training, the final **mAP50** value is 0.94 (>0.8), and the **mAP50-95** value is 0.65 (>0.5), with excellent results.

![train](./img/train/train54.png)

Click the left navigation bar--Training Records to see all training project information. Click the [Details] button on the right to enter:

![train](./img/train/train23.png)

After training is complete, you can click the [Download] button to download the model and code files.

![train](./img/train/train24.png)

### Deployment and Running

After downloading, copy to WalnutPi 2B via USB drive or other methods. The desktop version system is recommended to conveniently observe camera or image recognition results.

You can also open https://ai.01studio.cc in the desktop version WalnutPi system browser, log in with the same account, and download the training result files from the training records.

![train](./img/train/train55.png)

Use the command tar -xvf 71.rar to decompress (modify according to your own file name). You can see there are 4 files:

![train](./img/train/train56.png)

They are:

- `best.nb`: Model file suitable for WalnutPi 2B (Allwinner T527)
- `val.jpg`: Image used for testing the picture demo
- `demo-picture.py`: Picture recognition demo, uses val.jpg
- `demo-camera.py`: USB camera recognition

#### Image-Based

Use the **python demo-picture.py** command in the terminal, or open and run it with Thonny.

You can see the recognition results, with the identified fruits annotated, **and the result image result.jpg returned in the current path**.

![train](./img/train/train57.png)

#### Camera-Based

Connect a USB camera to WalnutPi 2B:

![train](./img/train/train29.png)

Run the command in the terminal: **python demo-camera.py**. A camera image display window will appear, allowing real-time detection of objects with bounding box annotation.

![train](./img/train/train58.png)

## Model Sharing

After training is complete, you can choose to share your model for other users to use, or browse the model sharing library to find a model that suits your needs.

### Model Sharing Library

Link: https://ai.01studio.cc/market

Click the link to enter the model sharing library, where you can see all models shared by users. Use the filter bar at the top to filter models that suit your needs.

![train](./img/train/share8.png)

Click a model card to enter and see the detailed information of the current model. On the right, you can add to favorites and download the model for deployment on your own development board. **Make sure the model development board model is consistent**.

![train](./img/train/share9.png)

### Sharing Your Own Model

Find the successfully trained record in the training records and click the `Share` button:

![train](./img/train/share1.png)

Enter the sharing editing interface. The platform will automatically generate some existing model information:

![train](./img/train/share2.png)

- Upload Cover

You can upload your own image or use the platform-generated image. The automatically generated detection image supports scaling.

![train](./img/train/share3.png)

- Fill in Model Name and Model Introduction

The model name is like a title; keep it short. The introduction can briefly describe this model.

![train](./img/train/share4.png)

- Detailed Description

The details have been pre-generated with some content that users can modify themselves. The editing box has rich editing features such as image upload and full-screen mode. Supports MarkDown syntax, allowing you to insert Bilibili videos and other functions. After editing, click the `Publish` button.

![train](./img/train/share5.png)

After publishing, you can click the `Edit` button below to edit again:

![train](./img/train/share6.png)

After publishing, you can see the relevant information in the model sharing library.

![train](./img/train/share7.png)


