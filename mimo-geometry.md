Projection, Subspaces, MIMO, and Beamforming — A Geometric View of Wireless PHY

Introduction

Modern wireless PHY often appears as a collection of unrelated blocks:

OFDM

matched filtering

correlation

MIMO detection

beamforming

equalization

synchronization

SVD

MMSE/ZF


But underneath these blocks lies a much deeper unifying idea:

> Wireless PHY is fundamentally geometry in high-dimensional signal spaces.



Once this viewpoint becomes clear, many apparently different PHY operations become variations of the same geometric concepts:

projection

orthogonality

basis decomposition

subspace separation

coordinate recovery

directional energy steering


This note summarizes an intuition-first geometric interpretation of modern PHY systems.


---

1. Signals as Vectors

A received signal is not merely a sequence of samples.

It can be viewed as a vector in a complex vector space.

For example:

\mathbf{r} \in \mathbb{C}^N

means the received signal occupies an N-dimensional complex space.

This leads to an important mental model:

signals correspond to vectors/directions

receiver operations become geometric operations

detection becomes a nearest-subspace problem

interference becomes vector overlap

beamforming becomes directional energy steering



---

2. OFDM Basis Functions as Orthogonal Directions

In OFDM, the basis functions are:

\phi_k[n] = e^{j2\pi kn/N}

These are orthogonal basis vectors/functions.

Any OFDM symbol can be represented as:

x[n] = \sum_{k=0}^{N-1} X_k \phi_k[n]

Interpretation:

Mathematical Quantity	Geometric Interpretation

basis functions	orthogonal directions
FFT coefficients	coordinates along those directions


Thus FFT decomposes a signal into coordinates along orthogonal frequency-space directions.


---

3. Projection = Correlation = Matched Filtering

Suppose:

\mathbf{r} = a\mathbf{s} + \mathbf{n}

where:

 is the desired signal direction

 is noise


The receiver computes:

\mathbf{s}^H \mathbf{r}

Geometrically this means:

> “How much of the received vector lies along direction ?”



This is:

projection

correlation

matched filtering


all viewed from different perspectives.


---

4. Why the Matched Filter Uses Time-Reversed Conjugate

In classical DSP, matched filter impulse response is:

h[n] = s^*[-n]

because convolution inherently slides one signal across another.

At the symbol-aligned sampling instant:

y[0] = \sum r[n] s^*[n]

which is exactly:

\mathbf{s}^H \mathbf{r}

Thus:

DSP View	Linear Algebra View

convolution with reversed conjugate	projection / inner product


These are mathematically equivalent.


---

5. Orthogonality and Interference

Suppose two signals:

\mathbf{s}_1, \mathbf{s}_2

If:

\mathbf{s}_1^H \mathbf{s}_2 = 0

then they are orthogonal.

Geometrically:

they occupy different directions

projection onto one removes the other

interference vanishes ideally


This idea appears everywhere:

OFDM subcarriers

CDMA spreading codes

spatial multiplexing

beamforming

SVD eigenmodes



---

6. Signal Subspace vs Noise

Suppose:

\mathbf{r} = a_1\mathbf{s}_1 + a_2\mathbf{s}_2 + \mathbf{n}

Then:

signal occupies the span of 

noise can spread across the entire ambient space


Thus:

Component	Interpretation

signal	structured low-dimensional subspace
noise	distributed across many/all dimensions


Noise does not merely rotate the signal direction.

It adds components outside the signal subspace.

Receiver processing attempts to:

project onto likely signal subspaces

reject orthogonal noise/interference

recover coordinates within the signal space



---

7. MIMO as Geometry

For a MIMO system:

\mathbf{y} = \mathbf{H}\mathbf{x} + \mathbf{n}

The channel matrix  is not merely algebra.

Geometrically:

> Each column of  represents a spatial direction seen by the receiver.



If columns overlap strongly:

streams interfere

channel becomes poorly conditioned

detection becomes difficult


If columns are nearly orthogonal:

streams separate cleanly

spatial multiplexing works efficiently


Thus MIMO detection becomes a geometric subspace-separation problem.


---

8. Zero Forcing as Projection-Based Separation

ZF detector:

\hat{\mathbf{x}} = (\mathbf{H}^H\mathbf{H})^{-1}\mathbf{H}^H\mathbf{y}

Geometrically this means:

1. estimate interfering spatial directions


2. project received vector appropriately


3. remove overlapping components


4. recover coordinates within signal basis



Thus ZF can be interpreted as:

> Orthogonal projection into the estimated signal subspace.




---

9. Beamforming as Directional Projection

Transmit beamforming:

\mathbf{x} = \mathbf{w}s

where:

 is beamforming vector

 is transmitted symbol


Interpretation:

antenna array creates a spatial direction

energy is concentrated into a chosen subspace

receiver observes constructive combination


This leads to a beautiful duality:

Receiver Operation	Transmitter Operation

matched filter projection	beam steering projection


Receiver projects signals onto basis directions.

Transmitter projects energy into basis directions.


---

10. SVD as Natural Spatial Basis Decomposition

SVD decomposition:

\mathbf{H} = \mathbf{U}\mathbf{\Sigma}\mathbf{V}^H

Interpretation:

Quantity	Meaning

columns of 	orthogonal transmit basis directions
columns of 	orthogonal receive basis directions
singular values 	gain of each spatial mode


Suppose:

\mathbf{x} = \sum_i x_i v_i

Then:

H\mathbf{x} = \sum_i \sigma_i x_i u_i

Interpretation:

1. decompose input into orthogonal eigen-directions


2. scale each mode by singular value


3. rotate into output basis



This converts coupled MIMO channels into approximately independent spatial pipes.


---

11. Relationship Between Coordinates and Singular Values

An important distinction:

Quantity	Role

	transmitted coordinate / symbol amplitude
	channel strength of eigenmode


These are fundamentally different.

The singular value is a property of the channel.

The coordinate is determined by transmitted data.

Received mode:

y_i = \sigma_i x_i + n_i

Received power:

|y_i|^2 = \sigma_i^2 |x_i|^2

Thus singular values scale energy in each spatial direction.


---

12. OFDM and SVD — A Deep Connection

OFDM diagonalizes convolution channels.

SVD diagonalizes spatial MIMO channels.

Both transform complicated coupled systems into independent orthogonal modes.

Comparison:

OFDM	MIMO-SVD

Fourier basis	singular-vector basis
subcarriers	spatial eigenmodes
frequency coefficients	spatial coordinates
channel response 	singular values 


This reveals a deeper unifying idea:

> Signal processing often seeks a basis where system behavior becomes simple and decoupled.




---

13. Synchronization as Subspace Alignment

Synchronization problems can also be viewed geometrically.

Examples:

timing estimation

CFO estimation

Doppler estimation

pilot detection

channel estimation


can all be interpreted as:

> Finding the parameterized signal subspace that best explains the received vector.



This connects synchronization, estimation theory, and subspace methods into the same geometric framework.


---

14. A Unified Mental Model of PHY

Instead of viewing PHY as disconnected blocks:

Classical View	Geometric View

correlation	projection
matched filtering	basis alignment
equalization	coordinate recovery
beamforming	directional projection
MIMO detection	subspace separation
MMSE/ZF	optimal projection under noise
synchronization	signal-manifold alignment


Thus modern PHY can be understood as:

> Geometry in noisy high-dimensional signal spaces.




---

15. Why This Perspective Matters

This viewpoint:

simplifies reasoning

unifies many PHY algorithms

improves intuition

bridges theory and implementation

connects naturally to AI/ML representations


It also explains why experienced PHY researchers often think in terms of:

subspaces

manifolds

projections

eigen-structures

information geometry


rather than only equations.


---

16. Suggested Learning Path

Phase 1 — Intuition

Useful topics:

vectors and span

orthogonality

projections

basis transformations

eigenvectors/eigenvalues

SVD intuition


Resources such as 3Blue1Brown provide excellent visual intuition.


---

Phase 2 — Engineering Linear Algebra

Important practical topics:

QR decomposition

least squares

pseudo-inverse

Hermitian matrices

covariance matrices

condition number

rank and null space


These directly connect to:

MIMO detection

MMSE

channel estimation

beamforming



---

Phase 3 — Advanced PHY Geometry

Future advanced topics:

random matrix theory

Grassmannian geometry

convex optimization

subspace tracking

information theory

AI-native adaptive PHY



---

Final Perspective

The major insight is not merely that these mathematical tools exist.

The important realization is:

> Many wireless PHY operations are different geometric manipulations of structured signal subspaces embedded in noisy high-dimensional spaces.



Once this viewpoint becomes natural, modern PHY systems become significantly easier to reason about, extend, and innovate upon.

This geometric interpretation also provides a strong conceptual bridge toward future adaptive and AI-driven wireless receiver architectures.
