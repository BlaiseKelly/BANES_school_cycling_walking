# AERMOD land use


# Introduction

The purpose of this analysis is to estimate the propensity to cycle for
school children in the BANES area. The postcode and school size of all
the schools have been obtained from the file
“spc_ees_school_characteristics.csv” which is part of the education
statistics portal:
https://explore-education-statistics.service.gov.uk/find-statistics/school-pupils-and-their-characteristics/2021-22
shown below:

The home postcode of the pupils has been estimated by assuming 80% of
pupils live within a 3km catchment of the school and randomly assigning
them to a postcode using the R dplyr function slice_sample and weighting
function 1/distance+population. Where distance is the distance from the
school to each postcode within the catchment and population is the
population of each postcode. This assumes that children are more likely
to live closer to the school and also more likely to live in a postcode
with more people.

Once the postcodes were estimated the routes from each postcode centroid
to the school postcode centroid were estimated using the osrm R package
which uses the Open Street Map (osm) routing engine to route. It is
possible to specify “car”, “bike” or “foot”. For this analysis “bike”
was selected. For the schools in BANES, estimating the journeys of 80%
of the pupils from each school resulted in 17550 routes.

The purpose of this analysis is to estimate which roads would see the
most cyclist journeys. To do this all the routes were input to the
stplanr R package ‘overline’ function which matches segments and sums up
the journeys for each one. The result is a map showing the osm road
segments by number of pupils estimated to travel this way each day,
shown below.
