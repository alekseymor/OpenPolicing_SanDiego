# OpenPolicing_SanDiego

## Project Overview
The data was obtained from The Stanford Open Policing Project (https://openpolicing.stanford.edu/data/).  
The datatset is cleaned data (by SOPP), with each row representing a police stop.   

The fields in this dataset are as follows:  
<table>
  <tr>
    <td>Column name</td>
    <td>Column meaning</td>
    <td>Example value</td>
  </tr>
  <tr>
    <td>raw_row_number</td>
    <td>An number used to join clean data back to the raw data</td>
    <td>38299</td>
  </tr>
  <tr>
    <td>date</td>
    <td>The date of the stop, in YYYY-MM-DD format. Some states do not provide
    the exact stop date: for example, they only provide the year or quarter in
    which the stop occurred. For these states, stop_date is set to the date at
    the beginning of the period: for example, January 1 if only year is
    provided.</td>
    <td>"2017-02-02"</td>
  </tr>
  <tr>
    <td>time</td>
    <td>The 24-hour time of the stop, in HH:MM format.</td>
    <td>20:15</td>
  </tr>
  <tr>
    <td>service_area</td>
    <td>Police service area. If not provided, but we have retrieved police
    department shapefiles and the location of the stop, we geocode the stop and
    find the service area using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>subject_age</td>
    <td>The age of the stopped subject. When date of birth is given, we
    calculate the age based on the stop date. Values outside the range of
    10-110 are coerced to NA.</td>
    <td>54.23</td>
  </tr>
  <tr>
    <td>subject_race</td>
    <td>The race of the stopped subject. Values are standardized to white,
    black, hispanic, asian/pacific islander, and other/unknown</td>
    <td>"hispanic"</td>
  </tr>
  <tr>
    <td>subject_sex</td>
    <td>The recorded sex of the stopped subject.</td>
    <td>"female"</td>
  </tr>
  <tr>
    <td>type</td>
    <td>Type of stop: vehicular or pedestrian.</td>
    <td>"vehicular"</td>
  </tr>
  <tr>
    <td>arrest_made</td>
    <td>Indicates whether an arrest made.</td>
    <td>FALSE</td>
  </tr>
  <tr>
    <td>citation_issued</td>
    <td>Indicates whether a citation was issued.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>warning_issued</td>
    <td>Indicates whether a warning was issued.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>outcome</td>
    <td>The strictest action taken among arrest, citation, warning, and
    summons.</td>
    <td>"citation"</td>
  </tr>
  <tr>
    <td>contraband_found</td>
    <td>Indicates whether contraband was found. When search_conducted is NA,
    this is coerced to NA under the assumption that contraband_found shouldn't
    be discovered when no search occurred and likely represents a data
    error.</td>
    <td>FALSE</td>
  </tr>
  <tr>
    <td>search_conducted</td>
    <td>Indicates whether any type of search was conducted, i.e. driver,
    passenger, vehicle. Frisks are excluded where the department has provided
    resolution on both.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>search_person</td>
    <td>Indicates whether a search of a person has occurred. This is only
    defined when search_conducted is TRUE.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>search_vehicle</td>
    <td>Indicates whether a search of a vehicle has occurred. This is only
    defined when search_conducted is TRUE.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>search_basis</td>
    <td>This provides the reason for the search where provided and is
    categorized into k9, plain view, consent, probable cause, and other. If a
    serach occurred but the reason wasn't listed, we assume probable cause.
    </td>
    <td>"consent"</td>
  </tr>
  <tr>
    <td>reason_for_search</td>
    <td>A freeform text field indicating the reason for search where
    provided.</td>
    <td>"odor of marijuana"</td>
  </tr>
  <tr>
    <td>reason_for_stop</td>
    <td>A freeform text field indicating the reason for the stop where
    provided.</td>
    <td>"EQUIPMENT MALFUNCTION"</td>
  </tr>
</table>

## Concept Overview


## Data Overview / Preparation Steps
Data ranges from 2014-01-01 to 2017-03-31.   
There are a total of 382,844 entries.  

A quick glace at the data revealed some entries that may cause problems down the line. The first such issue occurs in the 'raw_row_number' field. According to SOPP, if there was a single stop but multiple different violations or passengers then the rows were combined. As a result there are row number entries that appear as such: "407|408|409|410|411|412". For this analysis I will be omitting everything after the first separator (|) as there is no additional data linked to the other numbers.  
Next, I am going to remove the 'type' column as all of the stops fall under the 'vehicular' category.
## Application

## Results and Outcomes
I'll start with some descriptive statistics of the data. It appears that the average age of a subject is 37.1 and the median age is 34.0.  
Interestingly, the minimum age of a subject in the dataset appears to be 10, and the maximum agea appears to be 100. We will look closes at these (and similar) cases.

Next I'll look at the frequency distributions for the following fields: subject_race,	subject_sex,	arrest_made,	citation_issued,	warning_issued,	outcome,	contraband_found,	search_conducted,	search_person,	search_vehicle,	search_basis,	and reason_for_search.  

Looking at the racial breakdown of the data, it appears that most of the stops are of white subjects, accounting for 162,226 or 42.35% of the stops, followed by hispanic with 117,083 or 30.57%, and black with 42,705 or 11.14%.  I'll compare these figures with the census data for San Diego to see if they match.

![San Diego Police Stops By Race](https://github.com/alekseymor/OpenPolicing_SanDiego/assets/10982274/5158af80-85c2-4953-8cb2-6fe0c326681d). 

Of the 383,028 stops made between the years of 2014 and 2017, only 4,815, or 1.25%, resulted in an arrest. The majority of the stops, 219,712, or 57.36%, resulted in a citation.  
![San Diego Police Stop Outcome](https://github.com/alekseymor/OpenPolicing_SanDiego/assets/10982274/a76d833a-ca64-4d39-9fb9-222188ebe4e8). 



## Next Steps
