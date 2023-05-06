Download Link: https://assignmentchef.com/product/solved-ee366-homework-6
<br>
Problem 1 (a) Linear image filters are implemented through 2D convolutions. The convolution operation was defined in class as:

O[<em>u, v</em>] = <sup>X </sup>I[<em>u − i, v − j</em>] K[<em>i, j</em>]<em>, ∀</em>(<em>u, v</em>) <em>∈ </em>I<em>,</em>

(<em>i,j</em>)<em>∈W</em>

where K <em>∈</em>R<sup>w<em>×</em>w </sup>is the convolution kernel. The center of the window and kernel is considered to be coordinate (0<em>, </em>0) and <em>i, j ∈ </em>[<em>−h, h</em>].

Work out (using pen and paper) the 2D convolution for the input image and kernel shown in Figure 1. The output image should be of the same size as the input image. You can choose to find output at the boundary by assuming any of the stated techniques in the slides (zero padding, loop around, etc.)

The convolution formula stated above can also be viewed as a graphical procedure, whose steps are outlined below:

<ol>

 <li>Flip the kernel in both the horizontal and vertical directions about the center pixel.</li>

 <li>Align the now flipped kernel over the input image, such that center pixel of the kernel is aligned with pixel location for which you want to compute output value.</li>

</ol>




<ol start="3">

 <li>Multiply the kernel values with overlapping input values respectively.</li>

 <li>Sum up all the obtained products to find the output value.</li>

</ol>

(b) The kernel of a Gaussian filter is:

G[<em>i, j</em>] = <em>e</em><em>− </em><em><u>i</u></em>22<u>+</u><em>σ</em>2<em><u>j</u></em>2 <em>,</em>

where <em>σ</em><sup>2 </sup>is the variance. As we know the Gaussian function has an infinite support, so we are considering a finite version of the kernel here obtained by truncation, e.g. if we want a 3<em>×</em>3 sized Gaussian kernel, then <em>i, j ∈{−</em>1<em>, </em>0<em>, </em>1<em>}</em>. Using the definition from the previous part, an image can be filtered using a Gaussian kernel as:

O = I <em>∗ </em>G<em>.</em>

An interesting property of the Gaussian kernel is that 2D convolution of an image with the Gaussian kernel can be written as two 1D sequential convolutions, i.e.

O[<em>x, y</em>] = I[<em>x, y</em>] <em>∗ </em>G[<em>x, y</em>] = I[<em>x, y</em>] <em>∗ G</em>[<em>y</em>] <em>∗ G<sup>T </sup></em>[<em>x</em>]<em>,</em>

where <em>G</em>[<em>y</em>] is a vertical 1D Gaussian kernel and <em>G<sup>T </sup></em>(<em>x</em>) is a horizontal 1D Gaussian

kernel . Prove this property, using the definition of 2D con-

volution and 1D convolution.

Note that the order of convolution does not matter because its commutative, i.e. image could be convolved with the horizontal vector first and then with the vertical vector.

2 2D kernels that allow decomposition into 1D kernels are called separable, and kernel matrix in such cases can be written as K = vh<em><sup>T </sup></em>, where v is a column vector and h<em><sup>T </sup></em>is a row vector.

Work out using pen and paper the convolution of the input image from Figure 1 with kernel corresponding to

<em>G</em><em> .</em>

<ul>

 <li>Write a MATLAB function convolve(image,kx,ky) that accepts an input image and two 1D kernels as arguments, and generates a filtered image as an output, assuming that 1D kernels form a separable 2D kernel. You cannot use any MATLAB functions that trivialize this task, e.g. conv2/conv. You may use any method to find the convolution output at the boundary pixels. The MATLAB functions imread,imshow or functions iread,idisp from Corke’s library may be of help here.</li>

 <li>Choose a grayscale image and apply a Gaussian filter of size 5<em>×</em>5 to it. Comment on the output using at max three sentences. Recall that Gaussian kernel is separable, and so you can use an 5 <em>× </em>1 Gaussian kernel using the expression <em>G </em><em><sup>y</sup></em><sup>2 </sup>where <em>y ∈{−</em>2<em>, −</em>1<em>, </em>0<em>, </em>1<em>, </em>2<em>}</em>. Choose <em>σ </em>= 0<em>.</em>83</li>

 <li>Sharpen the same image using the Gaussian kernel.</li>

 <li>An image <em>I</em>(<em>x, y</em>) is a 2D function <em>I </em>: R<sup>2 </sup><em>→ </em> The derivatives of this function can be computed and approximated as:</li>

</ul>

<em>I</em><em>x</em>

<em>I<sub>y </sub></em>(<em>x, y </em>+ 1) <em>− I</em>(<em>x, y − </em>1)] <em>.</em>

Find the kernels (i)<em>k<sub>x </sub>∈</em>R<sup>1<em>×</em>3 </sup>(ii) <em>k<sub>y </sub>∈</em>R<sup>3<em>×</em>1</sup>, such that <em>I<sub>x </sub></em>= <em>I ∗ k<sub>x </sub></em>and <em>I<sub>y </sub></em>= <em>I ∗ k<sub>y </sub></em>.

<ul>

 <li>Write a MATLAB function that accepts an image as an argument and computes</li>

</ul>

q

<em>I<sub>x</sub></em>, <em>I<sub>y </sub></em>, and  <em>I<sub>x</sub></em><sup>2 </sup>+ <em>I<sub>y</sub></em><sup>2 </sup>for this image. The last magnitude is returned as the output image.




<ul>

 <li>Use an original gray-scale image and Gaussian filtered image as inputs to the function in the previous part, and comment on the output for the original image and differences between the two outputs.</li>

</ul>

<table width="656">

 <tbody>

  <tr>

   <td width="83">Problem 2 </td>

   <td width="573">In this problem, you’re going to establish an image segmentation pipeline based exactly on the methods discussed in the class. Your goal in this problem is to have the computer find the answers to the following questions about the included image objects.png:1.   How many objects are in the image?2.   Provide a descriptor for the location of each object in the image.3.   Which object has the largest area?4.   Can question 1 be answered for ducks.png? You can threshold experimentally.5.   If you knew apriori that the image contained geometrical shapes, then can you think of some strategy for determining the shape? (You don’t have to write code)You are to provide your own MATLAB code for the entire pipeline. You cannot use MATLAB functions that trivialize these tasks. Examples of disallowed MATLAB functions include bwconncomp,bwlabel,bwpropfilt,imbinarize,regionprops,visboundaries. Your submission should include code for the following steps:(a)     A threshold˙image MATLAB function that thresholds an image. It should accept an input image and a threshold value as an argument, and return a binary image of same size as output. You don’t have to implement automatic thresholding, and can determine threshold experimentally. The MATLAB functions rgb2gray, imtool, and imhist may be of help here.(b)     A label˙image MATLAB function that accepts the binary image from the previous step as argument and returns a labeled image. Each blob in the image should be assigned a different label, based on 4-connectivity. The MATLAB function label2rgb can help you visualize your labels.(c)     A calculate˙centroids MATLAB function that accepts labeled image from the previous step as an argument and returns a matrix with locations of all centroids in (<em>x, y</em>) format.(d)     Necessary additions to the previous code to answer the questions outlined above.</td>

  </tr>

 </tbody>

</table>