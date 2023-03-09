# Lunar-ML-Planetary_Albedo-mercury

The experiments presented here were made with the use of the datasets described next. For the Moon: albedo map, LPFe (iron map), LPK (potassium map), LPTh (thorium map), and LPTi (titanium) map. For Mercury: the albedo map which is split into the top and bottom of the planet, chemical maps - Al to Si element ratio, Ca to Si element ratio, Fe to Si element ratio, Mg to Si element ratio, S to Si element ratio. The maps are csv files with data that represents the element concentration at each location. 

The goal of this project is to contribute towards the creation of an ML pipeline that predicts the relationship between the albedo of Mercury and the chemical composition of its surface. However, there are two main "problems" we must tackle before we start applying ML models.

There is a lot of missing data on our Mercury surface datasets, especially around the North pole of the planet.
The data we do have was measured by MESSENGER from different distances, due the probe's highly elliptical orbit. This results in Mercury image maps with spatial resolution that varies depending on the coordinates of the pixel we're looking at.

Here: We create an adaptive smoothing algorithm that applies 2D Gaussian convolutions based on real planetary distances (in kilometers) and not pixels. This allows us to go from the 2D map projections of the planets to the 3D spherical representation of them.
We try this algorithm out on the Moon.
We apply various ML methods to see how well we can predict the relationship between the albedo and the chemical composition of the lunar surface. The reason we apply all of these on the Moon and not directly on Mercury is because we have no missing information about the Lunar albedo and the corresponding element maps are of high quality. Essentialy, the Moon serves as a benchmark before we get to Mercury.
As mentioned above, some of the data on Mercury is missing. We create "masks" based on these areas that have no data. Afterwards, we apply these masks to the lunar surface in order to simulate something we call "Mooncury" - a version of the lunar dataset where there is data missing in a pattern identical to the missing data on Mercury.
We apply ML on Mooncury. Essentially we have simulated areas of no data on the moon and we're trying to "fill in the gaps" before we attempt the same thing on Mercury (where the data is actually missing).
We create a latitude dependent smoothing algorithm which is an evolution of the adaptive smoothing algorithm and allows to apply Gaussian smoothing of different radii based on the latitude of the pixel.
We apply ML on Mercury.
Importing all of the necessary modules. My algorithms of choice for this notebook are XGBoost and polynomial regression. I chose XGBoost because it was the top performing model in the task. I also wanted to use a model that's not based on decision trees, so I went with poly.
