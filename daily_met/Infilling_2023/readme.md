## Miles used the scripts include here to infilling c1 data from 2023.

These scripts should be run in 1,2,3,4,5 order + optionally the `infilled_viz_check.R`
script.

`1_prepare_climate_data.R` - The code in this file was almost entire
unchanged from the example daily_met workflow included in
../v1_example_scripts/. It is necessary to run this to pull at the
latest data from EDI and the various nearby stations. This year we added improvements to
the data fetch function. No longer does the user need to manually download any data! All are 
retrieved programmaticly. There is some additional code in here for visualizing data quality 
from provided flags as well as data availability.

`2T_qc_[temp/ppt]_data.R` - This code is used to read in, clean, and visually
inspect the data that will ultimately be used to infill c1 temperature.

`3T_gapfill.R & 3P_gapfill_precip.R` - This is where the gapfilling takes place! Easily
recyclable across years and sites. Fairly simple script, infilling is done using both
methods described by TK & the best method is selected via pval/r2.

`4T_homogenize_sdlts.R` - This script was designed by CTW (as was basically all of this workflow)
and used to homogenize data across loggers / instruments since they each are liable to have 
minute systematic differences and experience sensor drift differently. CTW/TK used Double Mass Analysis
to identify periods requiring adjustment which is then calculated and applied. This script
homogenizes everything to 'match' the HMP155A's since that is what is primarily running
at Saddle now. In processing the 2022 data, I did not use any adjustments because
only the hmp155's produced data. I did however, run this script because some 
reformatting occurs here.
*Note* This script is not run for c1/d1, only saddle!

`5_prep_v1_forEDI.R` - This "pretties" all three datasets to produce the final
EDI ready data tables and writes them out!

`infilled_viz_check.R` - This is the code used to produce the plots
and conduct a cross-site comparison of the final infilled data for each site.

## Recommended Workflow

I recommend running step 1 first, and then spending a long time examining the data in step 2T 
and 2P. Once you're satisfied with the data that will be used to infill missing 
data across sites, running step 3 - 5 are pretty quick. Then you can run `infilled_viz_check.R` 
to generate a bunch of plots.

This year, I worked the whole time series of data (since one of the infilling methods requires
inter-year comparison), only infilled the last few years (~2020 - ) and then clipped to just include 2023
in the reformat scripts in  the *NWT_metadata* repository.
