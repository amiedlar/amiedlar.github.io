---
layout: single
title: "Research"
permalink: /research/
author_profile: true
---
{% include base_path %}

## Research Interests

My research is in numerical analysis, with a focus on numerical linear algebra and scientific computing. I develop and analyze algorithms for large-scale matrix and eigenvalue problems: methods that are fast, reliable and backed by rigorous error analysis, and that scale to modern applications and computing architectures.

- **Iterative solvers for large-scale linear algebra problems.** Eigensolvers and linear system solvers for problems too large for direct methods. This includes adaptive finite element methods for PDE eigenvalue problems with reliable a posteriori error estimates; contour-integral and rational-approximation methods for nonlinear eigenvalue problems in acoustics, photonics and electronic structure calculations; and resilient asynchronous solvers for linear systems.
- **Randomized numerical linear algebra.** Randomized low-rank approximation beyond Gaussian random matrices, randomized eigensolvers with probabilistic error analysis, and randomized rounding for tensors in the tensor-train format.
- **Acceleration methods.** Analysis of Anderson-type acceleration and unified frameworks for nonlinear Krylov methods. This is the subject of my NSF CAREER award.
- **Quantum numerical linear algebra.** Numerical linear algebra for quantum algorithms in scientific computing, explored during the IPAM long program on quantum computing and taught as a graduate course at Virginia Tech.
- **Mathematics and the arts.** Interdisciplinary collaborations that bring linear algebra to public audiences, including the CERN–IARI collaboration and CyberArts and ICAT projects at Virginia Tech.

## Funding

### External Funding

{% assign grants = site.data.funding | sort: "end" | reverse %}{% for grant in grants %}{% include rs-cvrow.html item=grant %}{% endfor %}

### Internal Funding

{% assign grants = site.data.internal_funding | sort: "end" | reverse %}{% for grant in grants %}{% include rs-cvrow.html item=grant %}{% endfor %}

## Honors and Awards

{% for award in site.data.awards %}{% include rs-cvrow.html item=award %}{% endfor %}
