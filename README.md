# Project-Highlights-
Some Images and Descriptions of Past Projects. Extension of cv

## Automatic Key Point Value Data Validation 

A data validation tool designed to invalidate extreme outlier of vast set of aviation statistics. Tens of Thousands of kinds of values, Ie 'Max Groundspeed During Takeoff' 1000s created per flight. Sometimes inncorect due to broken sensors faulty code ect. 
As the tool needs to deal with so many types of values I took a very generalist approach and leveraged conditional distributions and bayesian analysis heavily. As not all of these values are expected to be normally distributed and I didnt want to write code for every possible distribution I also made heavy use of sklearns [Quantile transformer](https://scikit-learn.org/stable/auto_examples/preprocessing/plot_map_data_to_normal.html).
This project when combined with a similar event validation project I maintain (not discussed here) saves 100s of hours of analyst time a week that would otherwise need to be spent manually validating events.
The tool works by comparing a value being validated to various different conditional distributions of said value. One for the aircraft model, One for the analysis specification and version number, ect. For the first run the tool accumulates values until each distribution has a sufficient number of values. Once the distributions have been formed only the count, mean and variance of the normal mapping are saved. These values are updated using running versions of there formulai. With the distributions established simple Zscore analysis can be used for find extreme values.   
As even a quantile tranformer cannot always create an isomorphism to a normal distribution without horiffically overfitting. I found multimodal distributions where each mode is none symetric particularly troublesome. I managed to mitigate these issues by identifying problematic distributions pre transformation and writing custom solutions to the common low hanging fruit. For example a distribution resembelling 2 mirrored gumbel distributions formed from taking the most extreme value from a set of samples of normally distributed values, repeatedly. Can be seperated into 2 seperate distributions before 1 side is flipped and mapped onto the other such that the means are overlapping. This forms a close enough to normal distribution that a quantile tranformer can do the rest.  Some values such as 'Latitude at Touchdown' can never be meaningfully mapped to a normal distribution but the combination of custom solutions and the Quantile transformer was sufficient for the vast majority of not already normally distributed values. 
One issue is that a truly normally distributed value with a large portion in error may appear bi modal. While maintaining blindness to the context of the values this cant really be solved beyond statistical power based on sample size.

Many less extreme but still innacurate data points end up being consequtive, this happens as a result of broken sensors not being fixed for a few weeks or whatever else caused the issue persisting. Leveraging this I managed to flag a significant number of inncorrect values. 10 samples in a row all with Z score > 2 is an extremely strong indicator that somthing different was happening than the rest of the distribution.

## Fuel Efficiency Models and Dashboard

One of my first ever projects was analysing fuel burn in commerical aviation, looking for potential savings. Over approximately a year this resulted in 14 fuel efficiency metrics showing where and how much fuel could be saved.

This project also resulted in a set of time series lightgbm regression models (1 per aircraft model) that used flight recorder data to estimate fuel burn. When compared to recorded fuel burn, my models significantly out performed [alternatives](https://openap.dev/fuel_emission.html). However I did have acess to much higher quality training data. These models allowed to evaluate counter factuals, such as fuel burn in flight profiles we believed superior, by modifying flight recorder data before the model injests the data. As an example a decent profile would be analysed and a more optimum profile generated. This flight data is then modified to match the optimized profile and a fuel burn model used to evualate the optimized fuel burn.
By the close of the project potential savings were in the 100s of kg per flight. This is proportionally small but adds up. Admitedly I dont think airlines have yet saw saving that large due to limitation on any changes to flight behaviour.
This project also included a streamlit dashboard used to view and agregate results.
Due to flight data being very dense and time series and the requirement to display agregations of results from large sets of flights a significant ammount of thought needed to be put into data engineering. I ended up making my own caching system that would attempt to retrieve a value from an sqllite db and only uppon failing generate the value before saving. This also extended to agregations and required all agregations to be parameterized by the group the agregation is based on.

## Study on Change In Turbulence Frequency 

Confirmed and re-visualized [this meteorological study](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2023GL103814) on the effect of global warming on turbulence rates by leveraging Uber's H3 geospatial indexing, and massive amounts of past turbulence event information. The visualization, and validation of results, generated significant interest from airlines at aviation conferences.
For simplicity I only looked at if a 'severe' grade of turbulence was recorded. I think, this and my comparison not going back as far, is resposible for the significant changes in magnitude of results. However despite magnitudes of effect being different the same areas were all highlighted as increasing with similar relative rates. Its worth noting the original study uses mathematical meteorological modeling to predict were turbulence will increase. I simply took flight recorder data and after cleaning found the rates of turbulence being reported in a hex adjusted for ammount of time aircraft spent in said hex.  In the choropleth bellow only cells that had atleast 40K flights pass through are shaded.

<img src="https://github.com/11Kclarke/Project-Highlights-/blob/main/turbulence.png" alt="Visualization of Local Turbulence Changes"/>



## Generative Art

Generative are was one of the first things that got me interested in programming and maths. I sadly havent had much time to work on any of it for a while, but you can find on my github an infinite depth GPU accelerated fractal zoomer. As it uses Open cl it should be runnable even with AMD GPU without much faf. It Also allows for defining your own customer fractal seed equations instead of just the normal mandlebrott X^2+c. The zoomer isnt limited to escape type fractals and extends the use of customer seeds equations to julia set like fractals and more.
Theres also code for plotting images resulting from distance of jumps during attractor interation that produces images that i so far havnt seen anything similar to. Its Niche and useless enough it might even be unique.
![Example Attractor Art](https://github.com/11Kclarke/Project-Highlights-/blob/main/unknown.png)|  ![Inner Structure of Bulbs](https://github.com/11Kclarke/Project-Highlights-/blob/main/hoppalong-range-xy-are-x0y0-80-80%20zoomed%20spiral.png)
:-------------------------:|:-------------------------:
Example Attractor Art | Zoom of Inner Structure of bulbs 
  The most impressive component is probably the mapper from Sympy to Opencl syntax complete for any complex function writeable in expoential form Ie pretty much everything. This allows for GPU based iterations of custom functions. In retrospect im suprised this works given my experience level when writing it.

