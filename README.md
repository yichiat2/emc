## Effective Mass Calculator

#### Theory

```
Note: Will work in atomic units (a.u.), where: hbar = 1, energy is in Hartrees,
distance is in Bohrs, mass is in electron mass (m0).
```

Effective mass tensor is defined as:  
![Effective Mass Tensor](https://raw.github.com/alexandr-fonari/emc/master/p_ms.gif)

Energy gradient tensor (symmetric) is defined in 3D as follows:  
![Energy Gradient Tensor](https://raw.github.com/alexandr-fonari/emc/master/p_et.png)  
where ```x*, y*, z*``` are cartesian reciprocal directions (see ```EMCcoords.py``` for reference).

Second order derivatives are estimated with ```O(h^4)``` error:  
![2nd Derivative](https://raw.github.com/alexandr-fonari/emc/master/p_2ndd.png)

Mixed second derivatives are estimated also with ```O(h^4)``` error:  
![Mixed 2nd Derivative](http://www.holoborodko.com/pavel/wp-content/ql-cache/quicklatex.com-ead43440eddb0f8db2cc36a1df79c547_l3.svg)

After matrix is built, it is inversed (```DGETRF+DGETRI``` [SO](http://stackoverflow.com/questions/3519959/computing-the-inverse-of-a-matrix-using-lapack-in-c)) and diagonalized (```DGEEV```).

#### Required input files
```inp``` file is **required** and has the following form:  
```
0.000 0.000 0.000   ! K-POINT in reciprocal cartesian, set to Gamma: 3 floats
0.001               ! dk step: 1 float
81                  ! band number, can be VB or CB or whatever you want: 1 integer
V                   ! program, currently support V for VASP and C for crystal: 1 char
```
#### CRYSTAL pecularities