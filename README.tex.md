# fractals
Mandelbulb fractal 3D in pure Javascript based on [GPU.JS](https://github.com/gpujs/gpu.js)

[Run Mandelbulb!](https://kamil-kielczewski.github.io/fractals/mandelbulb.html)

## Calc Ray

Input parameters ([left-handed coordinate system](https://en.wikipedia.org/wiki/Cartesian_coordinate_system#In_three_dimensions)): 
* $E = [Ex,Ey,Ez]$ - camera (eye) position at point 
* $T= [Tx,Ty,Tz]$ - target point where camera looks  
* $w=[wx,wy,wz]$ - camera vertical normalized vector which idicates where is up and were is down (not shown on picture, usually equal [0,1,0]). 
* $\theta \in [0,360]$ - field of view (slacar value, for human eye $\approx 90^\circ$)
* $k$ - number of pixels on screen width 
* $m$ - number of pixels screen in height 

<p align="center"><img src="/tex/raysMatrix.png" align=middle /></p>

pre-calculations (we can assume that $d=1$ - it doesn't matter siecne $\theta$ determine viewport size)

$$
\begin{align}
t &= T-E \\
t_n &= t/||t|| \\
b &= w\times t \\
b_n &= b/||b|| \\
v_n &= t_n\times b_n \\
g_x &=h_x/2 = d \tan(\theta/2) \\
g_y &=h_y/2 = g_x m/k \\
\end{align}
$$

and (notice: $C=E+t_n$)

$$
\begin{align}
q_x &= \frac{2g_x}{k-1}b_n \\ 
q_y &= \frac{2g_y}{m-1}v_n \\ 
p_{11} &= t_n d - g_xb_n -  g_yv_n \\
\end{align}
$$

Final calculations for ray $r_{ij}$ for each pixel (notice: $P_{ij} &= E + p_{ij}$ )

$$
\begin{align}
p_{ij} &= p_{11} + q_x(i-1) + q_y(j-1) \\
r_{ij} &= p_{ij}/||p_{ij}|| \\
\end{align}
$$




x
