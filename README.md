# Project-Highlights-
Some Images and Descriptions of Past Projects. Extension of cv

## Fuel Efficiency Models and Dashboard

One of my first ever projects was analysing fuel burn in commerical aviation, looking for potential savings. Over approximately a year this resulted in 14 fuel efficiency metrics showing where and how much fuel could be saved. 
This project also resulted in a set of time series lightdbm regression models (1 per aircraft model) that used flight recorder data estimate fuel burn. When compared to recorded fuel burn, my models significantly out performed alternatives such as https://openap.dev/fuel_emission.html. However I did have acess to much higher quality training data. These models allowed to evaluate counter factuals, such as fuel burn in flight profiles we believed superior, by modifying flight recorder data before the model injests the data. As an example a decent profile would be analysed and a more optimum profile generated. This flight data is then modified to match the optimized profile and a fuel burn model used to evualate the optimized fuel burn.
By the close of the project potential savings were in the 100s of kg per flight. This is proportionally small but adds up. Admitedly I dont think airlines have yet saw saving that large due to limitation on any changes to flight behaviour.
This project also included a streamlit dashboard used to view and agregate results.
Due to flight data being very dense and time series and the requirement to display agregations of results from large sets of flights a significant ammount of thought needed to be put into data engineering. I ended up making my own caching system that would attempt to retrieve a value from an sqllite db and only uppon failing generate the value before saving. This also extended to agregations and required all agregations to be parameterized by the group the agregation is based on.

## Study on Change In Turbulence Frequency 

Confirmed and re-visualized this https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2023GL103814 study on the effect of global warming on turbulence rates by leveraging Uber's H3 geospatial indexing, and massive amounts of past turbulence event information. The visualization, and confirmation of results, generated significant interest from airlines at aviation conferences.

