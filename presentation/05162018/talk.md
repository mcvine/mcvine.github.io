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

        
.footnote[Created with [{Remark.js}](http://remarkjs.com/) using [{Markdown}](https://daringfireball.net/projects/markdown/) +  [{katex}](https://github.com/Khan/KaTeX/)]


---

# Overview

1. Introduction

--

2. Examples
   * Realistic virtual experiments
     * Inelastic: direct geometry spectrometers
     * Elastic: engineering diffractometers
     * Multiple scattering
   * Resolution functions for DGS experiments
     * Powder
     * Single crystal
.hidden[* Super resolution phonon Density of States]
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

# MCViNE: Support hierarchical structure

* Multiple scattering

.center[![:scale 90%](../images/basics/mcvine-scattering-path.png)]

---

# MCViNE: Support hierarchical structure

* Sample assembly
  * consists of multiple "neutron-scatterers"

.center[![:scale 50%](../images/basics/sampleassembly.png)]


---

# MCViNE: Support hierarchical structure

* Neutron scatterer
  * shape and scattering kernels

.center[![:scale 70%](../images/basics/scatterer-scattering-mapto-kernels.png)]

???
* Should add a slide for Constructive Solid Geometery

---

# MCViNE: Support hierarchical structure -- sample

.center[![:scale 85%](../images/basics/composite-sample.png)]


---

# MCViNE: Support hierarchical structure -- detector system

.center[![:scale 85%](../images/basics/composite-detectorsystem.png)]

---
# MCViNE: Support hierarchical structure

Publication: [Lin J.Y.Y et al., MCViNE – An object oriented Monte Carlo neutron ray tracing simulation package](http://dx.doi.org/10.1016/j.nima.2015.11.118)


---

# Examples

   * Realistic virtual experiments
     * Inelastic: direct geometry spectrometers
     * Elastic: engineering diffractometers
     * Multiple scattering
     
   * Resolution functions for DGS experiments
     * Powder
     * Single crystal
.hidden[* Super resolution phonon Density of States]


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

.reference[
[Sala G. et al., Conceptual design of CHESS, a new direct‐geometry inelastic neutron spectrometer dedicated to studying small samples](https://doi.org/10.1107/S1600576718002224)
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
.center[![:scale 50%](../images/basics/sampleassembly.png)]

---
# Typical simulation procedure

* Simulate incident beam using MCViNE or McStas
* Sample scattering simulation

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
class: split-50

# Typical simulation procedure

* Simulate incident beam using MCViNE or McStas
* Sample scattering simulation
* Detector system simulation -- generate NeXus files -- reduce by Mantid
  - Detector system specification in Mantid can be converted into MCViNE
    by [mantid2mcvine](https://github.com/mcvine/mantid2mcvine)

.left-column[
.center[![:scale 60%](../images/CHESS/3D.png)]
]

.right-column[
&nbsp;
.center[![:scale 55%](../images/CHESS/Mantid_instrument_view.png)]
]


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
# More DGS examples

See http://mcvine.org/examples.html

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

---
class: split-50
# Example 2: MENUS instrument at STS

* Ni3Al
* Kernel: powder diffraction
* MENUS boosts intensities at long-wavelengths

.left-column[
.center[![:scale 90%](../images/MENUS/Ni3Al-Vulcan.png)]
]

.right-column[
.center[![:scale 90%](../images/MENUS/Ni3Al-MENUS.png)]
]

???
* high flux, wide Q coverage
* strain/phase-transition/texture evolution in 3 orthogonal axes
* Ni3Al diffraction peaks: https://jupyter.sns.gov/user/lj7/notebooks/simulations/MENUS/sample-fccNi/create.ipynb

---
class: split-50
# Example 2: MENUS instrument at STS

* Ni3Al
* Kernel: powder diffraction
* MENUS high resolution mode good for resolving superlattice peaks

.left-column[
.center[![:scale 90%](../images/MENUS/resolution_comparison.png)]
]

.right-column[
.center[![:scale 90%](../images/MENUS/diffraction_peaks_200_MENUS.png)]
]

---
# Multiple scattering

.center[![:scale 50%](../images/basics/sampleassembly.png)]

---
# Multiple scattering - MICAS furnace

.center[![:scale 40%](../images/MICAS/schematic.png)]

???
# Multiple scattering - MICAS furnace

.center[![:scale 40%](../images/MICAS/schematic-cans-only.png)]


---
# Multiple scattering - MICAS furnace

.center[![:scale 40%](../images/MICAS/SCAD.png)]

---
class: split-60
# Multiple scattering - MICAS furnace

.left-column[
![:scale 100%](../images/MICAS/IQE_exp_vs_sim.png)
]

.right-column[

* Top: experimental 
* Middle: simulation without multiple-scattering (MS)
* Bottom: simulation with MS

&nbsp;

&nbsp;

&nbsp;

&nbsp;


* Left: without collimator
* Right: with collimator
]


.reference[
[Niedziela J.L. et al., Design and operating characteristic of a vacuum furnace for time-of-flight inelastic neutron scattering measurements](https://doi.org/10.1063/1.5007089)
]

---
# Examples

   * Realistic virtual experiments
     * Inelastic: direct geometry spectrometers
     * Elastic: engineering diffractometers
     * Multiple scattering
     
   * **Resolution functions for DGS experiments**
     * Powder
     * Single crystal
.hidden[* Super resolution phonon Density of States]

---
# Resolution - \\(^4 \mathrm{He}\\) measurement at ARCS

---
# Usage

   * of ready-to-use virtual instruments (Direct Geometry Spectrometers)
   * instrument design and optimization

---
# Usage

   * of ready-to-use virtual instruments (Direct Geometry Spectrometers)

Start from here: http://mcvine.org/usage.html

