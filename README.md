# Factorization Machine
**Image corruption correction using FunkMF**

Factorization machines are an approach to infer missing data using a loss function (with gradient descent) across the product of 2 different matrices. It is an approach popularized by Simon Funk in 2006 owing to his efforts on the Netflix recommendation prize. The aim of Funk MF is to minimize the error between a synthetic matrix, derived from 2 matrices, and the real data. This is done through the initialized coefficients stored in 2 matrices. Practical uses include restoring image corruption and generating recommendations or suggestions to users based on x and y pairs.

This particular project is an implementation of the same algorithm but in R with a focus on image restoration.
Special thanks to Albert Au Yeung, a very smart computer scientist and machine learning engineer, for writing a tutorial on matrix factorization years ago. The tutorial involved the imputation of a MxN matrix and in python. After reading the wiki math, I had a look at his tutorial in trying to understand how Funk MF worked and found his post. Here, I began to transpose the code into R. 
His tutorial can be found here:

http://albertauyeung.com/2017/04/23/python-matrix-factorization/

**Execution**<br>
Copy the files into a folder, set the parameters of imageFactorization.R to what you require along with the image folder name.
Parameters BLOCKX and BLOCKY determine the x and y dimensions of the size of the blocks you divide your image into.
Therefore, choose values that where your x and y image dimensions are divided, there are no remainders - factors of x and y.
Example, 100x100 image can be divided by 5,10,20,50,100 for x or y. The x and y of the blocks do not need to be the same.
The smaller the blocks, the more sub matrices that can be farmed off to your cpus to process in parallel.
Smaller blocks lead to faster performance but image results degrade in a non linear manner at a very small size.

K is another parameter that impacts performance as this determines the width and high of matrices X and Y (Q and P)
The higher the count, the finer the detail that can be captured from the image.

Execute the script and you should seen an output similar to that of below:

`[1] "Init  10  cpu/s..."`<br/>
`[1] "Loading data..."`<br/>
`[1] "Corrupting data..."`<br/>
`[1] "Plotting corrupted image..."`<br/>
`[1] "Begin main loop..."`<br/>
`[1] "..Dividing image..."`<br/>
`[1] "....Sending off workload to CPUs, tail -f -n 100 cluster.txt"`<br/>
`[1] "....in your image directory to monitor. No feedback in R..."`<br/>
`[1] "Smoothing outlier pixels..."`<br/>
`[1] "Smoothing outlier pixels..."`<br/>
`.........................`<br/>
`[1] "Smoothing outlier pixels..."`<br/>
`[1] "Smoothing outlier pixels..."`<br/>
`[1] "..start imputing pixels back into our corrupted image..."`<br/>
`[1] "..Plot images for comparison..."`<br/>
`[1] "..Write each image to disk at original resolution..."`<br/>
`[1] "Stop the cluster..."`<br/>
`[1] "Done."`<br/>
`[1] 0`<br/>
<br>
After successfully processing the following image<br>
<br>
![Original](https://github.com/RayBosman/FactorizationMachine/blob/master/14.png)<br>
<br>
You should see an output of the following images<br>
<br>
**Corrupted at 33%**<br>
![Corrupted](https://github.com/RayBosman/FactorizationMachine/blob/master/14.png1_14.png_37_0.02_400_20_corrupt.png)

**Synthetic - 400 steps, .02 learning rate, k=20**<br>
![Synthetic](https://github.com/RayBosman/FactorizationMachine/blob/master/14.png1_14.png_37_0.02_400_20_fact.png)

**Corrected**<br>
![Corrected](https://github.com/RayBosman/FactorizationMachine/blob/master/14.png1_14.png_37_0.02_400_20_corrected.png)
