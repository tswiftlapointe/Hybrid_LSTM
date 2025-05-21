# Hybrid Statistical-Dynamical Forecast for Seasonal Streamflow in the Columbia River basin

This repository contains the code used in the study:

Swift-LaPointe, T., White, R.H., and Radic, V.  "A hybrid statistical-dynamical forecast of seasonal streamflow for the Columbia River basin in Canada" (Submitted 2025).

The code in this repository can reproduce all figures in the study, as well as provide an example to train one hybrid statistical-dynamical forecast as used in the study. The repository contains the following:

* Data_setup.ipynb: Loads raw data (temperature, precipitation, streamflow), processes into format required for Train_LSTM_example.ipynb. 
* Train_LSTM_example.ipynb: Defines functions, loads preprocessed data, trains LSTM model, creates hybrid forecast for one example test year.
* Paper_figures/: Directory that contains code, data to reproduce figures, figure pdf files.
  * Figures_code.ipynb: Code to reproduce all figures
  * Data_for_figures/: Contains all data to reproduce figures.
    * Elevation_data/: Directory containing NOAA ETOPO Elevation data files required for Figure 1 (NOAA, 2022).
* indices_example.csv: Example training, validation, and testing year indices for one example test year (1982), as used in Train_LSTM_example.ipynb.
* indices_example1.csv: Example training, validation, and testing year indices for one example test year (2014), as used in Train_LSTM_example.ipynb.
* Mica_basin_outline.csv: Basin outline coordinates for the Kinbasket Lake Reservoir catchment, from Environment and Climate Change Canada: National hydrometric network basins polygons dataset (Environment and Climate Change Canada, 2016).

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.15483232.svg)](https://doi.org/10.5281/zenodo.15483232)

## Steps to build example hybrid forecast

Local file organization should be as outlined below before proceeding. Create new directory ./Hybrid_LSTM/Data/ to hold the preprocessed data.

1. Download Bonneville Power Administration 2020 Level Modified Flow daily data (Dakhlalla et al., 2020) from [here](https://www.bpa.gov/energy-and-services/power/historical-streamflow-data). Only the file MCD6A_daily.xlsx is required, save this as .csv in Hybrid_LSTM/Data/.
2. Download ERA5 reanalysis data (Hersbach et al., 2020) as specified in Data_setup.ipynb from [here](https://cds.climate.copernicus.eu/datasets/reanalysis-era5-single-levels?tab=download). Save this data locally in Hybrid_LSTM/Data/.
3. Download ECMWF SEAS5 seasonal forecast data (Johnson et al., 2019) as specified in Data_setup.ipynb from [here](https://cds.climate.copernicus.eu/datasets/seasonal-monthly-single-levels?tab=download)
5. Run Data_setup.ipynb to convert raw data into monthly-averaged format required for Train_LSTM_example.ipynb.

Train_LSTM_example.ipynb is set up to run in Google Colab, as this gives access to a GPU which can significantly speed up computation time when training the LSTM model. Google Colab accesses data in Google Drive and all outputs are saved in Google Drive. Thus, input files must be uploaded to an appropriate folder in Google Drive. Google Drive file organization specified below.

5. Upload the preprocessed input data from Step 5 to Google Drive in folder './Hybrid_LSTM/Data/'.
6. Upload the files indices_example.csv and indices_example1.csv to Google Drive in folder './Hybrid_LSTM/Output/'.
7. Run Train_LSTM_example.ipynb.

## File Organization

Local organization:
* Hybrid_LSTM/
  * Data_setup.ipynb
  * Train_LSTM_example.ipynb
  * indices_example.csv
  * indices_example1.csv
  * Mica_basin_outline.csv
  * Paper_figures/
    * Figures_code.ipynb
    * Data_for_figures/
      * Data need for creating figures (.csv)
      * Elevation_data/
        * ETOPO_2022_v1_15s_N60W120_surface.nc
        * ...
        * ETOPO_2022_v1_15s_N75W150_surface.nc
    * Fig01.pdf
    * ...
    * Fig12.pdf
  * Data/
    * MCD6A_daily.csv
    * ERA5_T2m_1981_2017_6hourly_ecmwfgrid.nc
    * ERA5_Precip_1981_1993_hourly_ecmwfgrid.nc
    * ERA5_Precip_1994_2006_hourly_ecmwfgrid.nc
    * ERA5_Precip_2007_2017_hourly_ecmwfgrid.nc
    * SEAS5_forecasts_1981_2017_monthly.nc

In Google Drive, for using Google Colab:
* My Drive/  
	* Colab Notebooks/  
		* Hybrid_LSTM/   
			* Data/
              * BPA_monthly_volumes_1981_2017.csv
              * Monthly_input_Mica_1981_2017.csv
              * Monthly_climatology_Mica_1981_2017.csv
              * SEAS5_monthly_input_Mica_1981_2017.csv
			* Output/
              * indices_example.csv
              * indices_example1.csv
			* Models/
 
## References

* Dakhlalla, A., Hughes, S., McManamon, A., Pytlak, E., Roth, T. R., and van der Zweep, R.: 2020 Level Modified Streamflow: 1928-2018, Bonneville Power Administration, Department of Energy, Portland, OR, 2020.
* Environment and Climate Change Canada: National hydrometric network basin polygons, https://open.canada.ca/data/en/dataset/0c121878-ac23-46f5-95df-eb9960753375 (last access: 10 March 2025), 2016.
* Hersbach, H., et al.: The ERA5 global reanalysis, Quarterly Journal of the Royal Meteorological Society, 146, 1999–2049, https://doi.org/10.1002/qj.3803, 2020.
* Johnson, S. J., et al.: SEAS5: the new ECMWF seasonal forecast system, Geoscientific Model Development, 12, 1087–1117, https://doi.org/10.5194/gmd-12-1087-2019, 2019.
* NOAA:National Centers for Environmental Information: ETOPO 2022 15 Arc-Second Global Relief Model, https://doi.org/10.25921/fd45gt74 (last access 12 Sep 2024), 2022.
