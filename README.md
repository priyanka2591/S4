# Assignment 4 - Part 1
The archtiecture of the Artificial neural network (ANN) is as mentioned below <br>
![arch](https://user-images.githubusercontent.com/84949894/119928482-4bf23c80-bf99-11eb-8322-c4c07df2bd19.PNG) <br>

<p align = "center"> Architecture </p>
Number of inputs  - 2 (i1 and i2) <br>
Number of hidden layers  - 1<br>
Number of  neurons in the hidden layers  - 2<br>
Number of output layers - 1<br>
Number of neurons in the output layer  - 2<br>
Number of outputs  - 2 class output<br>

![forward propogation](https://user-images.githubusercontent.com/84949894/119925012-447b6500-bf92-11eb-927c-016924556871.PNG)

<p align = "center"> Forward propogation </p>

1) The above image explains the forward propogation that happens in a neural network given two inputs i1 and i2 <br>
2) Given a feature vector consiting of two inputs i1 and i2 the outputs to the subsequent layer are calculated by multipying the corresponding weights of that particular output neuron to the input vector and then summing it (Dot product).  h1 is calculated by multiplying w1 and w2  with i1 and h2 is calculated by w3 and w4 with i2 . <br>
3) This gives the raw output h1 and h2.<br>
![first inactive layer](https://user-images.githubusercontent.com/84949894/119924917-1433c680-bf92-11eb-92d8-7d0865c72079.PNG) <br>

4) As activation is necessary for non linearity and to add complexity to the equation so that the outputs are not represneted by just a linear combination of the initial layer, a sigmoid activation is added to the outputs h1 and h2 resulting in out_h1 and out_h2 respectively. Sigmoid function is represnted by the formula 1/1+exp(-hi). This pushes the output to be between zero and one. <br>
![active first layer](https://user-images.githubusercontent.com/84949894/119924910-1138d600-bf92-11eb-8ae8-fa36fbe13556.PNG)

5) This forms the first hidden layer
6) Now for the next layer which is the output layer there are two neurons. And the corresponding weights are w5, w6, w7 and w8.
7) The input to the output layer is again calculated as per the logic mentioned in step2 my multiplying the sets of weights with the corresponding inputs and summing it.This way o1 and o2 are calculated.<br>
![rawnoutput](https://user-images.githubusercontent.com/84949894/119924896-08e09b00-bf92-11eb-932d-a2d8d758630a.PNG)

8) Sigmoid Activation is aplied on this output layer as well sig(o1) ->  out_o1 and sig(o2) - > out_o2 <br>
![actoutput](https://user-images.githubusercontent.com/84949894/119924886-054d1400-bf92-11eb-8d6c-8abe2f9ff6b9.PNG)

9) Finally the errors are calculated which is nothing but the difference between what we expect the network to predict (ground truth) and what the network has predicted.<br>
![errorsindv](https://user-images.githubusercontent.com/84949894/119924882-02522380-bf92-11eb-8ecd-5d9779ee6143.PNG)

10) In this case the squared errors are calculated. We are multiplying this error with 0.5 in order to enable easy differentiation of the erros during back propogation


<p align = "center"> Bckward propogation </p> <br>
1) Backward propogation is done by calculating the gradients which is nothing but the differntial of the total loss w.r.t the weights at each layer. <br>
2) This is done in two steps as there are two layers for easy understanding <br>
  a) Calculating hte gradient of the last layer weights (w5, w6, w7 and w8) <br> 
  b) Calculating the gradients of hidden layer weights (w1, w2, w3 and w4) <br>
3) The total loss wrt w5 can be calcualted by differentiating the total loss sequentially back until we reach w5. This is shown by this snippet mentioned below, where total lsos is sum of E1  + E2. The differntial of total loss w.r.t w5 is the sum of differential of E1 w.r.t w5 and differential of E2 w.r.t w5. <br>

![w5loss](https://user-images.githubusercontent.com/84949894/119924855-f8c8bb80-bf91-11eb-8be3-94b5d3e08619.PNG) <br>

4) Here the differential of  E2 wrt w5 is zero as E2 does not receive any input from the w5 weight in the neural network as seen in the initial figure above and hence its differential is zero.Similary later down while calcualting differntial  of E1 w.r.t w8 will alos be zero as E1 does not receive any input via w8 and hence differential = 0. <br>
5) Hence the differential of total loss w.r.t w5 can be represented as the differential of E1 w.r.t w5 which is nothing but the product of the sequential differentials progressing backward along the chain until  we reach w5 as per the chain rule of differentiation. <br>
![chain rule diff](https://user-images.githubusercontent.com/84949894/119925428-0fbbdd80-bf93-11eb-93a8-17451bef5cbd.PNG) <br>

6) In the below image the three values of the three differntial  equations are calculated by substituting the values from the original image. On substituting the values the values are as shown below. <br> 
![3sep](https://user-images.githubusercontent.com/84949894/119924810-e5b5eb80-bf91-11eb-8a99-656a006bcaff.PNG) <br>

7) Hence d(Etotal)/d(w5) is  given by the following after multipying the values after subsituting them in the above equation <br>
![ew5](https://user-images.githubusercontent.com/84949894/119924754-ccad3a80-bf91-11eb-996e-b553d3e1ca67.PNG)<br>

8) Intuitively the differntial of loss w.r.t weights w6, w7 and w8 can be calcuated as mentioned below.<br>
![ew678](https://user-images.githubusercontent.com/84949894/119924777-d6cf3900-bf91-11eb-8512-c0be102ff1e1.PNG)<br>

9) The next step is finding the differential of the total loss w.r.t w1, w2, w3 and w4.<br>
10) Lets start with differential  of the loss w.r.t w1 which can be broken down into the following. Th back propogation upto  the level of w1 is done sequentially backwards from the error till the time we reach w1. The same is repeated for each weights.and broken down sequntially<br>
![first](https://user-images.githubusercontent.com/84949894/119924790-dd5db080-bf91-11eb-8fbf-d27949862bfa.PNG)<br>

11) This is  done as per the chain rule of differentiation. can be further broken down into the following.<br>
![chain rule](https://user-images.githubusercontent.com/84949894/119924723-be5f1e80-bf91-11eb-83d7-cf6097d10b6d.PNG)<br>

12) Step number 10 can further be broken down separtely by susbutituing values in the equation.<br>
13) AS the differnetial chain rule becomes mroe complex each differential right from the loss  till the inital weights have been MANUALLY typed and explained and **NOTHING HAS BEEN LEFT TO INTUITION** They are as shown below<br>
![final](https://user-images.githubusercontent.com/84949894/119924519-5e687800-bf91-11eb-9a19-9be6bdec02b8.PNG)<br>

14) The values in the equation are substituted with the actual values present in the forward propogation screenshot arriving at the final equation as shown above.BAsed on this the random inputs 0.05 and 0.1 are initialized as i1 and i2 with target value of 0.01 and 0.99 respectively and the losses are calulated based on th equations and formulas mentioned above. <br>
15) A total of 181 rows are present where in each subseqient row takes the weights the previous row. The new weights are calculated by the formula 
**new weight = old weight  - learning rate * gradient** <br>
16) The losses are now calulated for the new set of weights to check if the prediction is as close to the ground truth or not.The network is trained for 181 epochs with different learning rates from  [0.1, 0.2, 0.5, 0.8, 1.0, 2.0]  <br>
17) The graphical representationf of the same is as follows <br>

![lr0 1n](https://user-images.githubusercontent.com/84949894/119928067-768fc580-bf98-11eb-89a9-de11342267c9.png)
![lr0 2](https://user-images.githubusercontent.com/84949894/119928069-77285c00-bf98-11eb-80cc-3dce406aa210.png)
![lr0 5](https://user-images.githubusercontent.com/84949894/119928072-77c0f280-bf98-11eb-86e6-07563187ec4a.png)
![lr0 8](https://user-images.githubusercontent.com/84949894/119928074-78598900-bf98-11eb-8ac8-ebc8966c5b9e.png)
![lr1](https://user-images.githubusercontent.com/84949894/119928075-78f21f80-bf98-11eb-82f1-a8ce74966adc.png)
![lr2](https://user-images.githubusercontent.com/84949894/119928063-7394d500-bf98-11eb-85ee-b2be3bc9b38c.png)

18) As seen above as the learning rate increases the slope of the gradient curve steepens and theres is a sharp fall in the loss. However a balance needs to be struck here as there is a very high chances of the gradient descent overshooting the optima minima and it would keep oscillating and would never reach it eventually. Higher learning rate -> less number of epochs. Lower learning rate -> higher number of epochs.


# Assignment 4 - Part 2
1) In this model exercise there are a total of 12 models that have been trained trying to reach an accuracy of 99.4%. However the closest possible accuray to be achieved is 99.28% which 0.12% short of the target.
2) the model architecture is as explained below
3) Functions to laod the MNIST dataset adn to train the model  are already present in the python notebook. the rationale behind choosing this architecture after 10 experimental models is as mentioned below.
4) There are 4 convolutional layers preent. The number of channels / features to be extracted using corresponding kernels are kept to a minimum due to the decreased number of parameters that are required in this scenario. The number of channels are sequentially increased from 10 - 20 - 30 - 40 beore  passing it to the output softmax layer. Batch normalization and pooling is done after every layer. <br>
![cnn](https://user-images.githubusercontent.com/84949894/120039645-e9458300-c022-11eb-91e0-0eb34f536e9f.PNG) <br>

6) Dropout of 0.01 is chosen as the numner of features extracted are very less w.r.t the number of channels, hence losing out on these features wouldnt be ideal and hence a lower drop out value.
7) Max pooling is done from the second layer, as only very basic features are extracted in the first layer. Some amount of feature extraction  is required before we decide on the importance of the features that needs to go through to the next layer.Hence the max pooling is done from layer 2 onwards.
8) AFter the fourth convolutional block the image is then passed through a GAP layer which converts the 2 dimensional image into a single dimsensinal vector. But this however there is an extra dimension which is present in this vector which needs to be removed by using the squeeze() function, so that it can be linked tothe next FC layer. The output of the last cnn layer has a dimension of 3x3, hence the size of the GAP layer also needs to be 3x3 to enable Global average. <br>
![gap](https://user-images.githubusercontent.com/84949894/120040037-843e5d00-c023-11eb-8050-34d9d0e8ff29.PNG) <br>
9) The dropout and the squeeze functionalities are shown below. <br>
![dropout and squeeze](https://user-images.githubusercontent.com/84949894/120040299-e7c88a80-c023-11eb-954a-937854ff4e36.PNG) <br>
11) After this step is done the next step is to pass it through a soft max output which is present in the code already. The losses used here are negative likelihood loss. The optimizer used is SGD which is the gradient descent algorithm. <br>
12) The model  summary is indicated below. There are a total of 18800 paramters with 20 epochs being the maximum number of epoch. The learning rate is 0.01 with SGD as the optimizer as mentioned above. <br>
![summary](https://user-images.githubusercontent.com/84949894/120040511-51e12f80-c024-11eb-86e7-f6bf2942981f.PNG) <br>
13) We reach almost **Near target accuracy** at Epoch 12. <br>
![epoch12](https://user-images.githubusercontent.com/84949894/120040942-14c96d00-c025-11eb-820f-d052dbce20b7.PNG) <br>
15) The total number of models trained are 12. We reached our target model at attempt 11 of model building. (Total  12 models built) <br>





