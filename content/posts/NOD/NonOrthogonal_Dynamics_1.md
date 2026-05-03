+++
date = '2026-04-30T14:52:28+08:00'
draft = true
title = 'NonOrthogonal_Dynamics_1'
+++

# 非厄米 EP 传感中的加性噪声、频率噪声与 Petermann 因子

本文整理非厄米 exceptional point（EP）传感中一个常见但容易混淆的问题：**EP 附近 responsivity 可以增强，但 sensitivity 或 signal-to-noise ratio（SNR）并不一定增强**。其核心原因是，EP 附近本征态的非正交性会放大噪声；在 Brillouin ring laser gyroscope 这类系统中，信号响应增强因子（signal enhancement factor, SEF）与 Petermann 噪声增强因子（Petermann factor, PF）具有相同的发散形式，因此信号和噪声一起增强，基本 SNR 不提升。

本文重点讨论的是**激光自然线宽所对应的加性噪声**：它首先作为 Langevin 噪声加在激光场的复振幅方程中，随后投影成相位噪声，再表现为拍频的频率噪声。它不同于 Hamiltonian 参数本身随机波动所导致的参数噪声。

---

## 1. EP 传感中的增强 responsivity

考虑 Brillouin ring laser gyroscope 文章中使用的两模非厄米 Hamiltonian：

$$
H=
\begin{pmatrix}
\omega_{cw} & i\Delta\omega_{EP}/2\\
i\Delta\omega_{EP}/2 & \omega_{ccw}
\end{pmatrix}.
$$

定义

$$
\bar\omega=\frac{\omega_{cw}+\omega_{ccw}}{2},
\qquad
\Delta\omega_D=\omega_{ccw}-\omega_{cw}.
$$

则 Hamiltonian 可以写成

$$
H=\bar\omega I+\frac{1}{2}
\begin{pmatrix}
-\Delta\omega_D & i\Delta\omega_{EP}\\
i\Delta\omega_{EP} & \Delta\omega_D
\end{pmatrix}.
$$

其两个本征频率为

$$
\omega_\pm=\bar\omega\pm \frac{1}{2}\sqrt{\Delta\omega_D^2-\Delta\omega_{EP}^2}.
$$

因此两条本征模之间的频率劈裂，即实际 beat frequency 对应的分裂量，为

$$
\Delta\omega_S=\omega_+-\omega_-=
\sqrt{\Delta\omega_D^2-\Delta\omega_{EP}^2}.
$$

在激光陀螺中，外界旋转通过 Sagnac 效应改变 cw 与 ccw 模的频率差，即改变 $\Delta\omega_D$。所以小信号响应可以用局部导数表示：

$$
\delta\Delta\omega_S
\approx
\frac{\partial \Delta\omega_S}{\partial \Delta\omega_D}
\delta\Delta\omega_D.
$$

计算得

$$
\frac{\partial \Delta\omega_S}{\partial \Delta\omega_D}
=
\frac{\Delta\omega_D}{\sqrt{\Delta\omega_D^2-\Delta\omega_{EP}^2}}.
$$

文章中定义的 signal enhancement factor 是信号**功率**增强，因此是导数的平方：

$$
SEF=
\left|\frac{\partial \Delta\omega_S}{\partial \Delta\omega_D}\right|^2
=
\frac{\Delta\omega_D^2}{\Delta\omega_D^2-\Delta\omega_{EP}^2}.
$$

这就是 EP 附近 responsivity 增强的来源。

---

## 2. 平方根劈裂与 SEF 的关系

EP 处的本征值响应常被写成平方根形式。例如令

$$
\Delta\omega_D=\Delta\omega_{EP}+\epsilon,
\qquad
0<\epsilon\ll \Delta\omega_{EP},
$$

则

$$
\Delta\omega_S
=
\sqrt{(\Delta\omega_{EP}+\epsilon)^2-\Delta\omega_{EP}^2}
\approx
\sqrt{2\Delta\omega_{EP}\epsilon}.
$$

因此本征值劈裂本身满足

$$
\Delta\omega_S\propto \sqrt{\epsilon}.
$$

但是 SEF 不是劈裂本身，而是局部斜率的平方。由于

$$
\frac{\partial \Delta\omega_S}{\partial \Delta\omega_D}
\approx
\sqrt{\frac{\Delta\omega_{EP}}{2\epsilon}},
$$

所以

$$
SEF\approx \frac{\Delta\omega_{EP}}{2\epsilon}.
$$

因此并不存在矛盾：

- 本征值劈裂：$\Delta\omega_S\sim \sqrt{\epsilon}$；
- 局部振幅增益：$\partial \Delta\omega_S/\partial \Delta\omega_D\sim \epsilon^{-1/2}$；
- 信号功率增强：$SEF\sim \epsilon^{-1}$。

---

## 3. 为什么 sensitivity 不一定增加

实际测量中，输出不是一个无噪声的 $\Delta\omega_S$，而是

$$
\Delta\omega_S^{\mathrm{meas}}(t)
=
\bar{\Delta\omega}_S
+
\delta\Delta\omega_S^{\mathrm{sig}}(t)
+n(t),
$$

其中

- $\bar{\Delta\omega}_S$ 是工作点处的平均拍频；
- $\delta\Delta\omega_S^{\mathrm{sig}}(t)$ 是待测信号引起的输出变化；
- $n(t)$ 是输出拍频本身的随机波动。

若用角频率噪声谱密度 $S_\omega$，在测量带宽 $B$ 内，一个自然的振幅型 SNR 是

$$
\mathrm{SNR}
=
\frac{|\delta\Delta\omega_S^{\mathrm{sig}}|}{\sqrt{S_\omega B}}.
$$

若用普通频率 $\nu=\omega/(2\pi)$，则

$$
\mathrm{SNR}
=
\frac{|\delta\nu_{\mathrm{sig}}|}{\sqrt{S_\nu B}}.
$$

所以，responsivity 增强只说明分子变大；如果输出噪声谱密度 $S_\nu$ 也按同样规律变大，那么 SNR 不会改善。

---

## 4. 两类噪声：参数噪声与加性场噪声

### 4.1 参数噪声：Hamiltonian 自身在抖

参数噪声指系统矩阵的参数本身随时间随机变化。例如

$$
H(t)=H_0+\xi(t)H_{\mathrm{noise}}.
$$

代入动力学方程：

$$
i\dot\Psi=H(t)\Psi
=H_0\Psi+\xi(t)H_{\mathrm{noise}}\Psi.
$$

因为噪声项乘在态矢量 $\Psi$ 上，所以这是**乘性噪声**。例如：

- $\omega_{cw}$ 和 $\omega_{ccw}$ 的温度漂移；
- 泵浦失谐噪声；
- 耦合强度 $\Delta\omega_{EP}$ 的波动；
- Kerr shift 的波动。

这类噪声会通过平方根本征值公式转导到输出拍频：

$$
\Delta\omega_S(t)=
\sqrt{\Delta\omega_D(t)^2-\Delta\omega_{EP}(t)^2}.
$$

若

$$
\Delta\omega_D(t)=D_0+\xi_D(t),
\qquad
\Delta\omega_{EP}(t)=E_0+\xi_E(t),
$$

则一阶展开得

$$
n_{\mathrm{param}}(t)
\approx
\frac{D_0}{\sqrt{D_0^2-E_0^2}}\xi_D(t)
-
\frac{E_0}{\sqrt{D_0^2-E_0^2}}\xi_E(t).
$$

如果只有 $D$ 在抖，则

$$
S_{\omega,\mathrm{param}}^{\mathrm{out}}(\Omega)
=
\frac{D_0^2}{D_0^2-E_0^2}S_D(\Omega)
=
SEF\cdot S_D(\Omega).
$$

这是“参数噪声被局部微分增益放大”。

---

### 4.2 加性场噪声：Hamiltonian 固定，激光场被随机踢动

激光自然线宽不是通常意义上“$\omega_{cw}$ 这个裸参数自己在抖”，而是即使 Hamiltonian 完全固定，激光场的复振幅仍然受到自发辐射等 Langevin 噪声的随机驱动：

$$
i\dot\Psi=H\Psi+\eta(t).
$$

这里 $\eta(t)$ 直接加在方程右端，不与 $\Psi$ 相乘，因此是**加性噪声**。

在相位变量降阶后，这种加性场噪声会表现成有效频率噪声。因此，从现象学上看它像是“瞬时频率在抖”；但从根本动力学上看，它不是 Hamiltonian 参数噪声，而是加性场噪声引起的相位扩散。

---

## 5. 单模激光：从复振幅噪声到频率噪声

### 5.1 最小随机振幅方程

考虑单模激光复振幅 $a(t)$：

$$
\dot a=\left[\frac{G-\kappa}{2}-i\omega_0\right]a+F(t),
$$

其中

- $G$ 是增益；
- $\kappa$ 是损耗；
- $\omega_0$ 是中心角频率；
- $F(t)$ 是加性复 Langevin 噪声。

在稳态激射时，平均上增益与损耗平衡，振幅被钳制在某个稳态值附近。

---

### 5.2 极坐标分解

写成

$$
a(t)=r(t)e^{i\phi(t)}.
$$

则

$$
\dot a=(\dot r+ir\dot\phi)e^{i\phi}.
$$

代回方程并乘以 $e^{-i\phi}$：

$$
\dot r+ir\dot\phi
=
\left[\frac{G-\kappa}{2}-i\omega_0\right]r
+F(t)e^{-i\phi}.
$$

分离实部和虚部：

$$
\dot r= 
\dfrac{G-\kappa}{2}r+\Re\left[F(t)e^{-i\phi}\right],
$$

$$
r\dot\phi=-\omega_0 r+\Im\left[F(t)e^{-i\phi}\right].
$$

这里的频率符号取决于相位约定。若采用 $a=re^{-i\phi}$，符号会反过来。为了突出物理内容，下面写成

$$
\dot\phi(t)
\simeq
\omega_0+\dfrac{1}{r(t)}\Im\left[F(t)e^{-i\phi(t)}\right].
$$

---

### 5.3 振幅钳制极限：有效频率噪声

高于阈值时，振幅涨落相对较小，可令

$$
r(t)\simeq r_0=\sqrt{n_0}.
$$

于是

$$
\dot\phi(t)=\omega_0+
\underbrace{\frac{1}{r_0}\Im\left[F(t)e^{-i\phi(t)}\right]}_{\xi_\phi(t)}.
$$

定义

$$
\xi_\phi(t)=\frac{1}{r_0}\Im\left[F(t)e^{-i\phi(t)}\right],
$$

则瞬时角频率为

$$
\omega_{\mathrm{inst}}(t)=\dot\phi(t)=\omega_0+\xi_\phi(t).
$$

这说明：**加性复振幅噪声在相位方程中表现为有效频率噪声**。

---

### 5.4 噪声强度与相位扩散

假设 $F(t)$ 是圆对称复白噪声：

$$
\langle F(t)F^*(t')\rangle=2D\delta(t-t'),
\qquad
\langle F(t)F(t')\rangle=0.
$$

则相位噪声满足

$$
\langle \xi_\phi(t)\xi_\phi(t')\rangle
=D_\phi\delta(t-t'),
$$

其中量级上

$$
D_\phi\propto \frac{D}{r_0^2}=\frac{D}{n_0}.
$$

这就是 Schawlow--Townes 型线宽公式的基本结构：

$$
\text{相位扩散强度}\propto
\frac{\text{加性噪声强度}}{\text{平均光子数}}.
$$

因此光子数越大，线宽越窄；加性噪声源越强，线宽越宽。

若改用普通频率 $\nu=\omega/(2\pi)$，则

$$
S_\nu=\frac{S_\omega}{(2\pi)^2}.
$$

对白频率噪声，谱线为 Lorentzian，并满足

$$
S_\nu=\frac{1}{\pi}\Delta\nu_{\mathrm{FWHM}},
$$

短时间 Allan deviation 满足

$$
\sigma_\nu(\tau)=\sqrt{\frac{S_\nu}{2\tau}}.
$$

---

## 6. 从单模推广到 cw/ccw 二模拍频测量

### 6.1 二模随机场方程

定义

$$
\Psi=
\begin{pmatrix}
a_{cw}\\
a_{ccw}
\end{pmatrix}.
$$

二模随机方程为

$$
i\dot\Psi=H\Psi+\eta(t),
$$

其中

$$
\eta(t)=
\begin{pmatrix}
\eta_{cw}(t)\\
\eta_{ccw}(t)
\end{pmatrix}.
$$

写成相位形式：

$$
a_{cw}=\sqrt{n_{cw}}e^{i\phi_{cw}},
\qquad
a_{ccw}=\sqrt{n_{ccw}}e^{i\phi_{ccw}}.
$$

---

### 6.2 实际测量量是差相位导数

探测器上测到的是两束激光的拍频。beat note 的相位是

$$
\Phi_b(t)=\phi_{ccw}(t)-\phi_{cw}(t).
$$

因此瞬时拍频为

$$
\omega_b(t)=\dot\Phi_b(t)
=\dot\phi_{ccw}(t)-\dot\phi_{cw}(t).
$$

输出噪声就是差相位导数中的随机部分：

$$
n_\omega(t)=\delta\dot\phi_{ccw}(t)-\delta\dot\phi_{cw}(t).
$$

换成普通频率：

$$
n_\nu(t)=\frac{1}{2\pi}n_\omega(t).
$$

所以，所谓“输出拍频噪声”并不是抽象内部变量，而是实际 beat note 的相位差随时间变化中的随机部分。

---

### 6.3 far from EP：独立噪声近似

在远离 EP 时，两个模式近似为纯 cw 与 ccw 行波。一个自然的最小模型是认为 bare 基底中的原始加性噪声独立：

$$
\langle \eta_i(t)\eta_j^*(t')\rangle
=2D_i\delta_{ij}\delta(t-t'),
\qquad i,j\in\{cw,ccw\}.
$$

这时拍频频率噪声谱近似为

$$
S_{\omega_b}(\Omega)=S_{\omega,cw}(\Omega)+S_{\omega,ccw}(\Omega).
$$

若存在交叉相关，则应写成

$$
S_{\omega_b}(\Omega)
=S_{\omega,cw}(\Omega)+S_{\omega,ccw}(\Omega)
-2\Re S_{\omega,\mathrm{cross}}(\Omega).
$$

因此：

- 如果两路噪声独立，拍频噪声相加；
- 如果存在共模噪声，拍频里可能部分抵消；
- 如果存在反相关噪声，拍频噪声可能更大。

---

## 7. 从双正交展开到非正交噪声放大

### 7.1 带加性噪声的非厄米线性方程

考虑一般非厄米系统

$$
i\frac{d}{dt}\Psi=H\Psi+\eta(t).
$$

设 $H$ 可对角化，右、左本征矢定义为

$$
H|R_\mu\rangle=\Omega_\mu |R_\mu\rangle,
\qquad
\langle L_\mu|H=\Omega_\mu\langle L_\mu|.
$$

采用双正交归一化：

$$
\langle L_\mu|R_\nu\rangle=\delta_{\mu\nu}.
$$

任意态可展开为

$$
|\Psi\rangle=\sum_\mu b_\mu |R_\mu\rangle,
\qquad
b_\mu=\langle L_\mu|\Psi\rangle.
$$

代回随机方程并左乘 $\langle L_\nu|$：

$$
i\dot b_\nu=\Omega_\nu b_\nu+\tilde\eta_\nu(t),
$$

其中

$$
\tilde\eta_\nu(t)=\langle L_\nu|\eta(t)\rangle.
$$

这一步说明：**原始噪声不是直接等于模态噪声，而要先经过左本征态投影。**

---

### 7.2 模态噪声协方差

设原始噪声协方差为

$$
\langle \eta(t)\eta^\dagger(t')\rangle=N\delta(t-t').
$$

则模态噪声协方差为

$$
\langle \tilde\eta_\mu(t)\tilde\eta_\nu^*(t')\rangle
=
\langle L_\mu|N|L_\nu\rangle\delta(t-t').
$$

若原始噪声在 bare 基底中各向同性，

$$
N=2D I,
$$

则

$$
\langle \tilde\eta_\mu(t)\tilde\eta_\nu^*(t')\rangle
=
2D\langle L_\mu|L_\nu\rangle\delta(t-t').
$$

于是：

- 对角项 $\langle L_\mu|L_\mu\rangle$ 放大单模态噪声；
- 非对角项 $\langle L_\mu|L_\nu\rangle$ 使不同模态噪声相关。

这就是非正交性影响加性噪声的最基本公式。

---

### 7.3 从模态噪声到相位扩散

若某个本征模 $\mu$ 激射，写成

$$
b_\mu(t)=\rho_\mu(t)e^{i\phi_\mu(t)}.
$$

它满足

$$
i\dot b_\mu=\Omega_\mu b_\mu+\tilde\eta_\mu(t).
$$

在振幅近似固定 $\rho_\mu\simeq \rho_{\mu,0}$ 的极限下，类似单模推导可得

$$
\dot\phi_\mu(t)
=
\Re\Omega_\mu
+
\frac{1}{\rho_{\mu,0}}
\Im\left[e^{-i\phi_\mu(t)}\tilde\eta_\mu(t)\right].
$$

因此相位扩散强度满足

$$
D_{\phi_\mu}
\propto
\frac{\langle |\tilde\eta_\mu|^2\rangle}{\rho_{\mu,0}^2}
\propto
\frac{\langle L_\mu|L_\mu\rangle}{\rho_{\mu,0}^2}.
$$

这说明非正交性通过增大左本征矢范数来增加相位扩散和线宽。

---

## 8. Petermann 因子

### 8.1 定义

Petermann 因子定义为

$$
K_\mu=
\frac{\langle L_\mu|L_\mu\rangle\langle R_\mu|R_\mu\rangle}
{|\langle L_\mu|R_\mu\rangle|^2}.
$$

在双正交归一化 $\langle L_\mu|R_\mu\rangle=1$ 下，

$$
K_\mu=\langle L_\mu|L_\mu\rangle\langle R_\mu|R_\mu\rangle.
$$

如果进一步令 $\langle R_\mu|R_\mu\rangle=1$，则

$$
K_\mu=\langle L_\mu|L_\mu\rangle.
$$

因此 Petermann 因子的本质是：**它量化了本征态非正交导致的模态噪声与线宽增强。**

在最简线宽表达中可写成

$$
\Delta\nu_\mu=K_\mu\Delta\nu_{\mathrm{orth}},
$$

其中 $\Delta\nu_{\mathrm{orth}}$ 是对应正交模系统中的基准线宽。

---

### 8.2 复对称两模系统中的简化

在许多光学两模系统中，包括这里的 Brillouin gyroscope 模型，Hamiltonian 是复对称的：

$$
H^T=H.
$$

此时右本征矢的转置给出左本征矢的自然形式。若

$$
H|R_\mu\rangle=\Omega_\mu|R_\mu\rangle,
$$

则

$$
\langle R_\mu|^T H=\Omega_\mu\langle R_\mu|^T.
$$

因此可取

$$
\langle L_\mu|
=
\frac{\langle R_\mu|^T}{\langle R_\mu|^T R_\mu\rangle}.
$$

于是

$$
K_\mu=
\frac{\left(\langle R_\mu|R_\mu\rangle\right)^2}
{|\langle R_\mu|^T R_\mu\rangle|^2}.
$$

---

## 9. 对 Brillouin gyroscope 的显式 Petermann 因子推导

### 9.1 Hamiltonian 与本征值差

考虑

$$
H=
\begin{pmatrix}
\omega_{cw} & i\Delta\omega_{EP}/2\\
i\Delta\omega_{EP}/2 & \omega_{ccw}
\end{pmatrix}.
$$

去掉平均频率 $\bar\omega I$，只看 traceless 部分：

$$
H_0=\dfrac{1}{2}
\begin{pmatrix}
-\Delta\omega_D & i\Delta\omega_{EP}\\
i\Delta\omega_{EP} & \Delta\omega_D
\end{pmatrix}.
$$

定义

$$
\Omega=\Delta\omega_S=
\sqrt{\Delta\omega_D^2-\Delta\omega_{EP}^2}.
$$

---

### 9.2 右本征矢

对应上分支的右本征矢可取为

$$
|R_+\rangle=
\begin{pmatrix}
i\Delta\omega_{EP}\\
\Delta\omega_D+\Omega
\end{pmatrix}.
$$

对应下分支可取为

$$
|R_-\rangle=
\begin{pmatrix}
i\Delta\omega_{EP}\\
\Delta\omega_D-\Omega
\end{pmatrix}.
$$

下面以 $R_+$ 为例计算 $K_+$。

---

### 9.3 计算分子：普通 Hermitian 范数

有

$$
\langle R_+|R_+\rangle
=\Delta\omega_{EP}^2+(\Delta\omega_D+\Omega)^2.
$$

利用

$$
\Omega^2=\Delta\omega_D^2-\Delta\omega_{EP}^2,
$$

得到

$$
\langle R_+|R_+\rangle
=2\Delta\omega_D(\Delta\omega_D+\Omega).
$$

---

### 9.4 计算分母：复对称双线性型

复对称情形中需要计算

$$
\langle R_+|^T R_+\rangle.
$$

它等于

$$
\langle R_+|^T R_+\rangle
=(i\Delta\omega_{EP})^2+(\Delta\omega_D+\Omega)^2.
$$

即

$$
\langle R_+|^T R_+\rangle
=-\Delta\omega_{EP}^2+(\Delta\omega_D+\Omega)^2.
$$

同样利用 $\Omega^2=\Delta\omega_D^2-\Delta\omega_{EP}^2$，可化简为

$$
\langle R_+|^T R_+\rangle
=2\Omega(\Delta\omega_D+\Omega).
$$

---

### 9.5 得到 Petermann 因子

因此

$$
K_+=
\frac{\left[2\Delta\omega_D(\Delta\omega_D+\Omega)\right]^2}
{\left[2\Omega(\Delta\omega_D+\Omega)\right]^2}
=
\frac{\Delta\omega_D^2}{\Omega^2}.
$$

代入

$$
\Omega^2=\Delta\omega_D^2-\Delta\omega_{EP}^2,
$$

得到

$$
K_+=
\frac{\Delta\omega_D^2}
{\Delta\omega_D^2-\Delta\omega_{EP}^2}.
$$

同理，

$$
K_-=K_+.
$$

因此该系统的 Petermann 因子为

$$
PF=K_+=K_-=
\frac{\Delta\omega_D^2}
{\Delta\omega_D^2-\Delta\omega_{EP}^2}.
$$

这与该系统的信号功率增强因子相同：

$$
PF=SEF.
$$

---

## 10. 为什么 Petermann 因子在 EP 附近发散

EP 条件为

$$
\Delta\omega_D^2-\Delta\omega_{EP}^2=0.
$$

当系统靠近 EP 时，

$$
\Delta\omega_D^2-\Delta\omega_{EP}^2\to 0^+,
$$

所以

$$
PF=
\frac{\Delta\omega_D^2}
{\Delta\omega_D^2-\Delta\omega_{EP}^2}
\to \infty.
$$

这意味着：

- 两个本征态趋于并合；
- 右本征矢之间越来越不独立；
- 对偶的左本征矢范数越来越大；
- 同样的原始加性噪声被投影到模态坐标时变得更大；
- 最终表现为更强的相位扩散、更宽的线宽，以及更大的白频率噪声谱密度。

---

## 11. 物理直觉：非正交性为什么会放大噪声

### 11.1 正交基底

如果两个模式方向正交，那么一团各向同性的噪声云投影到每个模式方向上，方差不会出现额外放大。

### 11.2 非正交基底

如果两个右本征矢几乎平行，那么为了区分一个态到底沿模式 1 有多少、沿模式 2 有多少，必须使用很长的左本征矢作为对偶投影。

于是同样的噪声 $\eta$ 经过

$$
\tilde\eta_\mu=\langle L_\mu|\eta\rangle
$$

后，会因为 $\|L_\mu\|$ 很大而被放大。

所以 Petermann 因子可以理解为

$$
\boxed{\text{模态分解病态化的几何量化}}.
$$

它不是一个额外人为引入的经验系数，而是非正交本征态的双正交投影自然产生的噪声增强因子。

---

### 11.3 一个二维几何例子

令两个单位右本征矢为

$$
r_1=
\begin{pmatrix}
1\\0
\end{pmatrix},
\qquad
r_2=
\begin{pmatrix}
\cos\theta\\ \sin\theta
\end{pmatrix}.
$$

满足 $l_i^\dagger r_j=\delta_{ij}$ 的左矢可以取为

$$
l_1=
\begin{pmatrix}
1\\ -\cot\theta
\end{pmatrix},
\qquad
l_2=
\begin{pmatrix}
0\\ \csc\theta
\end{pmatrix}.
$$

因此

$$
\|l_1\|^2=\|l_2\|^2=\csc^2\theta=\dfrac{1}{\sin^2\theta}.
$$

当 $\theta\to 0$，两个右本征矢趋于平行，

$$
\|l_i\|^2\sim \frac{1}{\theta^2}\to \infty.
$$

因此同样大小的原始高斯白噪声，在模态坐标中的方差会按 $1/\theta^2$ 放大。

---

## 12. 噪声强度如何确定

### 12.1 微观理论给出

最严格的做法是从激光噪声理论出发，考虑：

- 自发辐射速率；
- 增益介质；
- 腔衰减；
- 热声子或热光子占据数；
- 输出功率；
- Brillouin 增益带宽。

对 Brillouin laser，远离 EP 时的拍频白频率噪声底可看作两束 SBL 激光的 Schawlow--Townes 型线宽贡献之和。

### 12.2 从实验远离 EP 处标定

工程上更常见的是先在远离 EP 的区域测量短时 Allan deviation，提取白频率噪声谱密度 $S_\nu^{(0)}$，然后近 EP 时写成

$$
S_\nu^{\mathrm{out}}
\approx
PF\cdot S_\nu^{(0)},
$$

或使用更精细的 Adler 型修正

$$
S_\nu^{\mathrm{out}}
\approx
NEF\cdot S_\nu^{(0)}.
$$

### 12.3 现象学拟合

也可以把 bare 基底中的噪声协方差写为

$$
\langle \eta(t)\eta^\dagger(t')\rangle=N\delta(t-t'),
$$

其中

$$
N=
\begin{pmatrix}
2D_{cw} & C\\
C^* & 2D_{ccw}
\end{pmatrix}.
$$

然后根据实验测得的线宽、拍频噪声谱或 Allan deviation 去拟合 $D_{cw},D_{ccw},C$。

---

## 13. $a_{cw}$ 与 $a_{ccw}$ 的噪声是否独立

### 13.1 最小模型中可以先假设独立

在 bare cw/ccw 基底中，最简单的假设是

$$
\langle \eta_i(t)\eta_j^*(t')\rangle
=2D_i\delta_{ij}\delta(t-t'),
\qquad i,j\in\{cw,ccw\}.
$$

这意味着两路原始加性噪声近似独立。在远离 EP、两束激光主要受各自独立的自发辐射驱动时，这是合理的第一近似。

### 13.2 真实系统中可能相关

真实系统中可能存在相关噪声来源：

- 共用泵浦；
- 共用腔体温漂；
- Kerr 非线性；
- 模式间耦合；
- 技术噪声。

因此一般应允许

$$
\langle \eta_{cw}(t)\eta_{ccw}^*(t')\rangle\neq 0.
$$

### 13.3 靠近 EP 后，有效模态噪声通常不独立

即使 bare 基底中 $\eta_{cw},\eta_{ccw}$ 独立，变到本征模基底后

$$
\tilde\eta=L^\dagger\eta,
$$

协方差变为

$$
\langle \tilde\eta(t)\tilde\eta^\dagger(t')\rangle
=L^\dagger N L\delta(t-t'),
$$

通常含有非零非对角项。因此：

$$
\boxed{\text{噪声是否独立，必须说明是在 bare 基底还是在本征模基底。}}
$$

---

## 14. 总结

EP 附近的噪声增强可以概括为以下链条：

$$
\text{加性场噪声}
\longrightarrow
\text{相位扩散}
\longrightarrow
\text{频率噪声}
\longrightarrow
\text{拍频噪声}.
$$

非厄米本征态非正交性通过双正交投影进入：

$$
\tilde\eta=L^\dagger\eta,
\qquad
\langle \tilde\eta\tilde\eta^\dagger\rangle=L^\dagger N L.
$$

当系统靠近 EP 时，左本征矢范数增大，模态分解变得病态，因而相同的原始噪声被投影成更大的模态噪声。这个增强由 Petermann 因子量化：

$$
K_\mu=
\frac{\langle L_\mu|L_\mu\rangle\langle R_\mu|R_\mu\rangle}
{|\langle L_\mu|R_\mu\rangle|^2}.
$$

对 Brillouin ring laser gyroscope 的两模模型，

$$
PF=
\frac{\Delta\omega_D^2}
{\Delta\omega_D^2-\Delta\omega_{EP}^2}.
$$

而信号功率增强因子为

$$
SEF=
\left|\frac{\partial\Delta\omega_S}{\partial\Delta\omega_D}\right|^2
=
\frac{\Delta\omega_D^2}
{\Delta\omega_D^2-\Delta\omega_{EP}^2}.
$$

因此在该系统中

$$
PF=SEF.
$$

这意味着 EP 附近输出对待测信号的局部响应确实增强了，但内禀拍频噪声也按同样规律增强。因此，基本 SNR 或 sensitivity 并不会因为单纯靠近 EP 而提升。

### 14.1其他文献

事实上关于这个非厄米系统中的SNR的问题，是有相当的讨论的，我们这里给出几篇文献，其实大致上就这么几种分类，首先是噪声的类型，要么是像我们这里的经典噪声，要么是量子噪声，要么是参数噪声，然后具体分析的量要么是对于复频率的分裂的影响，要么是对可观测量的响应，要么是Fisher信息，结论上都类似，就是EP点附近的敏感度提升可能是有限的。


经典噪声：PT -symmetry breaking in the steady state of microscopic gain±loss systems

量子噪声：Quantum Noise Theory of Exceptional Point Amplifying Sensors



---

## 参考文献

[1] Heming Wang, Yu-Hung Lai, Zhiquan Yuan, Myoung-Gyun Suh, and Kerry Vahala, “Petermann-factor sensitivity limit near an exceptional point in a Brillouin ring laser gyroscope,” *Nature Communications* **11**, 1610 (2020).

[2] Jan Wiersig, “Robustness of exceptional-point-based sensors against parametric noise: The role of Hamiltonian and Liouvillian degeneracies,” *Physical Review A* **101**, 053846 (2020).

[3] W. Langbein, “No exceptional precision of exceptional-point sensors,” *Physical Review A* **98**, 023805 (2018).

[4] C. Chen, L. Jin, and R.-B. Liu, “Sensitivity of parameter estimation near the exceptional point of a non-Hermitian system,” *New Journal of Physics* **21**, 083002 (2019).
