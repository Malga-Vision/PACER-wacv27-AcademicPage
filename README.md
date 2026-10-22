# PACER: Curriculum Self-Training with Spatial Uncertainty

This is the academic project page for the WACV 2027 paper:

**PACER: Curriculum Self-Training with Spatial Uncertainty for Pseudo-Label Selection in Few-Shot Anatomical Landmark Detection**

Project page: https://malga-vision.github.io/PACER-wacv27-AcademicPage/

## Paper Details

- **Venue**: WACV 2027 (Orlando, Florida, January 4-8, 2027)
- **Authors**: Roberto Di Via, Francesca Odone, Vito Paolo Pastore
- **Affiliation**: MaLGa-DIBRIS, University of Genoa, Italy

## Links

- [Code (GitHub)](https://github.com/Malga-Vision/PACER-wacv27)
- Paper, supplementary, poster and video: coming soon

## Abstract

Anatomical landmark detection is bottlenecked by the cost of expert annotation, making the few-shot regime the most relevant setting in practice: a handful of labeled images alongside a larger unlabeled pool. Self-training is a natural framework here, but treating unreliable predictions as pseudo-labels can trigger confirmation bias, and the class-confidence thresholds used in classification have no analogue in dense coordinate regression. We introduce PACER (Percentile-Adaptive Curriculum on Expected Radial Error), a lightweight finetuning stage that mines the unlabeled pool to improve a pre-trained heatmap detector. PACER ranks unlabeled images by the Expected Radial Error (ERE), a label-free, geometry-aware, millimeter-scale uncertainty estimate derived from the predicted heatmaps, and admits them through a percentile gate that expands an easy-to-hard curriculum over the current pool distribution. Because ERE is physically scaled rather than bounded, the gate needs no dataset-specific millimeter threshold and tightens in absolute terms as the detector sharpens, a property a class-probability curriculum cannot have. Across chest, cephalometric, and hand radiographs, comparing only within matched-backbone groups, PACER improves every prior it finetunes: from a plain supervised base it attains the lowest MRE among the pool-only methods sharing that backbone on chest and cephalometric, at a fraction of their cost, and on a recent diffusion-pretrained prior it lowers error on all three benchmarks. The gains are broad and clinically targeted, improving 61 of 62 landmarks at 5 shots and concentrating on the anatomically hardest ones.

## Key Results (5-shot)

- **61 of 62 landmarks improved** across the three benchmarks (chest 6/6, cephalometric 19/19, hand 36/37, the exception unchanged rather than degraded)
- **CDPM-Align + PACER**: best MRE and P95 in its block on every dataset (chest 4.14 → 2.65, cephalometric 2.94 → 2.19, hand 4.19 → 1.40)
- **Lowest pool-only MRE on chest and cephalometric** from the shared ImageNet base (MRE 7.71 and 2.85)
- **Roughly 6× faster** than every SSL baseline (≈35 vs. 210 min on one A30) at lower peak memory

## Method

1. **Expected Radial Error (ERE)**: a label-free, geometry-aware, millimeter-scale uncertainty, the probability-weighted physical distance of heatmap mass from the predicted landmark, averaged over landmarks into one image score
2. **Percentile-adaptive gate**: admits the lowest-ERE fraction of the unlabeled pool, with the induced millimeter threshold read off the current pool rather than chosen in advance
3. **Easy-to-hard curriculum**: the admitted fraction grows linearly over stages (default: 4 stages, up to the whole pool), with pseudo-targets refreshed once per stage; the gate self-tightens in absolute terms as the detector sharpens

## Datasets

- **Shenzhen**: 279 chest radiographs, 6 landmarks (pixels)
- **ISBI2015**: 400 lateral cephalograms, 19 landmarks
- **Digital Hand Atlas (DHA)**: 910 hand radiographs, 37 landmarks

## Website

This page is built using the [Academic Project Page Template](https://github.com/eliahuhorwitz/Academic-project-page-template) and is hosted on GitHub Pages.

## Citation

If you find this work useful, please cite:

```bibtex
@inproceedings{divia2027pacer,
  title     = {{PACER}: Curriculum Self-Training with Spatial Uncertainty for Pseudo-Label Selection in Few-Shot Anatomical Landmark Detection},
  author    = {Di Via, Roberto and Odone, Francesca and Pastore, Vito Paolo},
  booktitle = {Proceedings of the IEEE/CVF Winter Conference on Applications of Computer Vision (WACV)},
  year      = {2027}
}
```

## License

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
