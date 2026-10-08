---
layout: page
title: PAH Emission Spectra
description: a new method for modeling PAH heating and emission in arbitrary radiation environments
img: assets/img/pah_spec.png
importance: 3
category: research
giscus_comments: false
---


Polycyclic aromatic hydrocarbons (PAHs) are small carbonaceous molecules observed in and around galaxies, with spectral emission features that can be dominant in the mid-infrared. With JWST, we can now map PAH emission in unprecedented detail, including in the dusty outflows of nearby galaxies. Interpreting these observations requires models of how PAHs are heated and how they emit. Because PAHs are so small, a single absorbed photon can heat them to high temperatures, after which they cool by emitting in their infrared bands. Computing the resulting emission spectrum normally means solving for the full temperature distribution of each PAH, which is expensive to do for every radiation field of interest.

In [Richie & Hensley (2026)](https://doi.org/10.3847/1538-4357/ae7a42), we take advantage of the single-photon limit for PAH heating and emission. When photon absorptions are rare enough that each one can be treated as an independent event, the emission spectrum becomes a sum over contributions from individual absorbed photons. This means we can precompute a set of **basis spectra**, the emission produced by a PAH of a given size and charge after absorbing a photon of a given wavelength, and then simply scale and sum them to get the emission spectrum for _any_ input radiation field.

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/basis_vector_animation.gif" title="basis spectra animation" class="img-fluid rounded z-depth-1" avoid_scaling=true %}
    </div>
</div>
<div class="caption">
    An illustration of how basis spectra scaled to the input power of the <a href="https://ui.adsabs.harvard.edu/abs/1983A%26A...128..212M/abstract">Mathis, Mezger, and Panagia (1983)</a> Milky Way radiation field contribute to the integrated emission spectra for a 5&nbsp;Å PAH. The resulting spectrum agrees with a full multi-photon calculation to within a few percent.
</div>

This approach agrees with spectra computed with full multi-photon heating to within $$\approx10\%$$ over the 3–20 $$\mu\text{m}$$ range for radiation field intensities $$U<100$$. Because generating a spectrum is fast, it's easy to explore how PAH emission responds to the shape of the radiation field. For example, we find that the 3.3/11.2 $$\mu\text{m}$$ band ratio depends strongly on the hardness of the radiation field, which is important to account for when using band ratios to infer PAH sizes.

### pah_spec

To make this method easy to use, I developed [pah_spec](https://github.com/helenarichie/pah_spec), an open-source Python package for fast, flexible computation of PAH emission spectra with the single photon approximation. Full documentation is available on [Read the Docs](https://pah-spec.readthedocs.io).

The core of the package is the `PahSpec` class. Given a radiation field and size distributions for neutral and ionized PAHs, `PahSpec.generate_spectrum()` combines a precomputed set of basis spectra to return the emission spectrum of both populations. The package can be installed with pip, after which the internal data and sample basis spectra can be downloaded:

```bash
python -m pip install --user git+https://github.com/helenarichie/pah_spec
python -m pah_spec download --to-cache all
```

A minimal example looks something like this:

```python
import pah_spec

ps = pah_spec.PahSpec()

# PAH size distributions for neutral and ionized grains (Draine et al. 2021)
dn_neu, dn_ion = pah_spec.calc_dn(ps.grain_sizes, size_dist="st", ion_frac="st")

# wavelength_arr [um] and u_lambda_arr [erg/cm^4] describe your radiation field
spectrum_neu, spectrum_ion = ps.generate_spectrum(
    wavelength_arr=wavelength_arr,
    u_lambda_arr=u_lambda_arr,
    size_dist_neu=dn_neu,
    size_dist_ion=dn_ion,
)
```

All inputs and outputs are `astropy` quantities, so units are tracked throughout. Example notebooks for [generating spectra](https://github.com/helenarichie/pah_spec/blob/main/examples/generate_spectrum_example.ipynb) and [generating basis spectra](https://github.com/helenarichie/pah_spec/blob/main/examples/generate_basis_spectra_example.ipynb) are included in the repository.

By default, `pah_spec` uses the PAH absorption cross-sections and size distributions of [Draine et al. (2021)](https://ui.adsabs.harvard.edu/abs/2021ApJ...917....3D/abstract). It is also designed to be extensible: users can supply their own functions for absorption cross-sections, vibrational energies, and vibrational mode energies, then use `PahSpec.generate_basis_spectra()` to compute a new set of basis spectra for their own model of PAH physics. See the [customization guide](https://pah-spec.readthedocs.io/en/latest/customization.html) for details.

If you use `pah_spec` in your work, please cite [Richie & Hensley (2026)](https://doi.org/10.3847/1538-4357/ae7a42).
