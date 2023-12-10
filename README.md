# GEO-AI Challenge for Landslide Susceptibility Mapping by AI for Good ‐ International Telecommunication Union

**This project achieved the 1st place Zindi's [GEO-AI Challenge for Landslide Susceptibility Mapping](https://zindi.africa/competitions/geo-ai-challenge-for-landslide-susceptibility-mapping/) competition!!!**

This repository contains the code used for my submission for Zindi's [GEO-AI Challenge for Landslide Susceptibility Mapping by ITU](https://zindi.africa/competitions/geo-ai-challenge-for-landslide-susceptibility-mapping/) competition. The goal of the challenge was to develop an accurate and cost-effective model for landslide susceptibility mapping in the Valtellina Valley region in Italy using machine learning techniques.

You can watch [my presentation on the challenge finale](https://www.youtube.com/live/0iC2AZsov4I?si=DvOSV3ZJXBMJkMMO&t=1437), where I explain my approach. Also [later in the video](https://www.youtube.com/live/0iC2AZsov4I?si=_l8aurb8eY0foafi&t=2555) you can see my 1st place certificate!

![Final susceptibility map](map.png)

My submission for the competition used the only the official [datasets provided by the competition hosts](https://zindi.africa/competitions/geo-ai-challenge-for-landslide-susceptibility-mapping/data). In order to engineer features I created a circular buffer zone for each data point with the following radii: 100 m, 500 m, 1 km, 2.5 km, gathering information and relevant characteristics present in these areas. This is done because given that we want to model landslide susceptibility, the information present directly within the geometry that we're considering might not be enough. For instance, the fact that there's a river 50 m away from the geometry we're analyzing might make it more susceptible to a landslide, even though the river isn't crossing directly thorough the geometry. After acquiring and engineering the features, I used a LightGBM model to fit the data, performing a hyperparameter search with Optuna with 5-fold cross-validation to achieve the best performance. After 100 optimization trials, the model achieved an accuracy of 96.82% on the 5-fold cross-validation, leading to a score of 94.67% on the final competition leaderboard. 

## Repository structure

- `main.ipynb`: Jupyter notebook file containing my complete analysis, thoroughly explained. I recommend using the following [nbviewer link](https://nbviewer.org/github/zysymu/GEO-AI-Challenge-for-Landslide-Susceptibility-Mapping/blob/main/main.ipynb) to visualize it online.
- `GEO-AI Challenge for Landslide Susceptibility Mapping report.pdf.pdf`: an executive summary explaining the development of my features and model.
- `colorful_100.qgz`: final QGIS susceptibility map, where 1 are areas with very low probability of landslides and 5 are areas with very high probability.
- `map.png`: picture from the final susceptibility map. Green are areas with very low probability and red are areas with very high probability. The points indicate the location of the test set data.
- `data`: directory containing all of the data used.
    - `datasets`: directory where the data provided by the competition hosts should go.
    - `predictions.csv`: final predictions used for the competition.
    - `*` (other files): intermediate files that can be useful to reproduce the code.
