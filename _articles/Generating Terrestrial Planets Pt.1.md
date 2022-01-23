---
title: Generating Terrestrial Planets Pt.1
date: 2020-07-29 01:26:00 -0800
modified: 2022-01-23 00:20:00 -0700
permalink: /generating-terrestrial-planets-pt-1/
category: Programming
blags: [planets, procedural generation, space game]
tags: writing/blog/published
---

This is related to [Semi-Empirical Stellar Equations](https://blog.tangentfox.com/semi-empirical-stellar-equations/). I have had some questions easily answered, and others which are difficult or impossible to get the kind of accuracy I want.

I'm going to order what I've learned by the order I am planning to use these equations, marking equations loosely based on empirical data with an asterisk, and double asterisks for things I've completely made up to simplify calculation.

- Radius of Surface\* (R<sub>surface</sub>):  
  5500km mean, 1550km standard deviation
- Density\* \[based on common rock types] (D<sub>planet</sub>):  
  4.7g/cm<sup>3</sup> mean, 0.55g/cm<sup>3</sup> standard deviation
- Volume \[assumes a perfect sphere] (V<sub>planet</sub>):  
  4/3 \* π \* R<sub>surface</sub><sup>3</sup>
- Mass (M<sub>planet</sub>):  
  D<sub>planet</sub> \* V<sub>planet</sub>
- Surface Gravity (g<sub>surface</sub>):  
  6.673×10<sup>-11</sup>Nm<sup>2</sup>kg<sup>-2</sup> * M<sub>planet</sub> / R<sub>surface</sub><sup>2</sup>
- Surface Area \[assumes a perfect sphere]:  
  4 \* π \* R<sub>surface</sub><sup>2</sup>
- Atmospheric Pressure Reduction Rate\*\* (P<sub>r</sub>):  
  P<sub>r</sub> \[unit: none] = -0.00011701572 \[unit: s<sup>2</sup> / m<sup>2</sup>] \* g<sub>surface</sub>
- Atmospheric Halving Height\*\* (h<sub>d</sub>):  
  h<sub>d</sub> \[unit: m<sup>-1</sup>] = ln(2) / P<sub>r</sub>
- Atmospheric Volume at Constant Pressure\*\* (V<sub>sim</sub>):  
  (4/3 \* π \* (R<sub>surface</sub> + h<sub>d</sub>)<sup>3</sup> – V<sub>planet</sub>) \* 2
- Surface Atmospheric Pressure (P<sub>surface</sub>):  
  P<sub>surface</sub> \[unit: kPa] = ???
- Lowest Safe Orbital Height\*\* (h<sub>0</sub>):  
  h<sub>0</sub> \[unit: m] = ln(1.4×10<sup>-11</sup> / P<sub>surface</sub>) / P<sub>r</sub>
- True Atmospheric Volume (V<sub>atm</sub>):  
  4/3 \* π \* (R<sub>surface</sub> + h<sub>0</sub>)<sup>3</sup> – V<sub>planet</sub>

V<sub>sim</sub> exists to support a simulation of an entire planet's atmospheric contents using my [simple fluid simulation](https://blog.tangentfox.com/better-fluid-storage/) mechanic. The magic constant used to calculated P<sub>r</sub> is based on Earth's atmosphere, it can be changed to set an exact "atmospheric height" while maintaining other properties of this simulation.

- Atmospheric Pressure at Altitude\*\* (P<sub>altitude</sub>):  
  P<sub>altitude</sub> \[unit: kPa] = P<sub>surface</sub> \* exp(P<sub>r</sub> \* m<sub>altitude</sub>) \[P<sub>r</sub> may be -P<sub>r</sub>, I don't remember]

This post is obviously incomplete, but it's been a while since I posted anything here, and I felt like I should go ahead and share what I’ve been up to.
