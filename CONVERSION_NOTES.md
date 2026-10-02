# Conversion notes

This repository was prepared from the supplied notebook without executing the project's
training/evaluation cells.

## Colab -> local replacements

| Original | Local version |
|---|---|
| `google.colab` | removed |
| `drive.mount('/content/drive')` | removed |
| `/content/data/...` | `data/...` / `artifacts/...` |
| `/content/drive/MyDrive/rdd2022_project` | `artifacts/rdd2022_project` |
| `!pip install ...` | `%pip install -r requirements.txt` |
| generated `common.py` on Drive | tracked `src/common.py` |
| generated YAMLs on Drive/`/content` | tracked `configs/*.yaml` |
| `decisions_log.md` on Drive | `docs/decisions_log.md` |

Existing notebook outputs were preserved.
