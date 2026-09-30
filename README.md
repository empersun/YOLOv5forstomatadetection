# Stomatal detection and segmentation (S&D) framework

Model weights and measurement data accompanying *"Rapid Assessment of Stomatal Density Using
Digital Microscopy and Machine Learning"* (Sun, Cordoba Novoa, Hoyos-Villegas & Adamchuk).

## Model weights

| file | architecture | task |
|---|---|---|
| `best.pt` | YOLOv5s | stomata detection (1 class) |
| `best-seg.pt` | YOLOv5s-seg | image-usability segmentation (1 class) |

To use them, clone [Ultralytics YOLOv5](https://github.com/ultralytics/yolov5) and pass the
weight file to `detect.py` or `segment/predict.py`, e.g.

```
python detect.py --weights best.pt --source <image folder> --imgsz 640
python segment/predict.py --weights best-seg.pt --source <image folder> --imgsz 640
```

## Data

| file | contents |
|---|---|
| `stomatal_density_paired.csv` | 119 paired stomatal density measurements from 112 soybean genotypes, taken from symmetrical halves of the same leaves by the nail-polish method and by fresh-leaf digital microscopy. Units: stomata mm<sup>-2</sup>. Genotype identifiers are anonymised. |
| `model_vs_manual_counts.csv` | stomata counted by the S&D model and by a human operator on the same 30 images. |

### Note on the genotype identifiers

The labels `G001`–`G112` in `stomatal_density_paired.csv` are **arbitrary anonymised codes created
for this data release. They are not breeding line designations, they are not real genotype names,
and they carry no relationship to any genotype naming or accession scheme.** Their only function is
to indicate which rows come from the same plant material: seven codes appear twice, corresponding to
independent paired samples of the same genotype, which is why there are 119 measurements from 112
codes. The correspondence between these codes and the original breeding material is held by the
authors and is not published here.

The underlying plant material belongs to the soybean breeding programme of the Department of Plant
Science, McGill University. Requests concerning the material itself should be directed to the
corresponding author.

Raw microscopy images are not included owing to the volume of the image data.

## Regression results reproducible from these files

Fresh-leaf microscopy vs nail-polish method (`stomatal_density_paired.csv`, n = 119):

```
slope      0.8072   (95% CI 0.750 - 0.864)
intercept  56.38    (95% CI 38.2 - 74.6)   stomata mm^-2
R^2        0.8706
residual standard error   29.00 stomata mm^-2
```

S&D model vs manual count (`model_vs_manual_counts.csv`, n = 30):

```
slope      0.9943
intercept  0.0945
R^2        0.9997
residual standard error   0.40 stomata per image
```
