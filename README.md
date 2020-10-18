# Frac-Hit-Detection
Detecting frac hit events on oil wells using historical daily production data


# Motivation
A frac hit is an event in oil fields where the pressurized fluid from the fracturing of a well can make its way into the network of another offset well. While a direct, high-pressure frac hit on an operating well can cause damage to mechanical equipment on the wellpad, this possibility is protected against by shutting in nearby wells while a frac is occurring. However, these measures do not prevent the frac hit from occurring.

The impact of frac hits is not well understood by reservoir engineers and petrophysicists (from what the author understands). Access to more data on frac hits is helpful to increasing knowledge and drawing inferences. Unfortunately, most fracking has not been accompanied by high-quality data recording. Most frac hits have gone totally undetected and unstudied.

The algorithm in this repository can detect high-confidence frac hits using commonly available historical well economic data. With just well fracking time periods, well lat/long coordinates, and daily oil and water volume data, dozens of frac hits were detected. This is a low-cost, high-value method of extracting actionable information from freely available data.

# Impact
The author is not aware of specific business decisions made using this data, but certain assumptions about frac geometry were upended. Namely, frac hits were detected at further distance than previously assumed.

# Best indicators of frac hit in limited economic datasets
To state the most basic assumption - hydraulic fracturing is conducted using a water-based mixture of fluids, so wells which are hit by fracs should produce this fracturing fluid at the surface. Using the limited dataset at disposal and input from domain experts in reservoir and production engineering, the author constructed 3 criteria for labeling frac hits.
1. A frac must be occurring nearby at the time of the frac hit
2. A frac hit should increase expected volume of produced water at the affected well
3. A frac hit should increase expected ratio of water-to-oil or water-to-BOE (Barrel of Oil Equivalent, which includes oil and other lighter hydrocarbons)

# Elided Techniques
In an interest to have mercy on the reader, the author has obscured most of the work of data cleaning and exploration from this project in order to showcase the more novel and consequential parts of the code.

Elided data cleaning steps include:
1. Cleaning and imputing frac date periods
2. Finding mid-points between wellhead and well-toe to more precisely infer geometries

# Exhibited techniques in project
Given well locations, frac dates, and daily well production data, provide a count of "nearby fracks" at each well for each date.

Since it is common for nearby wells to have halted or "shut in" production during fracks, many frac hits will not be detected until the well is brought back online, which could be days or weeks after the end of the fracking period. So, nearby fracking time windows will need to be converted to match active "producing days" for the wells.

Time-dependent expected production characteristics need to be made for each producing well. For this project, the author chose a simple parameter-based model using '# of previous producing days' and '# of standard-deviations above mean' for Water volume and Water/Oil ratio to construct a trigger.

![An example frac hit](https://github.com/kialburg/Frac-Hit-Detection/blob/main/frac%20hit%20plots/4.png)

# Proposals for Improvement
Changing offset geometry from point-to-point to calculate distances between well laterals
Additional inputs for reservoir and well depth targeting
There is ample room for applying machine learning techniques to improve results, although a rigorously labeled set of training data would need to be constructed with input from a subject matter expert.

# Disclaimer
The sample data in this project originates in real data, but true dates, well identifiers, and locations have been obscured in order to protect proprietary information.
