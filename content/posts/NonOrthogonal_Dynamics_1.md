+++
date = '2026-04-30T14:52:28+08:00'
draft = true
title = 'NonOrthogonal_Dynamics_1'
+++


这里我们是想讨论在非厄米情形下探测过程中的噪声放大效应，该效应主要被用来否定有人试图用非厄米EP点来做探测，现在文章的一般认为是EP点的responsivity确实增加，但是sensitivity或者说signal-noise-ratio却没有增加，这里的noise的增加效应其本质上就是非厄米体系中本征态的非正交效应引起的。这里我们想讨论这一点。

## 增强的Responsivity

假如我们考虑的是类似于下面形式的一个非厄米体系，参考文献为[1]

$$\begin{pmatrix}
\omega_{cw} & i\Delta\omega_{EP}/2\\
i\Delta\omega_{EP}/2 & \omega_{ccw}
\end{pmatrix}$$

其能谱为$\omega_\pm = \bar{\omega}\pm \sqrt{\Delta \omega^2-\Delta\omega_{EP}^2}$，其中$\Delta\omega = \omega_{ccw}-\omega_{cw}$。那么对于我们想要进行的探测而言(对于激光陀螺，其原理是测量其内顺时针和逆时针传播的光的拍频，以此确定外界的输入量，因此我们的测量量实际是这个非厄米矩阵的本征谱，而外界的输入其实和$\Delta\omega=\omega_{ccw}-\omega_{cw}$相关)，他的响应是$\dfrac{\partial (\omega_+-\omega_-)}{\partial \Delta\omega}$，计算可以得到信号的增强为

``\dfrac{\Delta \omega_D^2}{\Delta\omega_D^2-\omega_{EP}^2}``

那么这种所谓的响应增强本质上和我们选取的测量方式有关，比如在其他的文献中有其他的对于这种响应的定义方式，比如[2,3]中都是以不同方式来定义的这种响应度的提升。比如设初始的矩阵为，

``H_0=\begin{pmatrix}E_0 & A_0 \\ 0 & E_0\end{pmatrix}``

而我们的扰动矩阵为

``H_1=\epsilon\begin{pmatrix}0 & A_1 \\ B_1 & 0 \end{pmatrix}``

那么我们的谱为$E_\pm = E_0\pm \sqrt{\epsilon A_0B_1 + \epsilon^2 A_1B_1}$，对于一般的非厄米形式的$H_0$，体系的响应就是$\sqrt{\epsilon}$的，要显著强于一般线性响应理论中的$\epsilon$级。


## sensitivity并没有增加

其实我们通过前面的内容大致可以猜到这么一件事，既然对于外界的扰动如此的敏感，那么对于噪声原则上来说是不是也有一样的放大效果？因为本质上如果我们认为存在一个两通道的独立高斯噪声，差不多也就是上面的这种矩阵形式，那么原则上应该也有放大效应。

事实上确实如此，这种对噪声的放大机制原则上就来自于非厄米体系本征态的非正交性。




## 参考文献
[1] Petermann-factor sensitivity limit near an exceptional point in a Brillouin ring laser gyroscope
[2] No exceptional precision of exceptional-point sensors
[3] Sensitivity of parameter estimation near the exceptional point of a non-Hermitian system