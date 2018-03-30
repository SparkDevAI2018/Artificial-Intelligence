CEILNet
=======

This is the implementation of ICCV 2017 paper *"A Generic Deep Architecture for Single Image Reflection Removal and Image Smoothing"* by Qingnan Fan *et al.*.

Guess which is real and which is synthetic?
![teaser](iccv17_poster_template-teaser.png "sample")

Note
----
All the test images, trained codes, test codes, data generation codes and trained models of both reflection removal and image smoothing tasks are released here. The ground truth reflection and background layer of synthetic reflection images are also public.

**Compilation** 

Our codes are implemented in Torch framework, before testing or training the models, you need to install the latest torch framework and compile the **computeEdge.lua**, **ComputeXGrad.lua**, **ComputeYGrad.lua** and **L1Criterion.lua** under the nn module, and compile **adam_state.lua** under optim module.

To be specific, the front 4 lua files have to be put in **./torch/extra/nn** module directory, and editing **init.lua** file to include the corresponding file. Finally run the command under nn directory, **luarocks make ./rocks/nn-scm-1.rockspec**. Then nn module will be independently compiled. Accordingly, the adam lua file has to be put in **./torch/pkg/optim**, edit the **init.lua** file and then run **luarocks make optim-1.0.5-0.rockspec**.

**Data Generation** 

By generating the training or testing data of image smoothing tasks, you need to run existing edge-aware filters first, and split the training and testing data in different lists. An example is shown in "VOC2012_fullsize_L0_train.txt" and "VOC2012_fullsize_L0_test.txt". Note the images are trained on original image size without cropping or scaling.

Regarding the reflection removal task, 
1. The synthetic training data is generated on the fly, but beforehand you also need to split plenty of natural images with the same image size in different file lists as demonstrated in "VOC2012_224_train_png.txt" and "VOC2012_224_test_png.txt".
2. The synthetic test images can be generated by "generate_data_reflection.lua".

**Training** 

The trained models we use to evaluate the performance in the paper are also released here with name like "CEILNet_*.net".

Trained codes are lua files with the same format "training_*.lua". Note E-CNN and I-CNN can be trained in parallel, and are finetuned together afterwards.

**Evaluation** 

Test images are in folder "testdata_reflection_real", "testdata_reflection_synthetic" and "testdata_smooth".
To test the trained models, run "evaluation_reflection.lua" or "evaluation_smooth.lua".

**ATTENTION**

Our CNN dose not predict refletion layers. The following code computes approximate reflection layers by simply subtracting the predicted background layers from the input images. Note the result so-obtained may not reflect the image structure and appearance of the original reflection scene. 

Cite
----

You can use our codes for research purpose only. And please cite our paper when you use our codes.
```
@article{fan2017generic,
  title={A Generic Deep Architecture for Single Image Reflection Removal and Image Smoothing},
  author={Fan, Qingnan and Yang, Jiaolong and Hua, Gang and Chen, Baoquan and Wipf, David},
  booktitle={IEEE International Conference on Computer Vision (ICCV)},
  year={2017}
}
```
Contact
-------

If you find any bugs or have any ideas of optimizing these codes, please contact me via fqnchina [at] gmail [dot] com



