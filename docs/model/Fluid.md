---
sidebar_position: 2
---

# Fluid

The `Fluid` object is a discrete packet of information passed from one component to another.  
It has no methods and does not act on other objects.

Its primary properties are pressure, temperature, and flowrate, and these are specified on initialization. Its secondary properties (density, viscosity, enthalpy) come from lookup tables created for a particular fluid composition.

| Property      | Unit             | Default | Notes                                          |
| ------------- | ---------------- | ------- | ---------------------------------------------- |
| `pressure`    | `Pressure`       | -       | Defined with `physical-quantities` npm package |
| `temperature` | `Temperature`    | -       | Defined with `physical-quantities` npm package |
| `flowrate`    | `Flowrate`       | -       | Defined with `physical-quantities` npm package |
| `density`     | kg/m<sup>3</sup> | -       | number                                         |
| `viscosity`   | Pa.s             | -       | number                                         |
| `enthalpy`    |                  | -       | number                                         |

Two input files are used to find the secondary properties. One details the phase envelope of the fluid and the other specifies the density, viscosity, and enthalpy of the fluid at each pressure/temperature combination in a range of possible values. Secondary fluid properties are then determined by interpolating the data points nearest the specified pressure and temperature.

```csv title="phaseEnvelope.csv"
TEMPERATURE,BUBBLEPRESSURE,DEWPRESSURE
-10,5928672.71,2804549.78
-9.7818792,5934775.06,2822460.52
-9.5637584,5940966.24,2840451.63
...
```

```csv title="fluidPropertiesLookup.csv"
PT,TM,HG,VISG,VISHL,ROG,ROHL
1000.00000,-46.655518,-58092.553,1.17144E-5,.000215567,.022951659,1143.33694
1000.00000,-45.819398,-57446.429,1.17569E-5,.000212998,.022867217,1139.07701
1000.00000,-44.983278,-56799.557,1.17995E-5,.000210453,.022783394,1134.78187
1000.00000,-44.147157,-56151.936,1.18420E-5,.000207931,.022700183,1130.45084
...
```
