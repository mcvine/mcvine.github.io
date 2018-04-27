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

# Example 1: CHESS instrument at STS

