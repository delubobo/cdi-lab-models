# CDI Lab models

Model files for the instruments at [roylanuzoma.com](https://roylanuzoma.com), published by the Construction Decision Intelligence Lab. The instruments load these files in the visitor's browser.

## site-photo-check

Files for the Site Photo Check instrument, an in-browser detector for people and personal protective equipment in construction site photos.

| File | What it is |
|---|---|
| `yolox_nano_ppe.onnx` | YOLOX-Nano detector. Input 1 x 3 x 416 x 416, BGR, values 0 to 255, letterboxed with gray 114 padding. ONNX opset 11. The output is the raw grid over strides 8, 16, and 32; the caller decodes it and removes overlapping boxes. |
| `classes.json` | The ten class names in output order. |
| `calibration.json` | The map from detector score to confidence, `p = sigmoid(a * logit(s) + b)`, where `s` is objectness times class score, and the two default routing thresholds. |

### Intended use

A demonstration of a method: a small detector, a calibrated confidence, and a rule that reports a detection, routes it to a person, or hides it. It is not a compliance tool. A detection is a prompt for a person to look.

### Limits

- It sees hard hats, safety vests, cones, machinery, vehicles, and people. It does not see harness attachment, edge protection, or whether PPE is worn correctly.
- It can miss missing PPE, most often at distance. A photo with no flag is not a cleared photo.
- It was trained on daytime photos of mostly outdoor sites. Expect weaker results at night, in rain, and on partial views.
- The confidence is calibrated on photos held out from the training dataset. On photos unlike those it can read high.

## Licenses and attribution

- Model weights in this repository: Apache-2.0, see `LICENSE`.
- Architecture, training code, and pretrained starting weights: [YOLOX](https://github.com/Megvii-BaseDetection/YOLOX), Megvii, Apache-2.0.
- Training data: [Construction Site Safety](https://universe.roboflow.com/roboflow-universe-projects/construction-site-safety), Roboflow Universe Projects, version 27, CC BY 4.0.

Cite as: Author's Research, Construction Decision Intelligence Lab, https://roylanuzoma.com

## Versions

Files are served by tag, for example `https://cdn.jsdelivr.net/gh/delubobo/cdi-lab-models@v1/site-photo-check/`. A published tag is not moved; a new model gets a new tag.
