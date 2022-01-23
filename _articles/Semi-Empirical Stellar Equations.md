---
title: Semi-Empirical Stellar Equations
date: 2020-02-09 19:30:00 -0800
modified: 2022-01-22 00:24:00 -0700
permalink: /semi-empirical-stellar-equations/
category: Programming
tags: [classification, data, maths, procedural generation, space game]
---

I've spent a lot of time trying to answer certain questions in astronomy, where I just want a rough approximation for the purpose of a simulation, and don't need an exact answer. These are some of the equations I've come up with.

## Yerkes Classes' T/M<sub>v</sub> Relations

These equations are shown as functions where x is temperature in Kelvin, and f(x) is absolute magnitude (visual). Most are valid from 2400 K to a little bit past 30000 K, the exceptions are noted. For the hypergiants and white dwarfs, the range is within an elliptical region, of which these functions define the major axis; for all others, they are a trend line along a Yerkes classification.

- Hypergiants (0):  
  f(x) = -8.9
- Supergiants (Ia):  
  f(x) = -0.00135x<sup>3</sup> + 0.0233x<sup>2</sup> + 0.0187x – 7.349
- Supergiants (Ib):  
  f(x) = 0.00329x<sup>3</sup> – 0.0962x<sup>2</sup> + 0.829x – 7.209
- Bright Giants (II):  
  f(x) = 0.00557x<sup>3</sup> – 0.166x<sup>2</sup> + 1.505x – 6.816
- Giants (III):  
  f(x) = 0.0135x<sup>3</sup> – 0.373x<sup>2</sup> + 3.019x – 7.233
- Subgiants (IV):  
  f(x) = -0.151x<sup>2</sup> + 2.216x – 5.128 _(4450-100000 K **only**)_
- Dwarfs (V):  
  f(x) = 0.00193x<sup>5</sup> – 0.0615x<sup>4</sup> + 0.742x<sup>3</sup> – 4.257x<sup>2</sup> + 12.439x – 12.996 _(note: this one is the least accurate)_
- Subdwarfs (VI):  
  f(x) = 0.131x<sup>3</sup> – 3.275x<sup>2</sup> + 27.576x – 71.7 _(3050-6000 K **only**)_
- White Dwarfs (VII):  
  f(x) = 0.489x + 10.01 _(4450-30000 K **only**)_

---

## Simple Conversions

- Absolute Magnitude (visual) → Luminosity (solar luminosities):  
  L<sub>sun</sub> = 100 \* exp(-0.944 \* M<sub>v</sub>)  
  Accurate between 0-10 M<sub>v</sub>. Probably continues accuracy relatively well.
- Main Sequence Luminosity / Mass Relation:  
  L<sub>star</sub> / L<sub>sun</sub> = (M<sub>star</sub> / M<sub>sun</sub>)<sup>3.5</sup>  
  L<sub>star</sub> = ( 3.68 \* ln(M<sub>star</sub>) – 0.244 )<sup>e</sup>  
  _(The second equation applies to all stars.)_
- Mass / Lifetime Relation:  
  T<sub>years</sub> = ( 23.4 – 2.68 \* ln(M<sub>star</sub>) )<sup>e</sup>  
  _(This applies to all stars.)_

Spectral filters are used to help classify stars. **U**ltraviolet, **B**lue, **V**isual, **R**ed, and **I**nfrared. Objects are listed in different indexes:

- **U**–**V** for the hottest objects (stellar remnants, galaxies)
- **B**–**V** (the majority of stars)
- **R**–**I** for the coolest (LTY "stars" and below)

---

## Equations I no longer recommend

Provided for completeness, in case they are found to be useful.

- Temperature (K) → Absolute Magnitude (visual):  
  M<sub>v</sub> = 35.463 \* exp(-0.000353 \* T)  
  Roughly accurate between 2000-50000 Kelvin. Probably doesn’t continue accuracy at hotter temperatures. Previously this was at the top of this post, now I am not sure why (perhaps the simplicity). The Yerkes' classifications are a better system.
- B-V index (x) → Temperature (K):  
  T = -772.2x<sup>3</sup> + 3152x<sup>2</sup> – 6893x + 9500  
  Sorta accurate between 0-2. (This equation I am least comfortable with, and don't plan to use.)
