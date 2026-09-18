# GAMESS-MO-Projector

6-31G → def2-TZVP Molecular-Orbital Projection Tool for GAMESS

**Purpose.** Generate a def2-TZVP initial guess (GAMESS (US) `$VEC` for `MOREAD`) by projecting a converged 6-31G molecular-orbital set onto the def2-TZVP basis. This steers the def2-TZVP SCF toward the physically correct electronic state and avoids convergence onto spurious solutions (e.g., open-shell orbitals localizing on ligands instead of the metal).

**Method.** For a fixed nuclear geometry, the 6-31G MO coefficients `C_s` are projected onto the def2-TZVP basis by least-squares fitting of each MO:

$$ C_{\mathrm{def2}} = S_{\mathrm{def2}}^{-1}\, S_{\mathrm{cross}}\, C_{\mathrm{6\text{-}31G}} $$

where `S_def2` is the def2-TZVP overlap matrix and `S_cross` is the cross-overlap between the def2-TZVP and 6-31G basis functions. All matrices are evaluated in a unit-normalized Cartesian representation and reordered between the GAMESS and PySCF basis-function conventions.

**Validation built in.** Before projecting, the tool verifies that the input 6-31G `$VEC` is orthonormal under the reconstructed overlap ($\lVert C^{\mathsf T} S\, C - I\rVert_\infty$ below a threshold). This confirms that the GAMESS↔PySCF basis-ordering and normalization maps are correct for every element present, and halts otherwise.

**Scope of this version.** 6-31G → def2-TZVP, Cartesian Gaussians (6d, 10f). Reusable for any geometry/conformer with the same element set. For a new element, add its `ATOMIC BASIS SET` block; the built-in check will stop if the mapping is not valid.

---
### License
MIT License — Copyright (c) 2026 Hiroshi Sakiyama. See the `LICENSE` file.

### Citation
If you use this tool, please cite the accompanying paper (details to be completed upon publication) and, if applicable, the archived code DOI.

### Dependencies (tested)
Python 3.12, PySCF 2.14.0, NumPy 2.4.4.
