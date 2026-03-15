# DummyApp
Python App for DevOps Practice

This is a minimal Flask app you can build and deploy to an Azure VM.

## Run locally

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install -r requirements.txt
python3 app.py
```

Then open: `http://localhost:8000/`

## Deploy to Azure VM (via GitHub Actions)

1. Push this repo to GitHub.
2. Add these secrets to your repository:
   - `AZURE_VM_HOST` (e.g., `123.45.67.89`)
   - `AZURE_VM_USER` (e.g., `azureuser`)
   - `AZURE_VM_SSH_KEY` (private key content)
   - `AZURE_VM_PORT` (usually `22`)

3. On the VM, clone your repo into a directory (e.g. `/home/azureuser/app`).

4. Ensure the VM has Python 3.12+ installed and `gunicorn` is installed as above.

5. The GitHub Action will SSH to the VM and run a deploy script that:
   - pulls latest code
   - installs dependencies
   - restarts the app via `gunicorn`

## Notes

- You can adjust the deployment script in `.github/workflows/ci-deploy.yml` to match your folder layout and process.
