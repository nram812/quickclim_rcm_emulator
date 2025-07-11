## Notes from Collaboration

# SSH into GADI:
ssh nr4680@gadi.nci.org.au


I’ve put together an initial dataset for you. I’ve generated 10 different emissions pathways with final end-of-century carbon equivalent concentrations equally spaced from just above that of RCP8.5 to just below that of RCP2.6.  I can do as many as emissions pathways as you like, and with whatever trajectory you like. In our papers we typically do 100 pathways, but 10 should be enough to test that everything is working OK.



The data can be found on gadi at the following location:

gadi.nci.org.au:cd 

To be able to access the data you’ll need to request access to the project v14 . To do so you’ll need to log in to https://my.nci.org.au/mancini/login. I’ve already mentioned this to the approver of the v14 project, Terry O’Kane, so he’s expecting your request.  If this is not practical, we can find another way to share the files.

 

Here’s a brief explanation of the files in the aforementioned directory:

FEMBVVARX_modelXX_temporal_params.pickle – This contains the ML coefficients for each CMIP5 model of index XX.
modelXX_expYYYY.nc – This is the QuickClim reconstruction of the required variables on the global grid with monthly averages for CMIP5 model XX and emissions pathway of index YYYY. This includes both the climate change and climate variability components.
modelXX_expYYYY.cc_delta_rcp45.nc – This is the climate change component of the required variables on the QuickClim reconstruction minus the climate change component of the RCP4.5 scenario of the global grid with monthly averages for CMIP5 model XX and emissions pathway of index YYYY. Adding this “delta” to the RCP4.5 scenario returns modelXX_expYYYY.nc at monthly timescales.
modelXX_expYYYY.daily.nc – This is what you need for your downscaling. It is the QuickClim reconstruction of the required variables on the local grid with daily averages for CMIP5 model XX and emissions pathway of index YYYY. The data in modelXX_expYYYY.cc_delta_rcp45.nc was interpolated to daily resolution then added to the RCP4.5 daily fields. At this stage these are finished for the first CMIP5 model (i.e. XX=00 of files model00_exp*.cc_delta_rcp45.nc). My code is still running to generate the other CMIP5 models. I’ll let you know when all the others are done. The files associated with the first CMIP5 model should be enough to figure out if everything is in order or not.
 

Note, the example data set you provided in your email below was from 1960 onwards. Whereas the QuickClim projections I’ve provided are aligned with the future CMIP5 projections from 2006 onwards. There was also a slight issue with some of the fields at 850hPa when cutting through topography. Some of the CMIP5 models set those values to NaN, whilst others provide interpolated values. I’ve got some logic to set the NaNs to zero during the model reduction process. Any values that were NaN in the inputs are then also NaN in the QuickClim output. I don’t think this is an issue over New Zealand though, but be an issue for certain CMIP5 models where the longitudes wrap around. I’ve done a basic sense check, but let me know if you find anything that seems odd. Happy to make modifications and produce a new version of the data as need be. I’m going to be away in Europe now for the next couple of weeks. I’ll try to sort out whatever issues there might be while I’m away.

 