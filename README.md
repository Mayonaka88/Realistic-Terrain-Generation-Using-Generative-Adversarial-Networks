# Realistic Terrain Generation Using Generative Adversarial Networks

Please note that the models implemented are currently closed-sourced and are available for sale, ensuring their exclusivity and value to potential customers. To inquire about licensing options and pricing, please reach out to me via [email](abdallah.elabora@gmail.com) or [LinkedIn](https://www.linkedin.com/in/abdallah-elabora-0942a6233/).

The models created and implemented are utilized in [SynthEarth AI](https://mayonaka88.itch.io/synthearth-ai) which is a drawing and photo editing tool that provides real-time AI-Powered hyper-realistic terrain generation from drawing.

The application allows users to generate terrain from an imported image or from an on-application canvas. The application allows users to save the generated terrain. The application also allows users to randomly generate terrain using the DCGAN model created.

The application was created purely for the purpose of presenting the power of the models created and serves as a proof of concept for intelligent generative terrain. 

## Introduction

Step into the virtual realities, where reality merges with imagination, and creativity knows no bounds! In this interconnected digital universe, prepare for an extraordinary journey filled with immersive landscapes, adventurous encounters, and the chance to shape your own destiny.

Filmmakers can now turn virtual environments into stunning realities on the big screen, while video game developers offer immersive experiences that combine cinematic storytelling and interactive gameplay. Engineers can prepare for any scenario using hyper-realistic environments and meteorologists can study weather patterns to help predict disasters.

As technology continues to advance, the demand for realistic and immersive virtual experiences grows. Whether it's a sprawling fantasy landscape in a video game or a meticulously replicated real-world location in a training simulator, the terrain sets the stage for the user's interaction and engagement.

By accurately simulating the natural features of the Earth's surface, such as mountains, valleys, and rivers, terrain generation breathes life into virtual worlds and enhances the user's sense of presence and immersion.

## Methodologies

For generating realistic terrain, the tools and libraries used are shared throughout the models created. Python was used throughout the implementation and development of the models and many Python packages were utilized. 

> Pytorch for the development of the DCGAN

> TenserFlow/Keras for the development of the CRNN, cGAN (Pix2Pix), and the CNN

> Numpy & OpenCV for data and image manipulation

> Tkinter for the development of the GUI


## Models Used

Approaching the objectives we set out to accomplish, there were many paths to explore.

The first method was to use a Deep Convolutional Generative Adversarial Network to generate terrain from random noise data and then use a Convolutional Recurrent Neural Network to predict the next sequence of pixels. This can allow us to generate terrain infinitely by continuously generating the next sequence of pixels.

The other method was to use 2 conditional Generative Adversarial Networks that would generate terrain based on the output of the other. This creates a grid effect that in theory can generate terrain infinitely. 

Finally, we used a Convolutional Neural Network to evaluate the model and to measure how realistic our generative networks are compared to real-world terrain height data. 

The final list of all models tested are:

> 1 Deep Convolutional Generative Adversarial Network

> 1 Convolutional Recurrent Neural Network

> 3 Conditional Generative Adversarial Networks

> 1 Convolutional Neural Network

## Dataset Used

The dataset is composed of 5000 image sets. Each set represents a random 512x512 pixel crop of the Earth and is composed of a Height map that contains altitude information through pixel value.

In order to have sufficient data to train the DCGAN, we needed to divide the 512x512 pictures into multiple pictures of 64x64 so now for each individual picture it produces 64 instead, which leaves us with 320k pictures to train.

## [SynthEarth Dataset](https://github.com/Mayonaka88/SynthEarth-Dataset)

The SynthEarth dataset is a brand-new dataset created specifically for this project. The dataset is created based on real-world terrain elevation data. 

The new dataset was created by training the DCGAN and utilizing it to create brand new unique hyper-realistic images of real word elevation. Each image in the new SynthEarth dataset is normalized, changed to greyscale, and has the dimensions of 64 pixels by 64 pixels.

Currently, The SynthEarth dataset consists of 150k unsegmented images, 150k 2 shades segmented images, 150k 3 shades segmented images, and 150k 5 shades segmented images. In total, there are currently 600k images in the dataset with plans for expansion. 

For more information, check out the repository of the brand-new dataset [here](https://github.com/Mayonaka88/SynthEarth-Dataset)!

## Prototypes and Testing

The final DCGAN model was trained using fine-tuned preprocessed data which resulted in the preservation of the detail of terrain data. The final model was utilized to create the brand-new SynthEarth dataset.

For the CRNN, many iterations were made but ultimately the model was scrapped due to undesired outputs. The output would generate the next sequence of pixels however not enough unique new data existed after every prediction which resulted in the predictions defaulting to a constant value of 0. 

For the conditional GANs, the first implementation contained two conditional GANs to infinitely generate terrain. Each model will generate from the output of the other. In theory, this should allow for the generation of terrain infinitely and from all sides.

However, in practice, the model faced a similar issue as the CRNN where subsequent predictions lost their original context and started predicting unusable data that did not follow the sequence. Ultimately, this method was scrapped.

The final conditional GAN is used to generate terrain from a drawing of the terrain. Even though it is restricted by size, in theory, this model will provide more control and input from the user to customize their terrain.

The final conditional GAN has been trained 3 times on 3 different new datasets created for it. Each iteration of this model is trained using different segmentation of the main dataset created in this project. 

In testing, the model in all iterations performed substantially better than the other models tested and implemented. In fact, through testing, it showed a high level of accurate prediction throughout all iterations and their testing. However, some iterations are better than others. The model that had the best user experience was the model that trained on the 5 shades segmented data from the SynthEarth dataset. This is due to the presence of more features than the other models.

## Evaluation

> Trained and tested two datasets, which consist of earth and Perlin noise. 

> Used these trained and tested datasets and compared them to our dataset created using DCGAN.

> Comparing Perlin noise to earth, the accuracy of the CNN returned to be around 90%.

> The model was trained for 100 epochs but stopped at 17/100 using Early Stopping to avoid overfitting. 

> Our dataset compared to Earth scored above 99%.

## Future Work

### Implementing a grid system

> Generating a new patch of terrain based on its 8 adjacent neighbors in a grid. Utilizing this method, context from the larger whole of the generated terrain is preserved, and context-aware infinitely procedurally generating terrain would be plausible.


### Utilizing region data

> Different regions and biomes have different terrain. In future implementations, tagging terrain belonging to a biome will result in a more dynamic and realistic terrain generation.






