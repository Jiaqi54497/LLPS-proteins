## Skip gram
![图片](https://user-images.githubusercontent.com/82629502/116552625-d197b380-a92b-11eb-8213-74830f95a471.png)
![图片](https://user-images.githubusercontent.com/82629502/116552636-d52b3a80-a92b-11eb-81f7-e0f139cdd081.png)
![图片](https://user-images.githubusercontent.com/82629502/116552651-d78d9480-a92b-11eb-9c66-8f6f49d16bd6.png)
![图片](https://user-images.githubusercontent.com/82629502/116552657-da888500-a92b-11eb-8d91-d20a7e12ba72.png)
![图片](https://user-images.githubusercontent.com/82629502/116552666-dc524880-a92b-11eb-9a3e-8f0ec5661ec8.png)

## Back propogation
* What can a hidden layer do?
![图片](https://user-images.githubusercontent.com/82629502/116553930-399ac980-a92d-11eb-8f67-79d466172e13.png)
* Suppose we have input **x** is an **m** dimensional vector, while output **y** is an **n** dimensional vector.
* We can create an **l** dimensional hidden layer **h**, in which **l** is chosen by the developer.
![图片](https://user-images.githubusercontent.com/82629502/116556216-d199b280-a92f-11eb-8a33-e62b98e0975f.png)
* Now the **j**th component of **h** can be expressed from a sigmoid function of a linear combination of **x**.
* In order to turn an **m** dimensional vector into an **l** dimensional one, the matrix **V** linking between should be __m*l__.
* Similarly, matrix **W** is an __l*m__ and links **h** and **y**.
![图片](https://user-images.githubusercontent.com/82629502/116554824-36540d80-a92e-11eb-9f06-f97241165332.png)
* **d** is the true label of input **x**.
![图片](https://user-images.githubusercontent.com/82629502/116557174-c430f800-a930-11eb-8d9f-78058dc840a9.png)
![图片](https://user-images.githubusercontent.com/82629502/116557306-e6c31100-a930-11eb-9c4b-ee5b1ce2265b.png)
* Then we will find the update rule of **V**.
![图片](https://user-images.githubusercontent.com/82629502/116557562-1eca5400-a931-11eb-9a29-708054d7665c.png)
![图片](https://user-images.githubusercontent.com/82629502/116557744-533e1000-a931-11eb-9f21-c0a2da9697ec.png)
![图片](https://user-images.githubusercontent.com/82629502/116557869-736dcf00-a931-11eb-848b-8626d801c0ae.png)

## Autoencoder
![图片](https://user-images.githubusercontent.com/82629502/116553097-571b6380-a92c-11eb-9749-b25eaefd85c1.png)

https://zhuanlan.zhihu.com/p/68903857

## Random Forest
![图片](https://user-images.githubusercontent.com/82629502/116558346-e70fdc00-a931-11eb-9cee-7b9e28cc0c06.png)
![图片](https://user-images.githubusercontent.com/82629502/116558751-5980bc00-a932-11eb-950b-6761505fdc6d.png)
• Decision Tree algorithm only generate one tree.<br>
• Random Forest can generate multiple trees to improve the generalization ability.<br>
• Random Forest<br>
• Repeat m times<br>
• Randomly draw n samples<br>
• Randomly select p attributes/features when growing the tree<br>
• Ensemble the m trees to predict each sample.<br>
