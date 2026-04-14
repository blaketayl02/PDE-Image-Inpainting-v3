# PDE-Based Image Inpainting

A from-scratch NumPy implementation of four PDE-based image inpainting models, built as a course project for UBC Mathematics. All solvers are implemented without any inpainting libraries — the PDE discretisation is done explicitly using finite differences.

## Models

| # | Model | PDE | Conductivity $G$ |
|---|-------|-----|-----------------|
| 1 | Harmonic | $\Delta u = 0$ | $G = 1$ |
| 2 | Total Variation (TV) | $\nabla \cdot [G \nabla u] = 0$ | $G = 1/\|\nabla u\|$ |
| 3 | Curvature-Driven Diffusion (CDD) | $\nabla \cdot [G \nabla u] = 0$ | $G = g(\|\kappa\|)/\|\nabla u\|$ |
| 4 | Quick CDD (QCDD) | $\nabla \cdot [G \nabla u] = 0$ | $G = g(\|\kappa\|)$ |

All four models share the same boundary condition: $u = f$ on $\partial\Omega$, where $f$ is the known image and $\Omega$ is the damaged region.

**Interactive painter** (Cell 9.2 in the notebook — HTML5 canvas, works in Colab):
Paint directly over the image in the notebook output, then click **Save Mask**.

## Evaluation Metrics

```python
from utils.metrics import evaluate
evaluate(original, restored, mask, label='Model name')
# prints:  [Model name]   PSNR = 28.14 dB    SSIM = 0.9312
```

- **PSNR** — pixel-level accuracy, computed over the masked region only
- **SSIM** — structural similarity, computed over the full image

## Dependencies

```
numpy
Pillow
scikit-image
matplotlib
```

Install in Colab:
```python
import subprocess
subprocess.run(['pip', 'install', 'scikit-image', '-q'], check=True)
```

## References

- Chan, T.F. & Shen, J. (2001). Non-texture inpainting by curvature-driven diffusions. *Journal of Visual Communication and Image Representation*, 12(4), 436–449.
- Rudin, L., Osher, S. & Fatemi, E. (1992). Nonlinear total variation based noise removal algorithms. *Physica D*, 60, 259–268.
- Xu, Z., Lian, X. & Feng, L. (2008). Image inpainting algorithm based on partial differential equation. *ISECS CCCM*, 120–124.

## AI Declaration:
- AI was used to generate TikZ diagrams
- Improve plot readability
- Explain the code, debug, writing meaningful comments
- Help numerically solve PDEs in Python
