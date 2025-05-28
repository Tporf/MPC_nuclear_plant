# MPC_nuclear_plant
```

A MATLAB/Python-based simulation tool for modeling and analyzing the dynamic behavior of nuclear reactors, with a focus on safety constraints and non-linear feedback effects.

## Project Overview
This project implements the mathematical model described in the ACMp4 diagrams, which captures:
- Core power dynamics
- Fuel and coolant temperature evolution
- Delayed neutron precursors
- Burnup accumulation
- Operational safety constraints

## Key Features
- **State Vector Modeling**: 
  ```math
  x = [P, T_f, C, E, T_c]^T
  ```
  Where:
  - P = Core power (MW)
  - T_f = Average fuel temperature (°C)
  - C = Delayed-neutron precursor concentration
  - E = Burn-up/energy tally (MW-s)
  - T_c = Hot-leg coolant temperature (°C)

- **Dynamics Equations**:
  - Power evolution with reactivity feedback
  - Fuel-coolant heat transfer
  - Delayed neutron kinetics
  - Coolant temperature dynamics

- **Safety Constraints**:
  - Fuel temperature limit (≤ 800°C)
  - Rod-drive ramp rate limit
  - Maximum licensed burn-up
  - Power ramp-rate limits

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/nuclear-reactor-sim.git
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt  # For Python version
   ```
   or
   ```matlab
   % For MATLAB version - ensure Control System Toolbox is installed
   ```

## Usage
### Python Version
```python
from reactor_model import ReactorSimulator

# Initialize with typical PWR parameters
sim = ReactorSimulator(
    mf_cpf=2.5,      # Fuel heat capacity [MJ/K]
    mc_cpc=0.75,     # Coolant heat capacity [MJ/K]
    hA=70,           # Fuel-coolant conductance [MW/K]
    beta0=0.0065     # Initial delayed neutron fraction
)

# Run simulation
results = sim.run(t_end=3600, P0=1000)  # 1 hour at 1000MW initial power
```

### MATLAB Version
```matlab
params = struct(...
    'mf_cpf', 2.5, ...
    'mc_cpc', 0.75, ...
    'hA', 70, ...
    'beta0', 0.0065);

[t, x] = simulateReactor(3600, 1000, params);
```

## Outputs
The simulator generates:
- Time-series plots of all state variables
- Constraint violation warnings
- Reactivity feedback analysis
- Heat transfer efficiency metrics

## Safety Constraints Implementation
The model enforces:
```python
def check_constraints(state):
    if state.T_f > 800:
        raise SafetyViolation("Fuel temperature exceeds 800°C limit")
    if abs(state.dPdt) > 0.05 * P_nominal:
        raise SafetyViolation("Power ramp rate too high")
    # Additional constraints...
```

## Contributing
Please read CONTRIBUTING.md for details on our code of conduct and the pull request process.

## License
This project is licensed under the MIT License - see the LICENSE.md file for details.

## References
1. Duderstadt & Hamilton, "Nuclear Reactor Analysis"
2. Lamarsh, "Introduction to Nuclear Engineering"
3. ANSI/ANS Standards for Reactor Safety
```

This README provides:
1. Clear project identification
2. Technical specifications matching your diagrams
3. Implementation examples in both Python and MATLAB
4. Safety constraint handling
5. Standard open-source project structure

Would you like me to:
- Add more detailed installation instructions?
- Include sample output plots?
- Create accompanying MATLAB/Python template files?
- Add specific reactor type parameters (PWR/BWR defaults)?
