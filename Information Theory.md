# 1. Introduction
Fundamental Problem of Communication: is accurately or approximately reproducing a selected message at another point

Three Performance Metrics of a Communication System:
- Transmission `Effectiveness` (Efficiency) (有效性) (e.g. Source Coding), is measured by spectrum efficiency
- Transmission `Reliability` (Accuracy) (可靠性) (e.g. Channel Coding) (Errors should be minimized), is measured by transmission error rate
- Transmission `Security` (Safety) (e.g. Data Encryption), is measured by the strength of encryption

Information is the understanding and representation of objective reality

Three Levels of Information:
- Syntactic Information (语法信息) (概率信息)
- Semantic Information (语义信息)
- Pragmatic Information (语用信息)

The message is the carrier of information, and information is contained within the message
The signal is the medium that carries the message, and the message is the specific content of the signal

Channel Encoder: adds redundant symbols
Modulator: converts the output symbols from the encoder into signals that are suitable for transmission over the channel to improve transmission efficiency.

AWGN(additive white Gaussian noise): Gaussian: stochastic process in time domain, the amplitude follows a Gaussian distribution

Decoder: to recover the message from the signal, which includes demodulator, channel decoder, and source decoder.
Destination: the function is to receive the information

## 1.1 Main Problems Studied in Shannon's Information Theory
1. About the Source and the Meaning and Measurement of Information
2. No-loss Source Coding Theorem (Shannon's First Theorem)
3. About the Channel Capacity and Reliable Information Transmission
4. Information Rate Distortion Theory (Theoretical Basis of Data Compression) (Distortion-Limited Source Coding Theorem (Shannon's Third Theorem))


# 2. Measurement of Discrete Information
## 2.1
- `Self-information (自信息)`: I_x(a_i) = -log(P_x(a_i))
- The choice of logarithm base:
  - log_2(x) -> bit
  - ln(x) -> knight (1 knight = 1.443 bits)
  - log_10(x) -> hart (1 hart = 3.32 bits)
- `Joint Self-information`: The self-information of an event x=a_i, y=b_j in the event set XY is `I_XY(a_i, b_j) = -log(P_XY(a_i, b_j))`
- `Conditional Self-information`: Given event y=b_j, the self-information of event x=a_i is `I_X|Y(a_i|b_j) = -log(P_X|Y(a_i|b_j))`
- ```
  I(xy) = I(x) + I(y|x) = I(y) + I(x|y)
  ```
## 2.2 `Mutual Information`
- The mutual information between discrete random events x = a_i and y = b_j is `I_X;Y(a_i; b_j) = log((P_X|Y(a_i|b_j)) / P_X(a_i))`
- Record briefly as `I(x;y) = log(p(x|y) / p(x)) or I(a_i; b_j) = log(p_ij / p_i)`
- Meaning: the information gain of a_i after knowing b_j, or, the decrease in uncertainty of a_i after knowing b_j. Mutual information is the basis of communication.
- ```
  I(x;y) = I(x) - I(x|y)
  ```
- e.g. the sending end sends a_i, and the receiving end receives b_j. P(x∣y)= 1​ if x=y, and P(x∣y) = 0 otherwise. If the channel is ideal, P(x∣y)= 1, then I(x|y) = 0. I(x|y) is the remaining uncertainty about x once y is known.
- Symmetric: I(x;y) = I(y;x)
- Can be either positive or negative
- Cannot exceed the self-information of either event (I(x|y)>=0)

## 2.3 Conditional mutual information
- `I(x;y|z) = log(p(x|yz) / p(x|z))`

## 2.4 Entropy
- Average of self-information
- `H(X) = E_p(x) [I(x)] = -∑_x p(x)log(p(x))`
- Represent the uncertainty of a source
- (Usually the transmission cannot reach the maximum load, the main reasons are: the letters are not equally likely to occur (e.g. 'e' is more likely to appear than 'z'), and the system has memory (e.g. 'o' is usually followed by 'n'))

## 2.5 Conditional Entropy
- `H(Y|X) = E_p(xy) [I(y|x)] = -∑_x ∑_y p(x y) log(p(y|x)) = ∑_x p(x) (-∑_y p(y|x) log(p(y|x))) = ∑_x p(x) H(Y|x)`
- `H(Y|x) = -∑_y p(y|x) log(p(y|x))`

## 2.6 Joint Entropy
- `H(XY) = E_p(xy) [I(xy)] = -∑_x ∑_y p(x y) log(p(x y))`

## 2.7 Properties
- Convex(凸、上凸) function
- Jensen's inequality

## 2.8  Information  Divergence
- `D(p||q) = ∑_x P(x) log(P(x)/Q(x))`
- Define the distance between two probability

## Properties of Entropy
- Symmetric:
- Non-negativity:
- Scalability: lim_ε→0 εlog(ε) = 0, then lim_ε→0 H_(q+1)(p1, p2, ..., pn-ε, ε) = H_q(p1, p2, ..., pn)
- Additivity: `H(XY) = H(X) + H(Y|X), H(X1X2...Xn) = H(X1) + H(X2|X1) + ... + H(Xn|X1X2...Xn-1)`
- Extremum Property
- Deterministic: H(1,0) = H(1,0,0,0,...) = 0
- Convexity
- H(Y|X) ≤ H(Y), equality holds if and only if X and Y are independent
- The joint entropy is less than or equal to the sum of the individual entropies: H(X1X2...Xn) ≤ Σ_(i=1)^n H(X_i)

## Mutual Information between a set X and and event y=bj
I(X; y)=∑_x P(x|y) log(P(x|y)/P(x))

## Mutual Information between two sets X and Y
I(X;Y)=∑_x p(x) I(Y;x)



H(X|Y) 损失的信息量