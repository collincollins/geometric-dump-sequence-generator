# Geometric Dump Sequence Generator

A web-based tool for generating geometrically-spaced dump sequences for molecular dynamics simulations of glassy systems.

## Overview

When studying aging in glassy systems, dynamics span many orders of magnitude in time. Linear (evenly-spaced) dumps are inefficient—they waste storage with redundant short-time snapshots while requiring impractical numbers of frames to capture long-time dynamics.

**Geometric dumping** solves this by spacing dumps as:

$$t_n = t_0 \cdot r^n$$

This gives uniform coverage on a logarithmic time axis, efficiently capturing both fast dynamics at short times and slow dynamics at long times with only ~100-500 dumps spanning 6+ decades.

## Features

- **Two-sequence approach**: 
  - **Long sequence** captures equilibration/aging during the waiting time
  - **Short sequences (repeated)** run after equilibration for TTI-preserving autocorrelation measurements
- **Auto-optimized parameters**: Automatically selects optimal number of terms to hit target end time
- **Reality checks**: Validates sequence continuity and coverage
- **File size estimation**: Calculates expected DCD trajectory sizes
- **Interactive visualization**: ECharts-powered plots of dump times and run intervals
- **Export options**: Download individual or stitched dump/run time files as ZIP
- **Dark/light theme**: Monospace aesthetic with theme toggle
- **Educational modal**: Explains the physics of aging, TTI, and geometric dumping

## Usage

1. Open `visualize_sequences.html` in a web browser
2. Enter your simulation parameters:
   - **dt**: Simulation timestep (LJ units)
   - **tau_equil**: Equilibration time target
   - **tau_alpha**: Alpha relaxation time
3. Click "Generate Sequences"
4. Review the generated commands, reality checks, and visualizations
5. Download the dump/run time files for your simulation

## Generated Output

The tool generates two Python commands for the `geo-rev11.py` script:

- **Long sequence command**: For the equilibration phase
- **Short sequence command**: For repeated production runs

Each sequence produces:
- `dump_times.txt`: Cumulative timesteps for each dump
- `run_times.txt`: Interval between consecutive dumps
- `file_names.txt`: Output filenames (short1.dcd, short2.dcd, ...)

## Physics Background

### Why Geometric Dumping?

In aging glassy systems, time-translation invariance (TTI) is broken:

$$C(t_w, t_w + \tau) \neq C(\tau)$$

The relaxation time grows with waiting time: $\tau_\alpha(t_w) \sim t_w^\mu$

Geometric spacing provides uniform resolution across all relevant timescales, from ballistic motion to structural relaxation.

### The Two-Sequence Strategy

1. **Long sequence**: Records the aging period. The system's properties evolve during this time.
2. **Short sequences**: Run in the quasi-stationary regime where TTI approximately holds, enabling standard autocorrelation analysis.

## Technologies

- Vanilla HTML/CSS/JavaScript (no build step required)
- [Apache ECharts](https://echarts.apache.org/) for visualization
- [KaTeX](https://katex.org/) for math rendering
- [JSZip](https://stuk.github.io/jszip/) for file downloads

## Authors

Made by Collin, Max, and Claude

## License

MIT License

