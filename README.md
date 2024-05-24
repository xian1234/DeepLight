# DeepLight: Reconstructing High-Resolution Observations of Nighttime Light With Multi-Modal Remote Sensing Data (IJCAI 2024)

This project is the PyTorch implementation of our IJCAI 2024 paper "DeepLight: Reconstructing High-Resolution Observations of Nighttime Light With Multi-Modal Remote Sensing Data".


## General remarks

Nighttime light (NTL) remote sensing observation serves as a unique proxy for quantitatively assessing progress toward meeting a series of Sustainable Development Goals (SDGs), such as poverty estimation, urban sustainable development, and carbon emission. However, existing NTL observations often suffer from pervasive degradation and inconsistency, limiting their utility for computing the indicators defined by the SDGs.

In this research, we present a novel task of reconstructing high-resolution nighttime light images with multi-modality data. To support this research endeavor, we introduce DeepLightMD, a comprehensive dataset comprising data from five heterogeneous sensors, offering fine spatial resolution and rich spectral information at a national scale. Additionally, we present DeepLightSR, a calibration-aware method for building bridges between spatially heterogeneous modality data in the multi-modality super-resolution. 


## Dataset Description

DeepLightMD is a natioanal-scale multimodality SR dataset, consisting of training, validating, and testing material. The training material contains 18,032 pairs of clips, the validating material contains 2,254 pairs of samples. To demonstrate evaluation at both local and regional scale, the testing material contains 2,254 pairs of clips and three province-level samples, covering Anhui, Beijing, and Taiwan. Each pair of clips contains LR NTL (256 × 256 in size), HR NTL (2048 × 2048 in size), DMO (2048 × 2048 in size, 7 bands), DEM (2048 × 2048 in size), and ISP (2048 × 2048 in size).



## Method Description
DeepLightSR framework partitions multi-modality data into four distinct categories, including main modality input (LR NTL), auxiliary modality inputs (DMO and DEM), main modality supervision (HR NTL), and auxiliary modality supervision (ISP). 

DeepLightSR can be optimized with supervision from the HR NTL image $ \boldsymbol{N_H} \in \mathbb {R}^{rh \times rw}$ and auxiliary supervision from the ISP $ \boldsymbol {M_{ISP}} $. Here, $r$, $h$, and $w$ denote the ratio in the SR task, the height, and the width of $ \boldsymbol {N_L} $, respectively. The comprehensive objective function for training DeepLightSR is formulated as follows:

\begin{small}
\begin{equation}
\begin{aligned}
    \boldsymbol {\Theta } = \mathop {\mathrm {argmin}} _{ \boldsymbol {\Theta }} &[ \alpha \mathcal{F}_{1} ||\sum _{j=1}^{m} \beta_{j} (\sum _{i=1}^{n} (\boldsymbol {N}_{L}^{i}, \boldsymbol {M}^{i}; \boldsymbol {\Theta })_{j}-\boldsymbol {N}^{i}_{H,j}||_{1}) + \\
    & (1-\alpha) \mathcal {F}_{2} \sum _{i=1}^{n}(\boldsymbol {M}^{i}_{ISP}\cdot log(\boldsymbol {N}_{G,m}^{i}; \boldsymbol {\Theta }) + \\
    & (1-\boldsymbol {M}^{i}_{ISP})\cdot log(1-(\boldsymbol {N}_{G,m}^{i}; \boldsymbol {\Theta }))],
\end{aligned}
\end{equation}
\end{small}
where $\boldsymbol {\Theta } $ is the parameters of DeepLightSR, the $ n $ and $m$ denote the number of training samples and multiscale outputs, respectively. The $ \boldsymbol {N}_{G,m} \in \mathbb {R}^{rh \times rw} $ represents the obtained SR NTL image in $\mathcal{F}_{1}$. The $\alpha$ and $\beta$ denote the weights of two functions and multiscale tasks.


The codes and datasets are under technical reviewing and will be available soon.
