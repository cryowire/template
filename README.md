# cryo-wiring-template

A template repository for dilution refrigerator wiring configuration data.

## Usage

### 1. Create a repository

Click the **"Use this template"** button on GitHub to create your own data repository.

### 2. Add fridge data

```bash
# Set up with the cryo-wiring CLI
pip install cryo-wiring-cli

# Create a new cooldown for a fridge
cryo-wiring new --fridge my-fridge --chip chip.yaml
```

Or use the [cryo-wiring-app](https://github.com/orangekame3/cryo-wiring-app) Web UI:

```bash
pip install cryo-wiring-cli-app

# Launch with this repository
cryo-wiring-app serve --repo https://github.com/<your-user>/<your-repo>.git
```

### 3. Structure

```
<your-repo>/
├── components.yaml              # Component catalog (master)
└── your-cryo/                   # Fridge directory
    ├── current/                 # Working cooldown
    │   ├── metadata.yaml
    │   ├── chip.yaml
    │   ├── components.yaml
    │   ├── control.yaml
    │   ├── readout_send.yaml
    │   └── readout_return.yaml
    └── 2026-001/                # Snapshot (frozen past cooldown)
        ├── metadata.yaml
        ├── chip.yaml
        ├── components.yaml
        ├── control.yaml
        ├── readout_send.yaml
        └── readout_return.yaml
```

### 4. CI validation

Validation runs automatically when a PR is created. Errors are raised if wiring data violates the schema or contains inconsistencies.

## Customization

### Component catalog

Define the components you use in `components.yaml`:

```yaml
XMA-10dB:
  type: attenuator
  model: XMA-2082-6431-10
  value_dB: 10.0

LNF-HEMT:
  type: amplifier
  model: LNF-LNC03_14A
  amplifier_type: HEMT
  gain_dB: 40.0
```

## Specification

For details on the data format, see [cryo-wiring-spec](https://github.com/orangekame3/cryo-wiring-spec).
