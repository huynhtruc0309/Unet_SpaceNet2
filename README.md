# SpaceNet2 Report
sn2_AOI_5_Khartoum dataset: https://drive.google.com/drive/folders/1-E0Qf56LnZJzwOGDRAGXLRgkHa1cT8Cx?usp=sharing

I try to solve this as an image segmentation problem and build a segmentation model which is Unet in Pytorch (based on this https://www.pyimagesearch.com/2021/11/08/u-net-training-image-segmentation-models-in-pytorch/). This report covers:

* An overview of U-Net features that make it a powerful segmentation model
* Creating a custom PyTorch Dataset for Space Net 2
* Training the U-Net segmentation model

## An overview of U-Net that make it a powerful segmentation model
* The U-Net architecture follows an encoder-decoder structure, where the encoder gradually compresses information into a lower-dimensional representation. Then the decoder decodes this information back to the original image dimension. Owing to this, the architecture gets an overall U-shape, which leads to the name U-Net.

* One of the salient features of the U-Net architecture is the skip connections, which enable the flow of information from the encoder side to the decoder side, enabling the model to make better predictions.

* As we go deeper, the encoder processes information at higher levels of abstraction. This simply means that at the initial layers, the feature maps of the encoder capture low-level details about object texture and edges, and as we gradually go deeper, the features capture high-level information about object shapes and categories.

* To segment objects in an image, both low-level and high-level information is important. For example, a change in texture between objects and edge information can help determine the boundaries of various objects. On the other hand, high-level information about the class to which an object shape belongs can help segment corresponding pixels to correct object classes they represent.

* Thus, to use both these pieces of information during predictions, the U-Net architecture implements skip connections between the encoder and decoder. This enables us to take intermediate feature map information from various depths on the encoder side and concatenate it at the decoder side to process and facilitate better predictions.

## Creating a custom PyTorch Dataset for Space Net 2
* I chose Khartoum as it is the smallest one. Downloading them is very time-consuming, AWS made me wait for 24h in oder to be able to register for AWS CLI. I managed to download it through mlhub https://mlhub.earth/data/spacenet2 and torchgeo https://torchgeo.readthedocs.io/en/latest/api/datasets.html#torchgeo.datasets.SpaceNet.

* torchgeo provided torchgeo.datasets.SpaceNet2 but it doesn't have train_test_split so I reimplement this class that allow me to create object by list of file paths from train and test split.

* About the .tif image files, to read them I use rasterio because PIL and cv2 read them wrong in this case.

## Training the U-Net segmentation model from scratch
* Overall, U-Net model will consist of an Encoder class and a Decoder class. The encoder will gradually reduce the spatial dimension to compress information. Furthermore, it will increase the number of channels, that is, the number of feature maps at each stage, enabling our model to capture different details or features in our image. On the other hand, the decoder will take the final encoder representation and gradually increase the spatial dimension and reduce the number of channels to finally output a segmentation mask of the same spatial dimension as the input image.

* I used Unet class definition from https://www.pyimagesearch.com/2021/11/08/u-net-training-image-segmentation-models-in-pytorch/

### Conclusion
In this task, I have completed:
* Researching about Unet and other segmentation models.
* Examinating SpaceNet2 sn2_AOI_5_Khartoum.
* Define Dataset and Model class

I have failed:
* Training the model because loss go to 0 after the first epoch
* Completing the task

Problem that I have met:
* Download the dataset with AWS
* Colab GPU limitation
