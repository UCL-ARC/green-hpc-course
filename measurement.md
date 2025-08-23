---
title: Measurement
teaching: 40
exercises: 20
---

::::::::::::::::::::::::::::::::::::::: objectives

- Understand how emissions are classified in the widely-used GHG protocol
- Know which GHG protocol classifications are relevant to use of HPC systems
- Learn a methodology to use GHG protocol to estimate the emissions associated with our use of HPC systems
- Understand how emission rates from HPC can be calculated

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How are emissions measured and classified under the GHG protocol?
- How do I use the GHG protocol to estimate emissions from my use of HPC?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

The Greenhouse Gas (GHG) protocol is the most commonly-used method for organisations to measure their total carbon emissions. Understanding GHG scopes and how to measure your software against industry standards will help you see to what extent you are reducing carbon emissions and how that fits with wider activities to reduce emissions.

To complement the GHG protocol, and if yo develop software that is used by others, you can also use the Software Carbon Intensity (SCI) specification. While the GHG is a more generic measurement suitable for all types of organisations, the SCI is specifically for measuring a rate of software emissions and designed to incentivise the elimination of those emissions.

## The GHG protocol

The [Greenhouse Gas protocol](https://ghgprotocol.org) is the most widely used and internationally recognized greenhouse gas accounting standard. [92%](https://ghgprotocol.org/about-us) of Fortune 500 companies use the GHG protocol when calculating and disclosing their carbon emissions and it provides the basis of emissions reporting for most countries (including the UK). Using the GHG protocol allows us to compare our emissions from use of HPC systems to other sources of emissions in a quantitative way.

The GHG protocol divides emissions into three scopes:

- **Scope 1**: Direct emissions from **operations** owned or controlled by the reporting organisation, such as on-site fuel combustion or fleet vehicles.
- **Scope 2**: Indirect emissions related to **emission generation of purchased energy**, such as heat and electricity.
- **Scope 3**: Other indirect emissions from all the other activities you are engaged in. Scope 3 emissions are typically split into two further categories: *Upstream Emissions* and *Downstream Emissions*:
   + **Upstream Scope 3 Emissions**: Includes all emissions from an organisation's supply chain, e.g. emissions from manufacturing and shipping a product
   + **Downstream Scope 3 Emissions**: Emissions resulting from the use of a product, e.g. the electricity customers may consume when using your product or waste output from the product

Scope 3, sometimes referred to as value chain emissions, is often the most significant source of emissions and the most complex to calculate for many organisations. These encompass the full range of activities needed to create a product or service, from conception to distribution. In the case of a laptop, for example, every raw material used in its production emits carbon when being extracted and processed (part of the upstream scope 3 emissions). Value chain emissions also include emissions from the use of the laptop, meaning the emissions from the energy used to power the laptop after it has been sold to a customer (part of downstream scope 3 emissions).

Through this approach, it's possible to sum up all the GHG emissions from every organisation and person in the world and reach a global total.

### What scope does my application fall into?

We have already seen how the GHG protocol asks us to bucket emissions from HPC system use according to scopes 1-3. But how do we actually do this?

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise: What scope for HPC emissions?

Throughout this lesson we have spoken about emissions from two different sources associated with our use of HPC: emissions from the electricity used to run our models/simulations on HPC systems and embodied emissions from the HPC system hardware. Given the definitions of scope 1-3 emissions given above, what scope do you think these two different sources of HPC system use emissions fall into?

:::::::::::::::  solution

## Solution

- Emissions from electricity used: these would be classified as Scope 2 emissions
- Embodied emissions from HPC system hardware: these would be classified as Upstream Scope 3 emissions

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  callout

## HPC electricity: Scope 2 or Downstream Scope 3?

Whether the emissions from electricity use on HPC systems are Downstream Scope 3 or Scope 2 really depends on who is computing the emissions and for what purpose. From the viewpoint of the hardware vendor who sells and manufactures the HPC system, the electricity use falls into Downstream Scope 3 emissions but for operators and users of the HPC system they would classified as Scope 2 emissions. As we are approaching this subject as buyers, operators and users of HPC systems we will always classify the emissions from our electricity use on HPC systems as Scope 2.

::::::::::::::::::::::::::::::::::::::::::::::::::


## How to calculate your HPC emissions


Quantifying the emissions from your work (and generating an emissions rate, as described below) are critical steps on the path to reducing and potentially eliminating emissions from your use of HPC systems. The formula for calculating your emissions from use of HPC systems (`HPC-E`) is straightforward:

```
HPC-E = (E * I) + M
```

- `E` = Energy consumed by HPC use (in kWh)
- `I` = Location-based carbon intensity (in kgCO<sub>2</sub>/kWh)
- `M` = Embodied emissions 

You can calculate this on a per job basis or for a larger grouping of HPC use - even for a full lifetime of an HPC service.

:::::::::::::::::::::::::::::::::::::::: callout

## Include failed jobs and jobs that did not produce useful output

While it can be tempting to only include the use of HPC that produced useful output in our emissions calculations, this should be avoided. The true amount of emissions includes **all** of our HPC system use to get us to the results we use and so failed jobs (due to errors) or calculations that did not produce useful output must be included. On the positive side, one of the ways we can reduce our emissions from use of HPC systems is to be more careful and eliminate emissions arising from these types of non-productive jobs.

::::::::::::::::::::::::::::::::::::::::::::::::::

Instead of bucketing the carbon emissions of HPC use into scopes 1-3, this calculation buckets them into **operational emissions** (carbon emissions from the electricity required for your HPC use, represented by `E * I`) and **embodied emissions** (carbon emissions from the physical HPC system components, represented by `M`).

Follow these steps to calculate your HPC emissions. 

1. Gather your energy use - this can be measured or estimated and is often a combination of measured and estimated data
2. Determine the carbon intensity at the location of the HPC system you are using
3. Determine the embodied emissions associated with your use of HPC
4. Compute your total HPC emissions

### 1. Gather energy use

Many HPC systems now provide energy use data for jobs run on the system. If this is the case, you can use these as the starting point for calculating your energy use of HPC resources. If this is not available, then you may need to estimate the energy use of your use of resources from component power draw. Even if you have energy use data available this may only cover energy use of compute nodes (or even processors on compute nodes) so you do typically have to do some estimation of power draw of other components to know how much extra energy to add on to include them in your calculation.

If you are really lucky, the HPC system staff will have done this calculation for you. As has been done for the UK National Supercomputing Service, ARCHER2: [Estimating emissions from ARCHER2](https://docs.archer2.ac.uk/user-guide/energy/#scope-2-emissions).

We will cover two different ways to estimate the power draw of HPC systems which can then be used to compute energy use.

a. Use the total power draw of the system
b. Use the per-component power draw of the system

:::::::::::::::::::::::::::::::::::::::: callout

## Heterogeneous systems

The methodologies outlined below all assume the compute nodes are homogeneous. What do you do if this is not the case and some nodes on the system have GPU and others do not, for example? In this case, you should try, as much as possible, to treat each homogeneous partition as its own smaller HPC system to help calculate energy use.

::::::::::::::::::::::::::::::::::::::::::::::::::

#### a. Using total power draw

One of the simplest ways to estimate your energy use is to use the total power draw of the HPC system and divide it by the number of components to get a mean power draw per component that can be used to estimate energy use. For example, if the total power draw of the system is 250 kW and it contains 512 GPU, then the mean power draw per GPU is `250 kW / 512 GPU = 0.488 kW/GPU`. This, in turn, means the energy used for 12 hours use of 2 GPU is estimated by `12 hours * 2 GPU * 0.488 kW/GPU = 11.7 kWh`.

You should use the component that you measure resource use in to compute the mean power draw. For example. if your usage is measured in GPUh, then compute the power draw per GPU; if your usage is measured in nodeh, compute the power draw per node.

#### b. Using per-component power draws

This approach requires more detailed information being available on the power draw of different components though measurement or from information from the vendors of the components. If you are getting your energy use from counters on the compute nodes (as is sometimes possible on HPC systems) then this approach allows you to estimate additional energy overheads that need to be added on in addition to the measured power draw.

We use the total power draw of the system to estimate anaegy usage for Young (where an extra 10% is added for energy usage of interconnect switched and coolant unites):

| Component | Energy usage from 04-07-2024 to 04-07-2025 (kWh) | % Total |
|---|--:|---|
| Compute and storage nodes | 1,533,082.28 | 90% |
| Interconnect switches and Coolant units | 153,308.2|  10% |
| Total | 1,686,390.48 | 100% |

Systems like ARCHER2 also have the total compute node energy use available per job to users from the Slurm scheduler, but Young does not have it as of now.

#### Add in energy from plant overheads

As well as the energy used by the system itself, there is also the energy used by the plant that supplies power and cooling to the HPC system. Different data centres have different sizes of overheads and this is given by PUE (Power Use Efficiency) which we met earlier in this lesson. For example, a PUE of 1.25 indicates that an additional 25% energy use is added on top of the system energy use to account for the plant. 

The PUE will vary with outside weather conditions at the data centre. For the Young example, PUE is typically less than 50-60% so, as an estimate, we add an additional 60% energy use to the total to account for plant overheads. 

So, for the Young example, the process for computing your total energy use becomes:

- Measure total compute node energy use from all jobs run via node counters
- Add 10% extra energy to cover energy use from other components
- Add another 60% energy use top of this new total to cover plant overheads

Hence, the total energy usage of Young from 04-07-2024 to 04-07-2025 comes out to be 2,698,224.76 kWh.

### 2. Determine local carbon intensity

Once you have your energy use then you need to convert this to emissions using the carbon intensity for the electricity supply for the HPC system. In most cases, HPC systems are powered by the energy grid and many energy grids provide details on the carbon intensity as a function of time.

As we saw earlier, for the UK, the carbon intensity is dependent on location and time. You can access the values through different web services but one that is commonly used is the [Carbon Intensity API](https://carbonintensity.org.uk). Carbon intensity is reported for every region every 30 minute interval. To estimate your emissions you can either use the fine grained intensity matched to the run times of your HPC system use or use an aggregate value over a longer period. The aggregate value is a simpler choice for a first estimate. The table below shows the approximate average carbon intensities for the different regions of the UK national grid for 2024 ordered from lowest to highest.

| Type | Regions | Carbon Intensity (gCO<sub>2</sub>e/kWh) |
|--|------|------:|
| Low | N. Scotland, S. Scotland, N.E. England, N.W. England | 22 - 48 |
| Low Medium | N. Wales | 77 |
| Medium | E. England, London, W. Midlands, S.E. England, Yorkshire | 108 - 135 |
| High Medium | S. England, E. Midlands | 186 - 203 |
| High | S.W. England, S. Wales, | 242 - 255 |

Young is located in Torington place, and querying the carbon intensity API from 04-07-2024 to 04-07-2025 for the postcode WC1E gives us a value of 139.96 gCO2e/kWh.

### 3. Determine embodied emissions

:::::::::::::::::::::::::::::::::::::::: callout

## Upstream Scope 3 emissions

Remember that we are considering only *upstream* Scope 3 emissions here. The emissions from electricity
use are captured in the Scope 2 emissions estimates.

::::::::::::::::::::::::::::::::::::::::::::::::::

Calculating the embodied emissions can be more difficult than the operational emissions from energy 
consumption as it can be more difficult to get information on embodied emissions associated with HPC system hardware. You may, of course, be lucky and the HPC system you are using could already provide estimates of the 
embodied emissions which you can use!

If you need to estimate this yourself, the major contributors to embodied emissions are likely to be:

- Compute nodes
- Interconnect switches
- Storage

so these are the best place to start. Bear in mind that each HPC system is different so other components
may need to be taken into account. As a rule of thumb, you should look at the HPC system to see which
components there are lots of and use that as the starting place. Complex components (such as nodes, storage
and switches) are likely to have much higher embodied emissions than simpler components (pumps, fans, cables etc.).

As an example, here is how the embodied emissions for Young have been estimated:

| Component type | Count | Model | Vendor | Estimated kgCO<sub>2</sub>e per unit | Estimated kgCO<sub>2</sub>e | References |
|---|--:|--:|--:|--:|--:|--:|---|
| Compute nodes | 32 | Cray XD220v | HPE | 1642 | 52,544 | 1 |
| Compute nodes | 11 | ProLiant DL360 Gen10 | HPE | 1,616 | 17,776 | 2 |
| Compute nodes | 8 | ProLiant DL380 Gen10 | HPE | 1,668 | 13,344 | 3 |
| Compute nodes | 508 | ProLiant XL170r Gen10 | HPE | 2,100 | 1,066,800 | 4 |
| Compute nodes | 6 | ProLiant XL675d Gen10 Plus | HPE | 2,300 | 13,800 | 4 |
| Interconnect switches | 22 | OPA SWITCH | Generic | 280 | 6160 | 5 |
| Interconnect switches | 2 | Aruba 6300M | HPE | 280 | 560 | 5 |
| Interconnect switches | 2 | FlexFabric 5710 JL689A | HPE | 280 | 560 | 5 |
| Interconnect switches | 38 | FlexNetwork 5510 JH146A | HPE | 280 | 10640 | 5 |
| Total | | | | | 1,182,184 | | |

| Component | Count | Estimated kgCO<sub>2</sub>e per unit | Estimated kgCO<sub>2</sub>e | References |
|---|--:|--:|--:|---|
| HDD | 2,000,000 GB | 0.02 | 40,000 | 6 |
| SSD | 2,000 GB | 0.16 | 320 | 6 |
| Total | | | 40,320 | |

The total estimated emobodied emission comes out to be 1,222,504 kgCO<sub>2</sub>e.

References:

1. Calculated as an average of 2 and 3
2. [HPE product carbon footprint HPE ProLiant DL360 Gen10 Plus Server](https://www.hpe.com/psnow/doc/a00133636enw?jumpid=in_hpesitesearch)
3. [HPE product carbon footprint HPE ProLiant DL380 Gen10 Server](https://www.hpe.com/psnow/doc/a50004545enw?jumpid=in_hpesitesearch)
4. Estimate taken from HPE's carbon footprint of similar products
5. Estimate taken from IBM z16(TM) multi frame 24-port Ethernet Switch Product Carbon Footprint
6. [Tannu and Nair, 2023](https://arxiv.org/abs/2207.10793)

Note that there is a large amount of uncertainty for Scope 3 emissions due to lack of high quality embodied
emissions data. The number used for the compute node emissions is at the high end of estimated values for a
CPU-only compute node and the actual value could be as low as 900 kgCO<sub>2</sub>e/node.
If the lower value is used, it reduces the overall estimated embodied emissions but does not significantly
change the fraction of emissions attributed to the compute nodes.

:::::::::::::::::::::::::::::::::::::::: callout

## Other embodied emissions sources

We have not included embodied emissions associated with the data centre buildings and plant in the
analysis above. [The IRISCAST report](https://doi.org/10.5281/zenodo.7692450) provides
an evaluation of these values. While the total embodied emissions can be high for these items, their
long lifespan means that their contribution to the embodied emissions during the lifespan of a particular
HPC system are generally much less significant than the embodied emissions from the HPC system hardware
itself.

::::::::::::::::::::::::::::::::::::::::::::::::::


### 4. Compute your total HPC emissions

Now we should have all the data we need to compute our total emissions from HPC system use:

- `E` - Total energy used
- `I` - Carbon intensity
- `M` - Embodied emissions estimate

Remember the equation for computing total emissions from HPC system use (`HPC-E`):

```
HPC-E = (E * I) + M
```

we can plug the numbers in and come up with a value for the total emissions arising from our
use of HPC.

For Young, the total HPC emissions from 04-07-2024 to 04-07-2025 can be calculated as:

```
E * I = 2,698,224.76 kWh * 0.14 kgCO2e/kWh = 377,751.46 kgCO2e
```

```
Amortised M = 1,222,504 kgCO2e / 5 years = 244,500.8 kgCO2e/year (assuming Young stays in operation for 5 years)
```

```
HPC-E = (E * I) + M = 377,751.46 kgCO2e + 244,500.8 kgCO2e/year * 1 year = 622,252.26 kgCO2e for 1 year.
```

Once can see that ~60% of the emission is scope 2 emission and ~40% of it is scope 3 emission; hence, Young's operational emission dominates. This means that we are getting the most out of our initial pollution (manufacturing), so now we should now try reducing or stabilising our operational emission (more on this in the next episode).

Interestingly, UCL produced 49,176,099.46 kgCO<sub>2</sub>e scope 2 emission in the academic years 2015/16 to 2023/24 according to ([HE Provider Data: Estates Management](https://www.hesa.ac.uk/data-and-analysis/estates/environmental)), which is 6,147,012.43 kgCO<sub>2</sub>e per year on an average. Therefore, Young’s scope 2 emission accounts for ~10.12% of UCL’s scope 2 emission per year, which is a huge chunk.

Similarly, UCL produced 162,005 kgCO<sub>2</sub>e scope 2 emission in the academic years 2015/16 to 2023/24, which is 20,250.625 kgCO<sub>2</sub>e per year on an average. Therefore, Young’s scope 3 emission is ~30.7 times UCL’s scope 3 emission per year. However, this number is very likely wrong as UCL does not include supply chain emission in its scope 3 emission (such as, the carbon emitted while procuring computer systems, construction of buildings (for instance, the entirety of UCL East campus), …).

:::::::::::::::::::::::::::::::::::::::: callout

## `E * I` on a per job basis

Rather than computing total energy use and then using an aggregate value for the carbon intensity, it may
make more sense to compute `E * I` on a per-job basis using the carbon intensity value at the job time. This is the approach used in the tools available on ARCHER2 for estimating emissions, but this is not yet available on Young.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise: Computing total emissions from HPC system use

You are using (or running) a GPU-based HPC service and a particular project has used the
following amounts of resource:

- 120,000 GPUh
- 72,000,000 kWh

The total embodied emissions for the service are 6,500,000 kgCO<sub>2</sub>e, the service lifetime 
is 5 years and there are 1000 compute nodes each with 4 GPU. The service is hosted in a
location with a carbon intensity of 20 gCO<sub>2</sub>e/kWh.

1. Compute the scope 2 emissions for the project use
2. Compute the scope 3 emissions rate in kgCO<sub>2</sub>e/GPUh
3. Compute the scope 3 emissions for the project use
4. Compute the total emissions for the project use
5. Do scope 2 or scope 3 emissions dominate or are they evenly matched?

:::::::::::::::  solution

## Solution

1. The scope 2 emissions from energy use by the project are given by `E * I`, the energy used multiplied by the carbon intensity of the electricity supply. In this case, this is given by `72,000,000 kWh x 0.020 kgCO2e/kWh = 1,440,000 kgCO2e`.

2. The scope 3 emissions rate per GPUh is the total scope 3 emissions for the service divided by number of GPUh available over the lifetime of the service.
   1. The total GPUh over the service lifetime is estimated by `5 years x 365 days x 24 hours x 1000 nodes x 4 GPU per node = 4,204,800,000 GPUh`.
   2. The scope 3 emissions rate is given by `6,500,000 kgCO2e / 490,560,000 GPUh = 0.0015 kgCO2e/GPUh`

3. The scope 3 emissions for the project use is the number of GPUh used multiplied by the scope 3 emissions per GPUh: `120,000 GPUh * 0.0015 kgCO2e/GPUh = 185.5 kgCO2e`

4. Total emissions are scope 2 + scope 3 emissions: `1,440,000 kgCO2e + 185.5 kgCO2e = 1,440,185.5 kgCO2e`

5. Scope 2 emissions (from electricity use) heavily dominate the emissions in this example.

:::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::

## HPC Carbon Intensity (HPC-CI) specification

:::::::::::::::::::::::::::::::::::::::: callout

## Software Carbon Intensity (SCI)

The definition, application and calculation of the HPC-CI is heavily inspired
by the [Software Carbon Intensity (SCI)](https://sci.greensoftware.foundation/)
from the Green Software Foundation.

::::::::::::::::::::::::::::::::::::::::::::::::::

We now describe a methodology (the HPC Carbon Intensity specification, HPC-CI) to calculate your emissions from HPC system use and to encourage action towards eliminating emissions.

It is not a replacement for the GHG protocol, but an additional metric that helps you understand how your HPC system use can be measured in terms of carbon emissions so you can make more informed decisions. While the GHG protocol and the HPC-E calculates the **total emissions**, the HPC-CI is about calculating the **rate of emissions**. In automotive terms, HPC-CI is more like a miles per gallon measurement and the GHG protocol/HPC-E is more like the total carbon footprint of a car manufacturer and all their cars they produce every year.

An important thing to note is that it is not possible to reduce your HPC-CI rate by purchasing offsets in the form of neutralisations, compensations, or by offsetting electricity in the form of renewable energy credits (we will cover this in more detail in the next section of the workshop). This means that HPC system use that makes no effort toward reducing emissions but spends money on carbon credits cannot reduce the associated HPC-CI rate.

Offsets are an essential component of any climate strategy; however, offsets are not eliminations and therefore are not included in the HPC-CI metric.

If you make your HPC use more **energy efficient**, **hardware efficient**, or **carbon aware**, your HPC-CI rate will decrease. The only way to reduce your rate is to invest time or resources into one of those three principles. As such, adopting the HPC-CI metric for your HPC use, will drive investment into one of the three pillars of green HPC use.

## The HPC-CI equation

The equation to calculate an HPC-CI rate is simple and very closely related to the calculation of total emissions (HPC-E) presented above:

```
HPC-CI = [(E * I) + M] per R
```

- `E` = Energy consumed by HPC use (in kWh)
- `I` = Location-based marginal carbon intensity (in kgCO2/kWh)
- `M` = Embodied emissions 
- `R` = Functional unit (e.g. iterations, simulated time, calculation cycles, research papers published, cost)

This yields an emissions rate in carbon emissions per functional unit (`HPC-E per R`), e.g. kgCO<sub>2</sub>e/iteration.

The steps to calculate your HPC-CI score are the same as calculating your total emissions (HPC-E) described above with additional steps to produce the rate. Steps 1-4 are identical to the HPC-E methodology described above:

1. Gather your energy use
2. Determine the carbon intensity at the location of the HPC system you are using
3. Determine the embodied emissions associated with your use of HPC
4. Compute your total HPC emissions
5. Select your functional unit (`R`)
6. Calculate your HPC-CI rate

### 5. Select your functional unit (`R`)

As we have seen, the HPC-CI is a rate rather than a total and measures the intensity of emissions
according to the chosen functional unit. The specification currently does not prescribe the
functional unit and you are free to pick whichever best describes the output from your use of HPC
systems. For example, this could be a metric from the software you use (ns simulated, number of
years simulated, iterations) or a metric tied to research progress (number of compounds modelled,
data points analysed, papers published). There may also be ideas in literature related to your
work area of what a good choice may be. You may want to trial different functional units to see
which one works best for your work.

As a concrete example, imagine that you are simulating the dynamics of a biomolecular system
(using software such as GROMACS, Amber or NAMD) then you could well chose the number of ns 
simulated as your functional unit.

You can use multiple functional units simultaneously to have multiple HPC-CI values for
your use of HPC systems. Different HPC-CI units may be more or less useful in different
contexts.

### 6. Calculate HPC-CI rate

Now you have both the total emissions for your use of HPC systems and the number of functional 
units arising from the same use of HPC systems you can calculate the HPC-CI by dividing the 
total emissions by the total number of functional units.

To continue our example of biomolecular simulation that we mentioned above, we would take the
total emissions from our HPC system use - let us say this came out to be 1500 kgCO<sub>2</sub>e -
and the total number of functional units - say 950 ns simulated - and combine them:

```
HPC-CI  = 1500 kgCO2e / 950 ns = 1.58 kgCO2e/ns
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Exercise: HPC-CI rate 

In the previous exercise we computed the total HPC system emissions for 3 months of project
use to be 14,184 kgCO<sub>2</sub>e. The project was modelling the climate and managed to simulate
3,680 years of Earth's climate during that 3 month period using 1,100 GPUh of resource.

1. What is the HPC-CI in kgCO2e per simulated year?
2. What is the HPC-CI in kgCO2e per GPUh?

:::::::::::::::  solution

## Solution

1. Given by: `14,184 kgCO2e / 3,680 simulated years = 3.85 kgCO2e/simulated year`

2. Given by: `14,184 kgCO2e / 1,100 GPUh = 12.89 kgCO2e/GPUh`

:::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: callout

## Estimating emissions associated with future use of HPC systems

As well as using the HPC-CI metric as a tool to help quantify and reduce your emissions
from HPC system use it can also be used to project the emissions from HPC system use
from future or planned projects. Many funding bodies are starting to ask for emissions
estimates as part of the submission process. Calculating HPC-CI values can help you 
provide these estimates.

::::::::::::::::::::::::::::::::::::::::::::::::::

Now we understand how to estimate our emissions (HPC-E) and how to define a useful
metric to understand our emissions rate linked to some concrete output from our use
of HPC systems (HPC-CI). The next section looks at how emissions can be reduced and,
ideally, eliminated.

:::::::::::::::::::::::::::::::::::::::: keypoints

- The GHG protocol is a metric for measuring an organisation's total carbon emissions and is used by organisations all over the world.
- The GHG protocol puts carbon emissions into three scopes. Scope 3, also known as value chain emissions, refers to the emissions from organisations that supply others in a chain. In this way, one organisation's scope 1 and 2 will sum up into another organization's scope 3.
- You can use the GHG protocol to estimate your emissions from HPC system use but it requires access to reasonable quality information from the HPC systems you are using.
- The HPC-CI is a metric designed specifically to calculate emissions from HPC systems and is a rate rather than a total. This can be used to measure improvements in emissions efficiency and drive reductions in emissions.

::::::::::::::::::::::::::::::::::::::::::::::::::
