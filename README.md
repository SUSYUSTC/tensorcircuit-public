<p align="center">
  <a href="https://github.com/tencent-quantum-lab/tensorcircuit">
    <img width=90% src="docs/source/statics/logov2.jpg">
  </a>
</p>

<p align="center">
  <!-- tests (GitHub actions) -->
  <a href="https://github.com/tencent-quantum-lab/tensorcircuit/actions/workflows/ci.yml">
    <img src="https://img.shields.io/github/workflow/status/tencent-quantum-lab/tensorcircuit/ci/master?logo=github&style=flat-square&logo=github" />
  </a>
  <!-- docs -->
  <a href="https://tensorcircuit.readthedocs.io/">
    <img src="https://img.shields.io/badge/docs-link-green.svg?style=flat-square&logo=read-the-docs"/>
  </a>
  <!-- PyPI -->
  <a href="https://pypi.org/project/tensorcircuit/">
    <img src="https://img.shields.io/pypi/v/tensorcircuit.svg?style=flat-square&logo=pypi"/>
  </a>
  <!-- License -->
  <a href="./LICENSE">
    <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg?style=flat-square&logo=apache"/>
  </a>
</p>

<p align="center"> English | <a href="README_cn.md"> 简体中文 </a></p>

TensorCircuit is the next generation of quantum circuit simulators with support for automatic differentiation, just-in-time compiling, hardware acceleration, and vectorized parallelism.

TensorCircuit is built on top of modern machine learning frameworks and is machine learning backend agnostic. It is specifically suitable for highly efficient simulations of quantum-classical hybrid paradigm and variational quantum algorithms.

## Getting Started

Please begin with [Quick Start](/docs/source/quickstart.rst).

For more information and introductions, please refer to helpful [example scripts](/examples) and [full documentation](https://tensorcircuit.readthedocs.io/). API docstrings and test cases in [tests](/tests) are also informative.

The following are some minimal demos.

- Circuit manipulation:

```python
import tensorcircuit as tc
c = tc.Circuit(2)
c.H(0)
c.CNOT(0,1)
c.rx(1, theta=0.2)
print(c.wavefunction())
print(c.expectation_ps(z=[0, 1]))
print(c.sample())
```

- Runtime behavior customization:

```python
tc.set_backend("tensorflow")
tc.set_dtype("complex128")
tc.set_contractor("greedy")
```

- Automatic differentiations with jit:

```python
def forward(theta):
    c = tc.Circuit(2)
    c.R(0, theta=theta, alpha=0.5, phi=0.8)
    return tc.backend.real(c.expectation((tc.gates.z(), [0])))

g = tc.backend.grad(forward)
g = tc.backend.jit(g)
theta = tc.array_to_tensor(1.0)
print(g(theta))
```

## Install

The package is purely written in Python and can be obtained via pip as:

```python
pip install tensorcircuit
```

We also have [Docker support](/docker).

## Advantages

- Tensor network simulation engine based

- JIT, AD, vectorized parallelism compatible, GPU support

- Efficiency

  - Time: 10 to 10^6 times acceleration compared to tfq or qiskit

  - Space: 600+ qubits 1D VQE workflow (converged energy inaccuracy: < 1%)

- Elegance

  - Flexibility: customized contraction, multiple ML backend/interface choices, multiple dtype precisions

  - API design: quantum for humans, less code, more power

## Citing TensorCircuit

This project is released by Tencent Quantum Lab and is currently maintained by [Shi-Xin Zhang](https://github.com/refraction-ray) with contributions from the lab and open source community.

If this project helps in your research, please cite our software whitepaper: [TensorCircuit: a Quantum Software Framework for the NISQ Era](https://arxiv.org/abs/2205.10091), which is also a good introduction for the software.

## Contributing

For contribution guidelines and notes, see [CONTRIBUTING](/CONTRIBUTING.md).

We welcome issues, PRs, and discussions from everyone, and these are all hosted on GitHub.

## Researches and Applications

### DQAS

For the application of Differentiable Quantum Architecture Search, see [applications](/tensorcircuit/applications).
Reference paper: https://arxiv.org/pdf/2010.08561.pdf.

### VQNHE

For the application of Variational Quantum-Neural Hybrid Eigensolver, see [applications](/tensorcircuit/applications).
Reference paper: https://arxiv.org/pdf/2106.05105.pdf and https://arxiv.org/pdf/2112.10380.pdf.

### VQEX - MBL

For the application of VQEX on MBL phase identification, see the [tutorial](/docs/source/tutorials/vqex_mbl.ipynb).
Reference paper: https://arxiv.org/pdf/2111.13719.pdf.
