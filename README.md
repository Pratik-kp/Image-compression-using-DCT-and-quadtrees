# Image-compression-using-DCT-and-quadtrees
Introduction
Image Compression:
Image compression is minimizing the size in bytes of a graphics file without degrading the quality of the image to an unacceptable level. The reduction in file size allows more images to be stored in a given amount of disk or memory space. It also reduces the time required for images to be sent over the Internet or downloaded from Web pages.
Compression:
Compression or bit-rate (no. of bits conveyed per unit of time) reduction involves encoding information using fewer bits than the original representation. Compression can be either lossy or lossless.
Lossless compression:
Lossless data compression is a class of data compression algorithms that allows the original data to be perfectly reconstructed from the compressed data. Lossless compression is preferred for archival purposes and often for medical imaging, technical drawings, clip art or comics.
Lossy compression:
Lossy compression is a data encoding method that compresses data by discarding some of it. The procedure aims to minimize the amount of data that needs to be held, handled, and/or transmitted by a computer.






Image Compression using Discrete Co-sine transformation
Discrete Co-sine transformation: JPEG image compression standard uses Discrete Cosine Transform (DCT). It is a fast transform. It is a widely used and robust method for image compression. It has excellent compaction for highly correlated data. DCT has fixed basis images. It gives good compromise between information packing ability and computational complexity.
Principle of image compression:
(i) Spatial redundancy: which is due to the correlation or dependence between neighbouring pixel values.
(ii) Spectral redundancy: which is due to the correlation between different colour planes or spectral bands.
(iii) Temporal redundancy: which is present because of correlation between different frames in images. Image compression research aims to reduce the number of bits required to represent an image by removing the spatial and spectral redundancies as much as possible.
RD=1-1/CR;
Redundancy:
Redundancy means the data that provides no relevant information.
Data that restates what is already known.
CR-Compression Ratio:
(1) If n1=n2, then CR=1 and hence RD=0 which implies that original image do not contain any redundancy between the pixels.
(2) If n1>>n1, then CR->inf and hence RD>1 which implies considerable amount of redundancy in the original image.
(3) If n1<<n2, then CR>0 and hence RD->Inf which indicates that the compressed image contains more data than original image.
 If n1 and n2 denote the number of information carrying units in original and compressed image respectively

Procedure for compression by DCT:
1. Divide image into 8*8 blocks
-quantization in this example means dropping co-efficients
-co-efficients are dropped based on their magnitude.
DCT 8*8 matrix is :
 

    2. The DCT, applied to 8 x 8 block A, is B=UAUT . We first compute C=UA  and this product is simply an application of U  to each column of A. 
 
3. The DCT B=UAUT  appears below:
 
4. The Discrete Cosine Transformation (DCT) maps the pre-processed 8 x 8 blocks of a digital image to a setting that is more amenable to the coding portion of the image compression algorithm. The reason the DCT is an effective tool in the compression algorithm is that it takes (near) constant blocks and transforms them to new blocks where most of the values are (near) zero.
An Example:
 
5. DCT rounded to two decimal places.
 
6. We are now considering such matrix which when divided gives last elements as zero.
 
Then, we’ll round to nearest integer, we’ll get the given matrix:
                      


7. Now to retrieve the matrix in RCB form , reverse operations are done.
We then multiply element by element of Q to matrix Z.
We then get B’:
 
8. We then obtain an approximation to A by computing the inverse DCT. We have A=UTBU . The matrix A is also displayed below so that you can see the loss in resolution.
 
 

Functions in MATLAB to perform the above operations:
1.	imread():
A = IMREAD(FILENAME,FMT) reads a gray-scale or colour image from the file specified by the string FILENAME. The return value A is an array containing the image data.
If the file contains a gray-scale image, A is an M-by-N array. If the file contains a true color image, A is an M-by-N-by-3 array.


2.	rgb2gray():
I = RGB2GRAY(RGB) converts the true-colour image RGB to the gray-scale intensity image I.
3.	dct2():
B = DCT2(A) returns the discrete cosine transform of A. The matrix B is the same size as A and contains the discrete cosine transform coefficients.

  Image Compression using Quad-trees
Quad tree: A quad-tree is a tree data structure in which each node has exactly four children. Mainly used for compression.





Quad-trees for Image Compression:
•	The quad-tree represents a partition of space in two dimensions by decomposing the region into four equal quadrants, sub-quadrants, and so on with each leaf node containing data corresponding to a specific sub-region.
•	 Each node in the tree either has exactly four children, or has no children (a leaf node). 
•	The height of quad-trees that follow this decomposition strategy (i.e. subdividing sub-quadrants as long as there is interesting data in the sub-quadrant for which more refinement is desired) is sensitive to and dependent on the spatial distribution of interesting areas in the space being decomposed.
•	The Quad tree approach divides a square image into four equal sized square blocks 
•	Tests each block to see if meets some criterion of homogeneity. If a block meets the criterion it is not divided any further, and the test criterion is applied to those blocks.
•	 This process is repeated iteratively until each block meets the criterion. The result may have blocks of several different sizes. 
Algorithm:
1.	Divides the original image using Quad-tree decomposition.
2. Record the values of x and y coordinates, mean value and block size from Quad-tree Decomposition.
3. Record the fractal coding information to complete encoding the image using Huffman coding and calculating the compression ratio.
4. For the encoding image applying Huffman decoding to reconstruct the image and calculating PSNR(Peak Signal to Noise Ratio) which is directly proportional to Compression Ratio.

Huffman Algorithm

This algorithm helps us to reduce the size of the any string because using fixed number of length waste memory. 
Using Fixed length encoding:
 
Number of bits used: 21*3=63 
 
But by using Huffman algorithm 58 bits are used.
The encoding is done in such a way it reduces number of bits used.

Steps to build Huffman tree:
Input is array of unique characters along with their frequency of occurrences and output is Huffman Tree.

1.	Create a leaf node for each unique character and build a min heap of all leaf nodes (Min Heap is used as a priority queue. The value of frequency field is used to compare two nodes in min heap. Initially, the least frequent character is at root).

2.	Extract two nodes with the minimum frequency from the min heap.

3.	Create a new internal node with frequency equal to the sum of the two nodes frequencies. Make the first extracted node as its left child and the other extracted node as its right child. Add this node to the min heap.

4.  Repeat steps#2 and #3 until the heap contains only one node. The remaining node is the root node and the tree is complete.


