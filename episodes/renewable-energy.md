---
title: Renewable Energy
teaching: 30
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Gain a more detailed understanding of how renewable energy feeds into reducing emissions.
- Understand the limits of Renewable Energy Certificates.
- Learn about different renewable energy matching approaches.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What does 100% renewable energy actually mean?
- How do we claim 100% renewable energy on a power grid with mixed energy sources?
- What impact do different renewable energy matching strategies make?

::::::::::::::::::::::::::::::::::::::::::::::::::


## 100% Renewable

When organisations set a target of 100% renewable power, they might distinguish between being **matched by** vs. **powered by** renewable energy sources.

**Powered by** means you are directly powered by a renewable power source, say a hydro dam. In that scenario, the energy the device receives only originates from that source, so you can confidently say that you are 100% powered by renewables.

For most people, we live on an interconnected grid, with many producers pumping electricity in and many consumers taking electricity out. This means the electrons coming into your device are a mixture of all the electrons going into the grid. For example, suppose the grid only has 5% of wind supply. You are getting 5% of wind-generated electrons and 95% fossil fuel-generated electrons.

You cannot track individual electrons. Once the electrons from a wind farm are on a grid, they all mix with the electrons from a fossil fuel plant. So there is no way for a consumer to insist the electrons that it uses only come from renewable sources.

### Renewable Energy Certificates (REC)

To solve this problem, a renewable plant sells two things. The first is its electricity, which it sells into a grid. The second is a REC, a [Renewable Energy Certificates](https://www.epa.gov/green-power-markets/renewable-energy-certificates-recs). 1 REC equals 1 kWh of energy.

If you want to be 100% matched by renewable energy and are on the grid, the solution is to buy enough RECs to cover the amount of electricity you consume. For instance, if you consume 100 kWh of electricity every day, then to be 100% matched by renewables, you buy 100 RECs.

When organisations set 100% renewable targets purchasing RECs on the market is the solution they often employ to meet their commitments.

### PPAs

You might also hear the term PPA used alongside RECs. A PPA is a [Power Purchase Agreement](https://ppp.worldbank.org/public-private-partnership/sector/energy/energy-power-agreements/power-purchase-agreements), which is another way to purchase RECs. If you estimate you need 500 MWh of electricity per year for a particular data center, you might sign a PPA to purchase 500 MWh per year from a renewable plant. You would then get all the RECs associated with this power plant.

PPAs are typically very long-term contracts. A renewable plant can find financing with one of these agreements since it already has had a buyer for its electricity for many years.

PPAs encourage something called **additionality**. Purchasing a PPA drives the creation of new renewable plants. PPAs are a solution that gets us towards a future where everyone has access to 100% renewable energy.

## 24/7 Hourly Matching

When it comes to 100% renewable claims, the critical question is, what is the granularity of matching? Do you sum up and net off yearly, monthly, weekly, daily, or hourly? That question is essential because to truly transition to renewable energy, we need 100% of the power to come from low-carbon energy sources like renewables 100% of the time. This fine granular matching is often called _[24/7 hourly matching](https://www.epa.gov/green-power-markets/247-hourly-matching-electricity)_.

24/7 hourly matching is one of the many strategies we need to employ to help accelerate the transition to a 100% renewable-powered grid. For example, [Google](https://sustainability.google/progress/energy/) and [Microsoft](https://blogs.microsoft.com/blog/2021/07/14/made-to-measure-sustainability-commitment-progress-and-updates/) have both committed to 24/7 hourly matching by 2030.

### Daily vs hourly matching

Imagine an organisation has a demand curve like this, each blue square represents 1kWh:

![Demand curve for electricity use](./fig/29_daily_consumption.png "Demand curve for electricity use")

They have purchased RECs from a wind farm that generated electricity with a curve, so each green square represents 1 REC. Matching by day means the organization consumed 18 kWh and bought 18 RECs. As a result, they netted off to zero. So they can say they are **100% matched by renewable energy daily.**

However, if we looked at it in hourly buckets (each square here is 2 hrs in length), then it seems a bit different:

![Diagram illustrating impact of hourly matching](./fig/30_hourly_match.png "Diagram illustrating impact of hourly matching")

The total amount of energy consumed is still 18kWh. However, there are only a few hours in the day where we are 100% matched by renewable energy for that hour. So for some hours, we have way more renewable energy than we need. Conversely, we have way less renewable energy than we require for most hours.

In the above example, they are **100% matched by renewable energy on an hourly basis for only 6 hrs of the day**.

### Carbon-free energy

The number we use to describe how successful we are at 24/7 hourly matching is the carbon-free energy percentage.

Carbon-free energy is defined as [the average percentage of carbon-free energy consumed in a particular location on an hourly basis](https://cloud.google.com/sustainability/region-carbon#understanding).

So for the previous example, if measured using daily matching, we are 100% matched with renewable energy. However, we are only 33.1% matched if measured using hourly matching. **The CFE percentage is, therefore, 33.1%**.

### Carbon Awareness as part of a 24/7 Hourly Matching Strategy

Carbon aware computing involves responding to electrical carbon intensity signals and changing the **behavior** of software, so it emits less carbon. Carbon awareness also helps an organisation meet their 24/7 hourly matching target and increase its CFE percentage.

One example of a behavior change is shifting compute to a time when more renewable energy is available. For example, delaying the start of a power intensive simulation (or even delaying charging of a laptop) to when the carbon intensity of electricity is lower, and the supply of renewable energy is higher.

![Temporal shifting along with matching strategy](./fig/31_carbon_awareness.png "Temporal shifting along with matching strategy")


:::::::::::::::::::::::::::::::::::::::: keypoints

- "Powered by" 100% renewable energy means that renewable energy sources are directly connected to the HPC system.
- "Matched by" 100% renewable energy means that the electricity for the HPC system is purchased from the grid along with renewable energy certificates to the same capacity as the usage.
- When electricity is "matched by" 100% renewable energy the matching interval has a large impact on how it drives transition to green energy. The term "carbon free energy" is used to quantify how well we are matched on a 24/7 basis.
- Large power purchase agreements (PPA) can be designed to incentivise the transition to green energy.

::::::::::::::::::::::::::::::::::::::::::::::::::
