# product-Endoursement
It is a real time Application which track the brand so that they they van analyse how their app is performing on social media
based on google firebase.

                

Under the supervision of Mr. Vivek Kumar Singh




# ACKNOWLEDGEMENT 


We would like to thank Mr. Vivek Kumar Singh, Jaypee Institute of Information Technology, for his guidance, help and useful suggestions. 
We express gratitude to Dept. of Computer Science/ IT, JIIT Noida, for their guidance, continuous encouragement and supervision throughout the course of the present work. 
We also wish to extend my thanks to our friends and classmates for their insightful comments and constructive suggestions to improve the quality of this project work. 




# INTRODUCTION
Although print, television, and radio advertising are still relevant, they can no longer comprise your entire marketing strategy; consumers now desire a more personal connection, and traditional advertising comes across as passive in the digital era. There are many benefit of social media that indicate how social media is more effective than traditional media. These benefits include the ability to communicate with your consumers in a two-way format, developing a long-term following, and being able to quickly promote new products and services.
However, there is one defining metric that defines the better option between traditional media and social media. This metric is cost per thousand impressions (CPM)
CPM is an advertising metric that measures how many advertising dollars you must spend to reach 1,000 people. The goal of any advertising should be to reach as many relevant people as possible at the lowest cost.

<img width="423" alt="image" src="https://user-images.githubusercontent.com/41268465/117125679-7cd6bb80-adb7-11eb-9f7c-b82960fe4bec.png">




Influencers Help Build Brand Trust
Influencer marketing is having a big moment now. Brands are increasingly turning to social media platforms for their marketing, and there are good reasons why 49% of consumers claim that they depend on influencer recommendations on social media to inform their purchasing decision (Fourcommunications,2018). 
This means that if consumers feel confident in the recommendation from an influencer, they’ll be more likely to purchase the product. This social media statistic makes it evident how brands could piggybank on the power of influencers to reach out to their customers. 

The project is a pure Development type.






# RESEARCH PAPERS

Bag of Freebies for Training Object Detection Neural Networks-

https://arxiv.org/pdf/1902.04103.pdf
The project studies the differences on the training accuracy and time between YOLOv3 and RCNN method for object detection.


Relation Networks for Object Detection-

https://openaccess.thecvf.com/content_cvpr_2018/papers/Hu_Relation_Networks_for_CVPR_2018_paper.pdf
        The project helped us in better understanding of Neural Networks.








# Overall Design of the Project

The project is based on client server mechanism.
The two sides of the project are-
Server: This side of the project is a python-based program that inputs the video from client and does processing over it to retrieve frames and then run each frame under trained CNN model to predict the probability of presence of product and returns the duration as result.

Client: This side of the project uses Android Studio and real time database to send and retrieve video, result duration and information about twitter tweets for product marketing.


                   
                    Client sends the
                    video to server.
<img width="680" alt="image" src="https://user-images.githubusercontent.com/41268465/117125748-911ab880-adb7-11eb-8226-86fb547341fe.png">



          Server sends back 
                   duration result.


# SERVER
As mentioned above the whole structure of the project is divided into two sections Client and the server . The server’s job begins when it receives the video from the client . The video is extracted from the backend and then further processed. The entire working here is done using python , the final result is then send back via backend server to the client.
Topics used for the working of server side are- Keras Sequential , CNN Model , OS Directories , Moviepy editor.
The entire workflow of the server is as follows-
+ Retrieving the video from added to backend by the client.
+ Processing the video first and breaking it into frames.
+ Running every frame under the trained CNN model to predict the presence 
     or absence of the product in the frame.
+ Storing the predicted output for every frame in a variable for calculation.
+ Calculating the duration for which the product was in the video by calculating the
      ratio between number of frames in which the product was detected and the total 
      number of frames and multiplying it to the duration of video.
+ This calculated result is stored in a variable and sent back to the client via backend.
PREPARING THE DATASET
The data set for training the model was done at home using mobile phone. We prepared the data set for two different product – Nescafe Cup and Hand Sanitizer. It was done by clicking 500 photos for the cup 250 with and 250 without the cup and then the same for hand sanitizer. As the model training was done through Google Colab we had the data set saved on a drive file for accessing while training the model.

                       

# Designing the CNN Model

Designing of the CNN model took some time as it had to be done so as to get the most optimum result.
The model uses Keras Sequential and Conv2D, MaxPooling2D, LeakyRelu , Dense and Dropout layers .The function defined below returns the model to be used.
The model consists of 4 Conv2D layers and several Relu , Maxpooling and dropout layers. And then the dense layers to give out the output.

 <img width="451" alt="image" src="https://user-images.githubusercontent.com/41268465/117125780-9d067a80-adb7-11eb-80dc-c60b96f92e03.png">


The input layer takes in the input in the shape (64,64,3) and gives out the out put as an array of size 2 with range 0-1 with first value representing the probability of presence of the product and second value probability of absence of the product in the frame.
The activation used for the output is Softmax.

# MODEL SUMMARY

Here we have displayed the various layers in the CNN Model and the total number of parameters .
The drop out layers have been added to the model to prevent an  model.
The last dense layer which is the output layer is giving out the result as an array of size2.
The whole structure of the model was changed a few times layers were added and removed by check the accuracy of the model training and the most optimum was finalized with the highest accuracy.
The model is compiled with loss= Categorical Cross Entropy and a 
Learning Rate of 0.005. 

<img width="259" alt="image" src="https://user-images.githubusercontent.com/41268465/117125802-a394f200-adb7-11eb-8158-b0b912c3024f.png">




# Training of the Model
 The model is fit with 50 epochs and a batch size of 12 . For this particular training of the model we use 80% of the data as the training data and 20% of the data that was picked in random is used for validation as test data.
 ![image](https://user-images.githubusercontent.com/41268465/117125817-aa236980-adb7-11eb-8cf1-e0ae60c20234.png)

 
The label for each element in the data set is as follows-
[1,0] – Label for images with product present
[0,1] – Label for images with product not present
This is how we allotted two different sets- training set and the test set for the training of the model.
training_set and train_label are used as the training data set and the target.
While
test_set and test_label is used as the validation data set and target.

The weights generated after training of the model was saved so as to be used for the video and prediction later.



Now that the model is ready and trained it is all set to predict for the input set of frames from the video provided by the client.



Processing of Input Video 
The processing of the input video involved breaking of the video into frames first. 
Then every frame is run through the CNN model to predict the presence of product.
All of this processing is combined into one single function.
This function takes in input the path to the video and category of the video ( this project right now can test for two product hand sanitiser and Nescafe cup) and gives out as a result the duration for which product was detected.

The variable ans being returned has the duration. 
Mathematics Involved

The result is calculated using a simple mathematic formula ,
Let , cc be the number of frames the product was detected in
idx is the total number of frames
vd is the total duration of the video.
Then,
ans = vd * ( cc / idx )

<img width="317" alt="image" src="https://user-images.githubusercontent.com/41268465/117125870-b60f2b80-adb7-11eb-9d90-327d6910de41.png">


# Final Run
Shown below is running the function for the video containing hand sanitiser , the input gives path to the video and category i.e. 1.

<img width="320" alt="image" src="https://user-images.githubusercontent.com/41268465/117125887-bd363980-adb7-11eb-97bd-b332e82e8468.png">



The out put has the duration for which the hand sanitiser was present in the video.
This final result will then be sent to the backend and then to client as a result.



# Client

The client side of the project is responsible for 2 jobs , One is as discussed it sends videos to the server for processing it and receives the result for the video sent and displays it to the user .
The second job of client is the twitter real time data base retrieval implemented in a manner so as to check how effectively your product is being advertised through the social platform .













The client side is implemented using an app for phone, as we all know apps are the most effective and easy access software for the users right now, almost everyone has a smart phone nowadays hence can easily download the app to use it.
We understand that although the main target audience for this app would be industries that sell a product and have to verify how the marketing of that product is going on the project should be available to a normal user as well.

# LOGIN & REGISTER

Security is one of the most important things in today's cyber world.
To make our app highly secure, we have used one of the most secure real time database, which keep all our users in isolation with each other so that they can work without thinking about security.
Our app is based on real time database server which mean you can access it for any device at any time you will always get a consistent result.
Login in our app is simple: 
just enter your email and password and you are in.
Once you get logged in you will remain login until you logout.
Our app support auto fill feature which mean it will help you with suggestions of previous Login id.

![image](https://user-images.githubusercontent.com/41268465/117125928-c7583800-adb7-11eb-98de-d07f0d5c32e7.png)


# Registration  
Just enter these four required details and you are registered.
You can't use the same email again.
We have minimum password length required to registerDesign and Dashboard

In our app we have used side navigation menu which make our app easy to use for the users.

In our app instead of creating new activity for each option available in side menu we are using a single activity which makes our fast and small in size.

![image](https://user-images.githubusercontent.com/41268465/117125958-cde6af80-adb7-11eb-92d6-7c1600aeef48.png)






# Dashboard

Our app dashboard show us most important things our app is based on -
![image](https://user-images.githubusercontent.com/41268465/117126005-d9d27180-adb7-11eb-9a1c-780200f1a29b.png)

Total time our product displayed in the user uploaded video.
![image](https://user-images.githubusercontent.com/41268465/117125985-d4752700-adb7-11eb-96b0-2334e2b682dc.png)

Tweet our brand ambassador made in past 7 days.

# TWITTER

![image](https://user-images.githubusercontent.com/41268465/117126137-f9699a00-adb7-11eb-86a0-3a5dd8315548.png)


It is very common nowadays for companies to use social media platforms for marketing of their product. Keeping the main motive of the project in mind “To verify Effectiveness of an advertisement” we have even added a way to check how effectively the product is being advertised on a social platform as well. Twitter is one of the major social media platform and is most widely used for brand advertisement. Keeping this in mind me made our app work with tweets. You can use it to track users, or by typing a particular  keyword.

It track users and the brand name of the company and give you the result through which you can analyze how your brand is going on twitter 
We have integrated twitter as firebase database so that it can be easy for the user to use it.


![image](https://user-images.githubusercontent.com/41268465/117126152-fe2e4e00-adb7-11eb-97d8-d982226feeca.png)



There is an explore button which takes you to the list of the tweets  we receive using the given input . On clicking on any of the tweet you can see detail of the tweet likes ,retweet everything you want you can get it just by tapping .

# VIDEO PROCESSING

In our app we have use real-time storage system so that user can upload video easily ,we are performing machine learning based processing on our server which maker app faster and easy to use. users just need to upload the file rest of the work is done at server.
User can see the list of the video it has uploaded and the time object appear in that video for now we are working on only two kind of object sanitizer and Nescafe coffee but in future we will increase the object list.
Our app is smart enough to resolve network issue if any , it start the upload again from where it left due to an error.
We can see a preview of our video before uploading it to the server.

After receiving the timing, we update the main dashboard of our app.



![image](https://user-images.githubusercontent.com/41268465/117126162-04242f00-adb8-11eb-94dc-93e3236747bc.png)







# Sources/Links –

https://arxiv.org/pdf/1902.04103.pdf

https://openaccess.thecvf.com/content_cvpr_2018/papers/Hu_Relation_Networks_for_CVPR_2018_paper.pdf


https://www.oberlo.in/blog/social-media-marketing-statistics

https://www.lyfemarketing.com/traditional-media-versus-social-media/


https://colab.research.google.com/drive/1BF5HF0EymAfTUyDVi_s2Vo_eE8M3kTcm#scrollTo=FJ2z9TDx7lke


