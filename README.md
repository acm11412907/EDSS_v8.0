EDSS v8.0 — Engineering Decision Support System for HMI Validation

Live Demo: https://acm11412907.github.io/EDSS_v8.0/

A browser-based engineering analysis tool for evaluating rotary HMI (Human-Machine Interface) controls that rely on magnetic sensing. EDSS models the relationship between mechanical tolerance, magnetic field behavior, firmware detection thresholds, and production yield — turning cross-functional engineering knowledge into a single, reusable decision framework.

Built to support the validation and production-readiness process for project, a magnetic rotary encoder / HMI control design.

Why This Exists

Rotary HMI controls that use magnetic sensing sit at the intersection of several engineering domains that normally live in separate spreadsheets and separate people's heads:


Mechanical: tolerance stack-up on the magnet-to-sensor gap
Magnetics: field strength (Br, flux density) at the sensor given that gap
Firmware: detection thresholds and noise margins that decide pass/fail
Production: the resulting yield, capability (Cpk/Ppk), and risk exposure


EDSS pulls these into one live data flow so a design or validation review can ask "what if we tighten this tolerance by 0.05mm" and immediately see the downstream effect on yield and risk — instead of waiting for four different engineers to re-run four different models.

How It Works

The tool is organized as a sequential analysis pipeline, with each module feeding the next:

Tolerance → Gap → Flux → Sensor Count → FW Decision → Capability → DOE → Decision Engine → Report

Modules


HW — Define the functional spec and component tolerance stack-up (add parts, set tolerance in ±mm)
Magnetic — Magnet field modeling (e.g. BMN-50SH/ST NdFeB) using an axial cylindrical-magnet field approximation; calibrate remanence (Br) and gap against real gauss-meter data
FW — Firmware threshold modeling: EE noise, threshold factor, baseline mean/σ, system σ, and the resulting pass range and false-reject rate
DOE — Cost-aware Design of Experiments optimizer that searches discrete tolerance options for the lowest-cost configuration that still meets the yield target
Capability — Statistical capability dashboard (Cp, Cpk, Ppk, Sigma, PPM, mean, std)
Decision — Engineering Decision Engine: recommendations plus a risk matrix (probability × impact → Accept / Monitor / Mitigate / Control / Critical)
Report — One-click export of a full engineering report (yield, Cpk, flux pass, FW range, configuration tables, DOE suggestions) as a PDF


Simulation Controls


Monte Carlo iteration count: 10,000 / 50,000 / 100,000
Distribution model: Normal / Uniform
Configurable magnet profile (custom or reference N42 / N52)


Tech Stack


Vanilla HTML / CSS / JavaScript — no build step, runs entirely client-side
Deployed as a static site via GitHub Pages


Usage


Open the live demo
Walk the modules in order (HW → Magnetic → FW → DOE → Capability → Decision → Report), or jump directly to the module you need
Enter your tolerance spec, magnet parameters, and firmware threshold inputs
Run the DOE optimizer for cost-aware tolerance recommendations
Review the capability dashboard and risk matrix
Export a PDF engineering report for design reviews or validation sign-off


Background

Developed to support NPI and validation work on magnetic rotary HMI controls, converting engineering judgment that typically lives across mechanical, magnetics, and firmware disciplines into a shared, reusable tool for design reviews, validation planning, and production-risk communication.

Author

Ya-Rou (Coco) Chen
acm11412907@gmail.com
