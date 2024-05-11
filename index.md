# Project

## Objective
To explore the significance of "self-reported health" as a health indicator. 

## Source of Data
- **Survey Data:**
Import the survey data from the 1999-2000 National Health and Nutrition Examination Survey (NHANES)

```stata
import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
```
- **Mortality Follow-up Data:**
Obtain follow-up mortality data to analyze over a 20-year period from the National Center for Health Statistics (NCHS). Detailed linkage instructions are available on the Linked Mortality page:
  - Health Statistics
      - NCHS
          - Datalinkage
              - Linked Mortality
                  - &nbsp; <kbd>NHANES_1999_2000_MORT_2019_PUBLIC.dat</kbd> &nbsp;
                  - &nbsp; <kbd>Stata_ReadInProgramAllSurveys.do</kbd> &nbsp; 
<br />

  ```stata           
  //data
   global mort_1999_2000 https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/NHANES_1999_2000_MORT_2019_PUBLIC.dat

  //code
  cat https://ftp.cdc.gov/pub/HEALTH_STATISTICS/NCHS/datalinkage/linked_mortality/Stata_ReadInProgramAllSurveys.do
  ```
  
## Code Development
  - **Edit Provided Script** <br />
    Download, modify and upload the provided Stata &nbsp; <kbd>.do file</kbd> &nbsp; for linking the &nbsp; <kbd>.DEMO.XPT</kbd> &nbsp; data to mortality follow-up data.     Rename file as followup.do and commit it with the description: <span style="color:red;">"Updated DEMO.XPT linkage .do file"</span>.
  - **Data Merging** <br />
    Merge the survey data with mortality data using the unique sequence numbers by executing the following stata code.

    ```stata
      //use your own username/project repo instead of the class repo below
      global repo "https://github.com/jhustata/intermediate/raw/main/"
      do ${repo}followup.do
      save followup, replace 
      import sasxport5 "https://wwwn.cdc.gov/Nchs/Nhanes/1999-2000/DEMO.XPT", clear
      merge 1:1 seqn using followup
      lookfor follow
    ```