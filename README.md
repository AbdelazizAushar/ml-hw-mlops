# FITE Classification Challenge

This project demonstrates dataset versioning and reproducibility using Git and DVC.

## Repository Structure

```
.
├── data/               # Dataset (managed by DVC)
├── notebooks/          # Jupyter notebooks
├── .dvc/               # DVC configuration
├── data.dvc            # Dataset metadata
├── requirements.txt
└── README.md
```

---

## Requirements

- Python 3.12+
- Git
- DVC


## Clone the project

```bash
git clone https://github.com/AbdelazizAushar/ml-hw-mlops.git
cd ml-hw-mlops
```

---

Install dependencies

```bash
pip install -r requirements.txt
```

---

## Configure Google Drive Authentication

The project uses a shared Google Drive folder as the DVC remote.

Each collaborator must create a local DVC configuration containing the Google OAuth credentials.

Run:

```bash
dvc remote modify --local storage gdrive_client_id YOUR_CLIENT_ID
dvc remote modify --local storage gdrive_client_secret YOUR_CLIENT_SECRET
```

These credentials are stored locally in:

```
.dvc/config.local
```

This file is ignored by Git and must never be committed.

---

## Download the dataset

```bash
dvc pull
```

if you encounter error like `"module 'lib' has no attribute 'GEN_EMAIL'"` just run:

```bash
pip install --upgrade pyOpenSSL
```

---

## Verify dataset status

```bash
dvc status
```

---

## After modifying the dataset

```bash
dvc add data
git add data.dvc
git commit -m "Update dataset"
dvc push
git push
```

---

## Notes

- Never commit datasets directly to Git.
- Never commit `.dvc/config.local`.
- Never commit OAuth credentials.
- All dataset versions are managed by DVC.