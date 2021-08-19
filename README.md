# Project-Eyesight
Project eyesight analyzes and detects different daily life activities of a person, currently trained on six classes, i.e



        1. Standing
        2. Sitting
        3. Drinking Water
        4. Reading book
        5. Tensed
        6. Unconscious
        
and alerts in case of any unwanted happening or unethical activity. EYESIGHT can be used for  monitoring workplaces like offices, households, as well as can be used for security measures i.e. Atm guards, Police stations etc. 
    

Quick abstract :-


    The project is able to classify a persons actions on the basis of these six classes, and can be extended to include more number of classes. Also, Eyesight 
    can analyze the activities of a person and alert the programmer if something unethical or unwanted happens via text messages and emails,Eyesight uses MobileNet 
    architecture and SSds to classify and train on different classes and provides accuracy of 93% and above in real time.


Detailed Explanation:-

We used a pre-built architecture, specially designed by tensorflow for faster object detection. It compromises accuracy for speed, however, it yielded great results.
The architecture used two components :-


    1.	Mobile net base architecture
    2.	Multiple SSDs for object detection.

Mobile Net architecture :- 


    It is a predefined and refined architecture specially designed to provide a speed of 25 fps using Covolutional Neural Networks, by trading off accuracy. It uses depthwise separable convolution which is a depthwise convolution followed by a point wise convolution.

 

SSD(Single Shot detector Algorithm):-

    The SSD architecture is a single convolution network that learns to predict bounding box locations and classify these locations in one pass. Hence, SSD can be trained end-to-end. The SSD network consists of base architecture (MobileNet in this case) followed by several convolution layers:
 

By using SSD, we only need to take one single shot to detect multiple objects within the image, while regional proposal network (RPN) based approaches such as R-CNN series that need two shots, one for generating region proposals, one for detecting the object of each proposal. Thus, SSD is much faster compared with two-shot RPN-based approaches.

Tensorflow Object Detection Api and dataset :-
    Tensorflow has created various state of the art models for the purpose of object detection. Thus we used one of those models named ‘ssd_mobilenet_v2_fpnlite_320x320_coco17_tpu-8’. We used this prebuilt architecture on the dataset of “https://homepages.inf.ed.ac.uk/rbf/OFFICEDATA/”. The dataset is over 30 GB and has more than 5 lakh frames which contains data for over 20 days of an office and 4 labels including :-

    0 --- Room is empty (the position values are also 0)
    1 --- Person is standing/walking
    2 --- Person is sitting
    3 --- Two or three people are talking to each other
    4 --- Person in room has fallen


However, it did not suit our needs as :-


    1.	Very few labels
    2.	Labels do not provide a behavioural aspect
    3.	Oversized dataset required too much time to train.

So a new dataset was created manually :-


    1.	We collected images of ourselves doing daily office work.
    2.	The images were then labelled using labelimg, a python package specially efficient in labelling.
    3.	The labelled images and their XML files were then separated into train and test category.
    4.	The dataset contained 6 labels:-
        a.	Working
        b.	Standing
        c.	Drinking Water
        d.	Reading
        e.	Tensed
        f.	Unconscious


Advantages :-


    1.	Not only we created labels perfect for behavioural aspects, but it greatly reduced training time and increased accuracy.
    2.	We could perform real time activity detection as the model was trained especially for us.

Implementation :-


    1.	Used the model architecture from tensorflow object detection:-
                    a.	Tensorflow has a heap of models for the purpose of object detection. However there is a tradeoff between speed and accuracy on the models, the higher the                               speed, the lower the accuracy. So we chose a model concentrated in speed. i.e. ‘ssd_mobilenet_v2_fpnlite_320x320_coco17_tpu-8’.
                    b.	The model converted images to 320x320, used them for detection, then decompressed the images for visualization.
                    c.	The model supported image Augmentation.
                    d.	Used the object_detection api to implement the model.
    2.	Changed the config file according to our needs.
                    a.	The config file contained paths to be configured i.e. the label path, the tf record path and the number of classes.
                    b.	The config file also contained the checkpoint path necessaryto implement the moel with minimum loss percentage.
    3.	Generated the dataset.
                    a.	30 different images under 6 categories were taken which amounts to 180 images.
                    b.	26 images from each category were transported to train set
                    c.	4 images from each category ere transported to test set.
    4.	Labelled the dataset
                    a.	LabelImg is a python software used to Label Images
                    b.	The images were labelled according to their category.
    5.	Generated tensorflow records from the labelled images so as to increase speed.
                    a.	A script was used to convert the images and xml Files into tensorflow records.
                    b.	The tf records helped speed up training process exponentially.
    6.	Trained the model using tf records.
                    a.	The model was trained for 20,000 steps achieveing a low loss function.
                    b.	The model was exported into a checkpoint and used for real time object detection.
    7.	Applied the model for real time activity detection.
                    a.	The checkpoint was accessed and along with OpenCV, a 30fps detection rate was achieved over 6 different labels.



