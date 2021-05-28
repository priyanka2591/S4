# Assignment 4
The archtiecture of the Artificial neural network (ANN) is as mentioned below

<p align = "center"> Architecture </p>
Number of inputs  - 2 (i1 and i2) <br>
Number of hidden layers  - 1<br>
Number of  neurons in the hidden layers  - 2<br>
Number of output layers - 1<br>
Number of neurons in the output layer  - 2<br>
Number of outputs  - 2 class output<br>
![forward propogation](https://user-images.githubusercontent.com/84949894/119924952-231a7900-bf92-11eb-989c-c91b8efe670b.PNG)

<p align = "center"> Forward propogation </p>

1) The above image explains the forward propogation that happens in a neural network given two inputs i1 and i2 <br>
2) Given a feature vector consiting of two inputs i1 and i2 the outputs to the subsequent layer are calculated by multipying the corresponding weights of that particular output neuron to the input vector and then summing it (Dot product).  h1 is calculated by multiplying w1 and w2  with i1 and h2 is calculated by w3 and w4 with i2 .
3) This gives the raw output h1 and h2.<br>
![first inactive layer](https://user-images.githubusercontent.com/84949894/119924917-1433c680-bf92-11eb-92d8-7d0865c72079.PNG)

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


<p align = "center"> Bckward propogation </p>
1) Backward propogation is done by calculating the gradients which is nothing but the differntial of the total loss w.r.t the weights at each layer.
2) This is done in two steps as there are two layers for easy understanding <br>
  a) Calculating hte gradient of the last layer weights (w5, w6, w7 and w8) <br> 
  b) Calculating the gradients of hidden layer weights (w1, w2, w3 and w4) <br>
3) The total loss wrt w5 can be calcualted by differentiating the total loss sequentially back until we reach w5. This is shown by this snippet mentioned below, where total lsos is sum of E1  + E2. The differntial of total loss w.r.t w5 is the sum of differential of E1 w.r.t w5 and differential of E2 w.r.t w5 <br>
![w5loss](https://user-images.githubusercontent.com/84949894/119924855-f8c8bb80-bf91-11eb-8be3-94b5d3e08619.PNG)

4) Here the differential of  E2 wrt w5 is zero as E2 does not receive any input from the w5 weight in the neural network as seen in the initial figure above and hence its differential is zero.Similary later down while calcualting differntial  of E1 w.r.t w8 will alos be zero as E1 does not receive any input via w8 and hence differential = 0. 

5) Hence the differential of total loss w.r.t w5 can be represented as the differential of E1 w.r.t w5 which is nothing but the product of the sequential differentials progressing backward along the chain until  we reach w5 as per the chain rule of differentiation. <br>
![chain rule diff](https://user-images.githubusercontent.com/84949894/119924816-e8b0dc00-bf91-11eb-95a7-b4c1ce96e6ac.PNG)

6) In the below image the three values of the three differntial  equations are calculated by substituting the values from the original image. On substituting the values the values are as shown below. <br> 
![3sep](https://user-images.githubusercontent.com/84949894/119924810-e5b5eb80-bf91-11eb-8a99-656a006bcaff.PNG)

7) Hence d(Etotal)/d(w5) is  given by the following after multipying the values after subsituting them in the above equation <br>
![ew5](https://user-images.githubusercontent.com/84949894/119924754-ccad3a80-bf91-11eb-996e-b553d3e1ca67.PNG)

8) Intuitively the differntial of loss w.r.t weights w6, w7 and w8 can be calcuated as mentioned below.<br>
![ew678](https://user-images.githubusercontent.com/84949894/119924777-d6cf3900-bf91-11eb-8512-c0be102ff1e1.PNG)

9) The next step is finding the differential of the total loss w.r.t w1, w2, w3 and w4
10) Lets start with differential  of the loss w.r.t w1 which can be broken down into the following. Th back propogation upto  the level of w1 is done sequentially backwards from the error till the time we reach w1. The same is repeated for each weights.and broken down sequntially<br>
![first](https://user-images.githubusercontent.com/84949894/119924790-dd5db080-bf91-11eb-8fbf-d27949862bfa.PNG)

11) This is  done as per the chain rule of differentiation. can be further broken down into the following
![chain rule](https://user-images.githubusercontent.com/84949894/119924723-be5f1e80-bf91-11eb-83d7-cf6097d10b6d.PNG)
12) Step number 10 can further be broken down separtely by susbutituing values in the equation.
13) AS the differnetial chain rule becomes mroe complex each differential right from the loss  till the inital weights have been MANUALLY typed and explained and **NOTHING HAS BEEN LEFT TO INTUITION** They are as shown below
![final](https://user-images.githubusercontent.com/84949894/119924519-5e687800-bf91-11eb-9a19-9be6bdec02b8.PNG)

