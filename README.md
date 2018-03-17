# My Deep ANPR


The work is based on Matthew Earl's [repository](https://github.com/matthewearl/deep-anpr).  
Do follow his [blog post](http://matthewearl.github.io/2016/05/06/cnn-anpr/) to get an overview how he designed the sysytem.


Here we are using CNN based sliding window approach to build an automatic number plate recognition system.The system performs well on standard number plates used in countries like UK but fails to achieve decent results on Indian Number plates.

*Another shortcoming with this model is that , the model has been designed based on the assumption of all the  number plates having 10 digits (7 digits in Matt Earls), which leads to error for recognition of number plates which don't have 10 digits.*


Following is a result of the model on an Indian Number Plate:
![alt text](https://raw.githubusercontent.com/mahavird/my_deep_anpr/master/output/out_4_1.jpg)


**Note: This is an experimental project and is incomplete in a number of ways,
if you're looking for a practical number plate recognition system this project
is not for you.** If however you've read the above blog post and wish to tinker
with the code, read on.  If you're really keen you can tackle some of the
enhancements on the Issues page to help make this project more practical.
Please comment on the relevant issue if you plan on making an enhancement and
we can talk through the potential solution.

# Usage is as follows:

1. `./extractbgs.py SUN397.tar.gz`: Extract ~3GB of background images from the [SUN database](http://groups.csail.mit.edu/vision/SUN/)
   into `bgs/`. (`bgs/` must not already exist.) The tar file (36GB) can be [downloaded here](http://vision.princeton.edu/projects/2010/SUN/SUN397.tar.gz).
   This step may take a while as it will extract 108,634 images.

2. `./gen.py 1000`: Generate 1000 test set images in `test/`. (`test/` must not
    already exist.) This step requires `UKNumberPlate.ttf` to be in the
    `fonts/` directory, which can be
    [downloaded here](http://www.dafont.com/uk-number-plate.font).

3. `./train.py`: Train the model. A GPU is recommended for this step. It will
   take around 100,000 batches to converge. When you're satisfied that the
   network has learned enough press `Ctrl+C` and the process will write the
   weights to `weights.npz` and return.
   (Google Drive link for the [weights.npz](https://drive.google.com/file/d/1ZArKaR2HfY_319A7WUAVRSU7KO8E5klE/view?usp=sharing))

4. `./detect.py in.jpg weights.npz out.jpg`: Detect number plates in an image.

# The project has the following dependencies:

* Using a python virtual environment is recommended.
* Code is based on python3 
* [TensorFlow](https://tensorflow.org) (TF Version 1.0.1, cuda 8.0, cudnn 5.0)
* OpenCV (Easy install: `pip install opencv-python`)
* NumPy

# If you directly want to see the results on a 10 digit license plate,do following:

1. `git clone https://github.com/mahavird/my_deep_anpr.git`

2. To download the weights.npz use following command:  
`python gdrivedownload.py 1ZArKaR2HfY_319A7WUAVRSU7KO8E5klE /home/mahavircingular/my_deep_anpr/weights.npz`

Replace the destination folder with your destination folder(In my case it is `/home/mahavircingular/my_deep_anpr/weights.npz` )

Finally see the output in out.jpg  
3. `python detect.py in.jpg weights.npz out.jpg`
