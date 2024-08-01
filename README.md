# Integrated modelling workshop

If you want to use this GitHub page to take your project further then please use
the [template](docs/template.md).

The overview of our integration day

- 09:00-09:10 Explain the day (now)
- 09:10-09:40 Present overviews:
  - [Inputs/outputs](#water-in-water-out)
  - [Conceptual diagram](#conceptual-diagram)
- 09:40-11:50 (30 min coffee break): [Fill in integration templates](#20-minute-integration-template)

## Example: groundwater (MODFLOW) and supply distribution (EPANET)

I don't know either of these models well, I just asked ChatGPT for info in the
inputs/outputs. These examples will be used throughout this explanation

## Introduction

Explain your system, I will present groundwater and supply distribution side-by
-side.

### Water in-water out

Where does water/pollutants come in/go out?

<!-- markdownlint-disable MD033 -->
<table>
   <!--- Headers -->
   <tr><th></th><th>MODFLOW</th><th>EPANET</th>

   <!--- Row 1, input section -->
   <tr>
      <td rowspan="4">Inputs</td>
      <td>Recharge from surface (includes precipitation, irrigation, or other surface water bodies).</td>
      <td>Reservoirs, with a fixed head thus representing a large store.</td>
   </tr>

   <!--- Row 2 -->
   <tr>
      <td>Rivers and streams (boundary condition model).</td>
      <td>Tanks, sources or sinks with variable elevation and head.</td>
   </tr>

   <tr>
      <td>Generalised/fixed head boundaries (reservoirs, lakes, lateral aquifer flows?)</td>
      <td>Other external inflows.</td>
   </tr>

   <tr>
      <td>Point and distributed pollutant sources/Injection wells.</td>
      <td></td>
   </tr>

   <!---Output section -->
   <tr>
      <td rowspan="4">Outputs</td>
      <td>Generalised/fixed head boundaries.</td>
      <td>Nodes representing demand.</td>
   </tr>

   <tr>
      <td>Rivers and streams (boundary condition model).</td>
      <td>Tanks, sources or sinks with variable elevation and head.</td>
   </tr>

   <tr>
      <td>Evapotranspiration.</td>
      <td>Reservoirs, with a fixed head thus representing a large store.</td>
   </tr>

   <tr>
      <td>Extraction wells.</td>
      <td>Leaks and valves.</td>
   </tr>

</table>

### Conceptual diagram

Other information is fine, but make sure to highlight all of your inputs and
outputs, in particular dynamic ones!

![conceptual-diagram](docs/images/conceptual-diagram-separate.png)

_Made with [draw.io](https://app.diagrams.net/?src=about#)_

## 20-minute integration template

- [What models/systems do you care about?](#models)
- [Do any inputs/outputs match?](#direct-integration)
- [What additional processes need to be represents in between the outputs/inputs
of the models?](#indirect-integration)
- [Update conceptual diagram](#conceptual-diagram-integrated)
- [Explore feasibility](#explore-feasibility)

### Models

- Groundwater: MODFLOW
- Supply distribution: EPANET

### Direct integration

- Leaks/Valves -> MODFLOW? I guess leak could be a point water/pollutant source,
 or maybe aggregate into recharge from surface.
- If there is a groundwater supply borehole, then that could be pumped from
MODFLOW enter the EPANET tanks?
- EPANET reservoirs seem like the system outflow - perhaps some of this can go
into MODFLOW depending on the case study.

### Indirect integration

- Generalised head boundaries in MODFLOW - maybe these could match with network
head in distribution? Presumably enabling infiltration (in the unpressurised
sections) or exfiltration (anywhere).
- Leaks/valves -> MODFLOW via river interactions (depends where the leaks go..).
- Garden water use interacting with recharge/evapotranspiration (probably needs
a model to 'translate' the EPANET demand outputs).

### Conceptual diagram integrated

Make sure to highlight all of your inputs, outputs and integration links!

![conceptual-diagram](docs/images/conceptual-diagram-integrated.png)

### Explore feasibility

- **Are these identified integrations likely to induce boundary condition errors
in one system or the other! (i.e., why integrate)**
- What temporal scale mismatches exist?
- What spatial scale mismatches exist?
- What other missing data is there?
- How complicated are the processes in between [indirect integration](#indirect-integration)?
- What kind of case studies might these work for?
