# Tesseract-SinOCR

Fine-tuned [Tesseract](https://github.com/tesseract-ocr/tesseract) models for recognizing single lines of Sinhala text. They were released with the SinFUND and SinOCR datasets (see [SriDoc/datasets](https://github.com/SriDoc/datasets)).

| File | Training data | Printed CER | Handwritten CER |
|---|---|---|---|
| `sin-printed.traineddata` | SinOCR printed training split (90,000 synthetic lines) | 0.1232 | 0.7898 |
| `sin-handwritten.traineddata` | The printed model, then the SinOCR handwritten training split (908 lines) | 0.2693 | 0.7204 |

CER is the character error rate (lower is better). It is measured on the SinOCR printed (10,000 lines) and handwritten (227 lines) test splits. Characters are Unicode code points.

## How the models were trained

Both models start from the Sinhala model in [tessdata_best](https://github.com/tesseract-ocr/tessdata_best). They were fine-tuned with Tesseract 4.1.1 and [tesstrain](https://github.com/tesseract-ocr/tesstrain), using `FINETUNE_TYPE=Impact` and `LANG_TYPE=indic`.

## Usage

Put the `.traineddata` file in a folder and point Tesseract to it. Use `--psm 7` because each image is a single text line:

```bash
tesseract line.png output --tessdata-dir /path/to/folder -l sin-handwritten --psm 7
```

## Limitations

- The models read pre-cropped single lines. They do not find text on a full page.
- The handwritten test split shares writers with the training split. The handwritten CER is therefore probably optimistic for new writers.

## Licence

Apache License 2.0 (see [LICENSE](LICENSE)), the same licence as the `tessdata_best` models that these models were fine-tuned from.

## Citation

Kavishka Gunathilaka, Danusha Hewagama, Supul Pushpakumara, Thanuja D. Ambegoda. *SinFUND and SinOCR: Benchmarks for Sinhala Handwritten OCR and Template-Free Form Understanding*. Preprint, Research Square, 2025. https://doi.org/10.21203/rs.3.rs-6976719/v1
