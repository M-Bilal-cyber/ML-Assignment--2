# Assignment 2 - End-to-End Machine Learning Systems

Muhammad Bilal Nawaz | SP24-BSE-070 | AIC354 | Fall 2026

**Current status: both public cloud apps verified on 22 October 2026.** Both notebook first cells contain their live links. Default and changed-input predictions were checked without signing in and matched the saved local models. See `deployment_status.json` and `deployment_evidence/`.

- [Titanic live app](https://ml-assignment--2-gd6kkhysuysojbbvijypvj.streamlit.app/)
- [Heart Disease live app](https://ml-assignment--2-nflehvnfyxcxutzvkm6u8z.streamlit.app/)

## Contents

| Task | Required notebook | Dataset | Saved model | Cloud entry point |
|---|---|---|---|---|
| Titanic | `Titanic/Titanic.ipynb` | `Titanic/data/titanic.csv` | `Titanic/models/model_bundle.pkl` | `Titanic/app.py` |
| Heart Disease | `Heart_Disease/Heart_Disease.ipynb` | `Heart_Disease/data/heart_cleveland.csv` and original UCI file | `Heart_Disease/models/model_bundle.pkl` | `Heart_Disease/app.py` |

Each notebook has saved cell outputs and an HTML reading copy. Each `outputs` directory contains metrics, confusion-matrix/ROC plots, train/test data, predictions and an empty feedback template. The model bundle includes fitted encoders and, for Heart Disease, its fitted imputer/scaler/SVC pipeline.

## Execute on this computer

From PowerShell:

```powershell
cd 'C:\Users\MY PC\Desktop\SPM\ML'
.\.venv\Scripts\python.exe -m notebook submission
```

Open either task notebook, choose a Python kernel using the installed requirements, then **Restart Kernel and Run All Cells**. A custom kernel is unnecessary. Each notebook creates its model, outputs and app again. No live input is needed during Run All; edit the example input in Step 8 to try another prediction.

Start either web app from the ML directory:

```powershell
.\.venv\Scripts\python.exe -m streamlit run submission/Titanic/app.py
.\.venv\Scripts\python.exe -m streamlit run submission/Heart_Disease/app.py --server.port 8502
```

Run those commands in separate terminals to use both apps together. The addresses are normally `http://localhost:8501` and `http://localhost:8502`. Press Ctrl+C in the terminal to stop an app. These local addresses must not be submitted as cloud links.

## Execute after downloading/extracting elsewhere

Use Python 3.14 to match the tested environment. From the folder containing this README:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-notebook.txt
.\.venv\Scripts\python.exe -m notebook
```

Use the environment's Python without activating it. On Linux replace `.venv\Scripts\python.exe` with `.venv/bin/python`. Package pins match the environment that created the included models; avoid silently changing scikit-learn when loading them. Retrain and rerun verification if changing versions.

## Observed results

| Metric | Titanic | Heart Disease |
|---|---:|---:|
| Total rows | 100 | 303 |
| Training / test rows | 80 / 20 | 242 / 61 |
| Test accuracy | 80.00% | 78.69% |
| Positive precision | 100.00% | 82.61% |
| Positive recall | 60.00% | 67.86% |
| Positive F1 | 0.7500 | 0.7451 |
| ROC AUC | 0.8100 | 0.8961 |
| Majority baseline accuracy | 50.00% | 54.10% |

The heart model uses **age, cp, thalach, exang only**. `num > 0` supplies its target and is not an input. The model is educational and has not been clinically validated. Scores describe the fixed held-out split, not guaranteed future accuracy.

## Deploy on Streamlit Community Cloud

1. Sign in to GitHub and create a repository, for example `aic354-assignment2`. Upload the **contents of this submission directory**, preserving the two task directories. Do not upload the enclosing ML environment or personal learning guide.
2. Sign in at https://share.streamlit.io/ and connect the GitHub account. Choose **Create app** and the option to deploy an existing app from GitHub.
3. Select the repository and its actual branch. For Titanic use main file path `Titanic/app.py`; under Advanced settings choose Python **3.14**, then deploy.
4. Create another app using the same repository and branch, with main file path `Heart_Disease/app.py` and the same Python version.
5. Check both build logs for successful startup. Open each public URL in a signed-out/private browser, submit a prediction, and confirm the result matches the same local input. Check both default and changed inputs. Record the URLs and verification date in `deployment_status.json`.
6. Replace the **very first markdown cell** of each notebook with its own working URL, for example `**Live cloud deployment:** [Open Titanic predictor](ACTUAL_URL)`. Use an actual verified URL, not the example text. Preserve executed outputs, then update the HTML reading copies and submission ZIP.
7. Upload code, datasets, notebooks and trained model bundles to Google Classroom as directed by the instructor. The ZIP contains these together; follow any Classroom rules about individual file uploads.

The app code is generated by Step 10 of each notebook. For lasting edits, update that cell as well as the deployed file. `build_notebooks.py` is a development helper outside the submission: rebuilding from it replaces notebook drafts and preserves verified links from `deployment_status.json`.

Official deployment reference: https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/deploy

## Source attribution

- Instructor repository: https://github.com/haqnawaz99/ml-teaching-notebooks, commit `c5f67db8361bd8953c4facf9e5ab98ce9242f314`. Original authors credited by the notebook: Mr. Mohsin Afzal and Dr. Rao Muhammad Adeel Nawab.
- UCI Heart Disease: Janosi, A., Steinbrunn, W., Pfisterer, M., & Detrano, R. (1989). https://doi.org/10.24432/C52P4X. CC BY 4.0. Only processed Cleveland data are used.
- `PROVENANCE.json` records sources, the selected features, the retrieval date and raw-file SHA256 hashes.
- The notebook implementation and documentation were prepared with AI assistance. The supplied teaching code is explicitly credited, and measured results are preserved for review.
