# Low-Power Digital Link — Stage 1

Local PC-only simulation. No MATLAB or radio hardware required.

## Run
**Interactive application:** open http://127.0.0.1:8765 in Chrome or another browser.
Automatic startup at Windows sign-in is configured via the Digital Link Lab shortcut
in the Windows Startup folder. Start-Background.ps1 launches the local server hidden.
No CMD file or ChatGPT is required during normal use. HTTP is used for this local
address; HTTPS is not configured. The PC must be on and signed in.
The manual `Start-Link-Lab.cmd` remains a fallback if automatic startup is disabled.
Enter text, select BPSK/QPSK and coding/noise settings, and click Run transmission.
The app computes an actual RRC waveform channel, received message, bit errors,
plots and optional BER comparison trials. It does not require ChatGPT or Internet.
The BER & tradeoffs tab shows previously computed full-sweep results and exports.

Double-click `Run-Simulation.cmd` for the quick experiment. Results are in `results`.
Or run in PowerShell:

```powershell
.\.venv\Scripts\python.exe -m unittest discover -s tests -v
.\.venv\Scripts\python.exe src\simulate.py --profile quick
.\.venv\Scripts\python.exe src\simulate.py --profile full
```

Quick sweeps use 64/256-byte payloads and a 120,000-bit cap per point.
Full sweeps add 1024-byte payloads and raise the cap to 1.2 million bits.
Each point also stops at 200 errors. Full mode takes longer. CSV counts,
seeds, confidence intervals and metadata make results reproducible.
Packets are processed whole, so the bit cap can be exceeded by less than one payload.
Results are overwritten by the next run: copy them first if comparing runs.

## Outputs
- BER curves and uncoded theoretical reference
- Coding gain / required payload Eb/N0 table
- Data rate and packet-size plots
- Modeled transmit power, bandwidth and battery-life tradeoff CSV
- RRC waveform, spectrum, QPSK constellation and recovered data demo
- REPORT.md with assumptions and limitations

Symbol-domain Monte Carlo sweeps assume ideal matched filtering and timing.
The separate sample-domain demo includes RRC filters and path attenuation.
Power and battery numbers are modeled, not physical measurements.
No framing/preamble/CRC, fading, frequency drift or hardware synchronization
is implemented yet. These are Stage 2 extension points; this version is not
a deployable soldier radio. Low BER estimates need larger independent runs.

All files live in D:\ChatGPT\Projects\Digital Comn project 2.
The virtual environment uses bundled Python 3.12 for scientific-package support.
No global Python installation or Windows app settings were changed.

Edit `configs/link_budget.json` to change power/battery assumptions. Values are
validated before a run. See `docs/SECURITY.md` for baseline review coverage.

Technical references: [convolutional codes and Viterbi decoding](https://www.mathworks.com/help/comm/ug/convolutional-codes.html),
[AWGN energy/noise relationships](https://www.mathworks.com/help/comm/ug/awgn-channel.html).

## Final simulation handoff - 11 November 2026

The original sweep remains archived. See output/pdf/Digital-Link-Lab-Submission.pdf
for the recommended configuration, independent confirmation and worked power
budget. Reproduce with src/final_study.py followed by src/confirm_design.py.
Bench needs and pending physical tests are in docs/BENCH_CHECKLIST.md.
