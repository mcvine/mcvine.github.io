class: center, middle

.title[MCViNE]
&nbsp;  
.subtitle[Realistic neutron experiment simulations]
&nbsp;
.center[[{mcvine.org}](http://mcvine.org)]
&nbsp;              
&nbsp;              
&nbsp;              
&nbsp;              
&nbsp;              
.author[Jiao Lin] 
<!--.center[[linjiao.info](http://linjiao.info)]-->
&nbsp;              
.institution[Neutron Data Sciences Group]
&nbsp;  
.institution[Oak Ridge National Lab]
&nbsp;              
.date[May 16, 2018]

        
.footnote[Created with [{Remark.js}](http://remarkjs.com/) using [{Markdown}](https://daringfireball.net/projects/markdown/) +  [{MathJax}](https://www.mathjax.org/)]


---

# Overview

1. Introduction

--

2. Examples
   * Realistic virtual experiments
     * Multiple scattering
   * Resolution functions

--

3. Usage
   * of ready-to-use virtual instruments (Direct Geometry Spectrometers)
   * instrument design and optimization


---

# Introduction

* MCViNE: Monte Carlo **VIrtual Neutron Experiment**

* Monte Carlo neutron ray-tracing simulation software
  - modeling of systems of hierachical structures

* Python/C++

???

* MCViNE is a Monte Carlo neutron ray-tracing software package written in C++,
and wrapped in Python.
* The key feature of MCViNE is that it is intended for realistic simulation 
of experiments, not just the instrument itself.
* We will talk about this in more details, but I want to mention here that 
mcvine models the neutron components in a hierarchical way, which allows for
flexible and powerful simulations.

--

* Website: http://mcvine.org

--

* Development portal: http://github.com/mcvine/devel


---

# Linear pipeline structure in Monte Carlo neutron ray-tracing packages

* Adopted by McStas, Vitess, IDEAS, etc

.center[![:scale 90%](../images/basics/legacy-mc-code-scattering-path.png)]

???
In the late 1990s and early 2000s.

---

# MCViNE: Support of hierarchical structure from the start

* Multiple scattering

.center[![:scale 90%](../images/basics/mcvine-scattering-path.png)]

---

# MCViNE: Support of hierarchical structure from the start

* Sample assembly
  * consists of multiple "neutron-scatterers"

.center[![:scale 50%](../images/basics/sampleassembly.png)]


---

# MCViNE: Support of hierarchical structure from the start

* Neutron scatterer
  * shape and scattering kernels

.center[![:scale 70%](../images/basics/scatterer-scattering-mapto-kernels.png)]


---

# MCViNE: Support of hierarchical structure from the start -- sample

.center[![:scale 85%](../images/basics/composite-sample.png)]


---

# MCViNE: Support of hierarchical structure from the start -- detector system

.center[![:scale 85%](../images/basics/composite-detectorsystem.png)]


---

# Examples
   * Realistic virtual experiments
     * Multiple scattering
   * Resolution functions


---
class: split-50

# Example 1: CHESS instrument at STS

.left-column[
CHESS
* A Time-of-Flight chopper spectrometer at STS
* Better brightness suitable for small samples
* Detector system with tremendous solid-angle coverage

.center[![:scale 50%](../images/CHESS/3D.png)]
]

.right-column[
.center[![:scale 100%](../images/CHESS/H00-slices-CHESS_vs_CNCS.png)]
MCViNE simulations
* Realistic Monte Carlo simulations tracking neutrons from start to end
* Performance of the moderator, guides, sample and detector system are considered
* Simulated data reduced by Mantid
]

---
# Typical simulation procedure

* Simulate incident beam using MCViNE or McStas
--
class: split-60

.right-column[
Energy spectrum

![:scale 70%](../images/ARCS/beam-Ei_100-I_E.png)

Cross section

![:scale 70%](../images/ARCS/beam-Ei_100-crosssection.png)
]

.left-column[
Beam monitors

![:scale 70%](../images/ARCS/beam-Ei_100-monitors.png)
]

---
# Typical simulation procedure

* Simulate incident beam using MCViNE or McStas
* Sample scattering simulation

--
```yaml
name: KVO
chemical_formula: K2V3O8
lattice:
  constants: 8.87, 8.87, 5.2, 90, 90, 90
  basis_vectors:
    - 8.87, 0, 0
    - 0, 8.87, 0
    - 0, 0, 5.2
excitation:
  type: spinwave
  E_Q: 2.563*sqrt(1-(cos(h*pi)*cos(k*pi))**2)
  S_Q: 1
  Emax: 3
orientation:
  u: 1, 0, 0
  v: 0, 1, 0
shape: block width="4.6*cm" height="4.6*cm" thickness="2.3/4*cm"
packing_factor: 0.5
temperature: 300*K
```

???
* shape
* kernel
---
# Typical simulation procedure

* Simulate incident beam using MCViNE or McStas
* Sample scattering simulation
* Detector system simulation -- generate NeXus files -- reduce by Mantid
--
.center[![:scale 85%](../images/basics/composite-detectorsystem.png)]  

---
# Typical simulation procedure

* Simulate incident beam using MCViNE or McStas
* Sample scattering simulation
* Detector system simulation -- generate NeXus files -- reduce by Mantid
  - Detector system specification in Mantid can be converted into MCViNE
    by [mantid2mcvine](https://github.com/mcvine/mantid2mcvine)

.center[![:scale 40%](../images/CHESS/3D.png)]

---
# Typical simulation procedure

* Simulate incident beam using MCViNE or McStas
* Sample scattering simulation
* Detector system simulation -- generate NeXus files -- reduce by Mantid

.center[![:scale 100%](../images/CHESS/H00-slices-CHESS_vs_CNCS.png)]

???
Kernels
* spin-wave kernel
* incoherent elastic line

---
class: split-50

# Example 2: MENUS instrument at STS

"MENUS at the STS will be a transformational high flux versatile multi-scale and multi-modal materials 
engineering beamline with unprecedented new capabilities."

.left-column[
.center[![:scale 90%](../images/MENUS/schematic.png)]
]

.right-column[
.center[![:scale 60%](../images/MENUS/mantid_instrument_view.png)]
]