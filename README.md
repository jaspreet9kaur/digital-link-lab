# Digital Link Lab

An interactive digital communications simulator and a reproducible bit-error-rate (BER) study. The project compares BPSK and QPSK with convolutional coding and models the power required to reach a target BER of 0.0001.

- [Download the complete project source and results](Digital-Link-Lab-source.zip)
- [Read the submission report](Digital-Link-Lab-Submission.pdf)
- [Read the study booklet](Digital-Link-Lab-Study-Booklet.pdf)
- [Download the two-minute explainer](Digital-Link-Lab-Explainer.mp4)

## Run locally

Extract the source archive and run these commands from the extracted folder on Windows with Python 3.12:

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements-lock.txt
.\.venv\Scripts\python.exe -m unittest discover -s tests -v
.\.venv\Scripts\python.exe src\web_app.py
```

Open [the local simulator](http://127.0.0.1:8765) while the server is running. The archive includes the simulation code, browser edition, test suite, measurement CSVs, and plots.

The submission report documents the simulation assumptions and pending hardware validation. Power and battery figures are modeled estimates.
