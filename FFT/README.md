# Fast Fourier transform
I think the thing should satisfy somethings for being called "transform".
1) If transform is defined, inverse transform should be defined too.
2) Original signal and transformed signal should have one to one correspondence.
3) The transformed signal should be back to original signal by inverse transformed.

For example, Fourier transform, it satisfy all condition described above. It's mathematical properties is not considered for judging that it is "transform" or not.

Fast Frouier transform also should satisfy these conditions for called transformed. And its mathematical properties is other one. But fast fourier transform's goal is to maintain Fourier transform's mathematical properties and modify some point of fourier transform for being used in computer. So it defined as 
<p align="center"> <img src="./img/FFT.png" alt="MLE" width="30%" height="30%"/> </p>

Y(k) is the fast fourier transformed results and, X is the original signal. The difference between fourier tranform and Fast fourier transform is 
1. Computer can't calculate "original integral form", because it can't save continuous data. It dispose of all data like discretized.  

Same points are
1. 간단하게, 위 식에 2번 식의 X(j)의 Y(k)에 1번 식 Y(k)을 대입하면, X(j)가 그대로 나옴을 알 수 있다. 즉, 임의로 결정된 푸리에 변환식에 대해 푸리에 역변환식이 만족해야 하는 조건을 만족했다.
2. 푸리에 변환의 수학적 의의는 신호를 정현파의 결합으로 분해할 수 있음을 의미함으로, 오일러 공식을 이용해 exp(complex)form으로 분해하였다. 따라서, 변환식 및 역변환식에 W_n들의 선형 결합으로 표현되었다.

pf) Discrete Fourier transform, DFT is defined 
<p align="center"> <img src="./img/DFT.png" alt="MLE" width="30%" height="30%"/> </p>
And modify this form for defining FFT.

1. x[n]'s length is N. Therefore x[1] ~ x[N]'s outside x[n] = 0. And  w = k * 2pi / N.  
**NOTE**: Why range is [1,N]? It is same that [0, N-1] and [1, N], considering (j-1)(k-1). Matlab just use [1, N] for matching (j-1)(k-1). 

2. X(e^jw) is defined discrete too. So X(e^jw) = X(e^(j*k*2pi/N)) = Y[k]
**NOTE**: Computer save all of data discrete.

And we get new form
<p align="center"> <img src="./img/FORM.png" alt="MLE" width="50%" height="50%"/> </p>

3. For satisfying transform's defined rule, "new fourier transform" should have "inverse transform" to recover transformed signal to original signal.  
It means x[n] = ifft(fft(x[n]))

**Fast Fourier Transform's ouptut is set X and, it is periodic signal with 2pi.**

## The result of fast fourier transform
Y[k] = X(jw) = [X(j1 * 2pi/N), X(j2 * 2pi/N), ..., X(jN * 2pi/N)] = [Y(1), Y(2), .., Y(N)]. Its length is defined x[n]'s length.


# Edge detection with differentiaton
Using matlab for getting these results

* original image
<p align="center"> <img src="./img/data1.png" alt="MLE" width="60%" height="60%"/> </p>

* image frequency domain and log magnitude with original img
<p align="center"> <img src="./img/frequency_spectrum.png" alt="MLE" width="60%" height="60%"/> </p>

* using differentiation for getting edge
<p align="center"> <img src="./img/img_edge.png" alt="MLE" width="60%" height="60%"/> </p>

* image frequency domain and log magnitude with differentiated img
<p align="center"> <img src="./img/img_diff_spec.png" alt="MLE" width="60%" height="60%"/> </p>

* inserting zero to high frequency's magnitude
<p align="center"> <img src="./img/img_low.png" alt="MLE" width="60%" height="60%"/> </p> 

* inserting zero to low frequency's magnitude
<p align="center"> <img src="./img/img_high.png" alt="MLE" width="60%" height="60%"/> </p> 


# Differentiator
If LTI sysmtem is differentiator, H(jw) is equal to jw.
As w increase, H(jw)'s magnitude also increase. It means input X(jw)'s low frequency is filtered when it is input of H(jw).
One purpose for which differentiating filters are often used is to enhance edges in picture processing.

Images can be thought of x(t1, t2). x means brightness where (t1, t2) are horizontal and vertical coordinates on image's specific position.
We can do 2 dimensional fourier transform this image and get linear combination of e^jw1t1, e^jw2t2.

There is an abrupt variation in brightness across the edge, the frequency content of the edge in the horizontal direction is concentrated at high frequencies.
Differentiator detect sudden changes, so edge is discovered. 
