# Citibike-May-2023-Report
Using PowerBI, I created the following report.
![citibike_0523](https://github.com/hanamartin876/Citibike-May-2023-Report/assets/98727041/a9e92d03-705a-496a-ba25-98d6f1a15310)

I downloaded Citibike's system data from May 2022, April 2023, and May 2023. I then used Power Query in PowerBI to aggregate the different datasets into one, and prepared the dataset for performing analysis.
Data source: [https://s3.amazonaws.com/tripdata/index.html](https://citibikenyc.com/system-data)
I used DAX to obtain new measures for the data analysis, including:
* Total Rides in May 2023.
  I previously created new columns containing the Month and Year of each particular ride, in order to facilitate the writing of DAX.
  0523 Total = CALCULATE(COUNT(citibike[ride_id]),citibike[Month]="May" && citibike[Year]=2023)
* Increase in Total Rides since the past month.
  Increase PM = 
    VAR pm = CALCULATE(COUNT(citibike[ride_id]),citibike[Month]="April" && citibike[Year]=2023)
    RETURN DIVIDE(citibike[0523 Total]-pm,pm)
* Increase in Total Rides since the past year.
  Increase PY = 
    VAR py = CALCULATE(COUNT(citibike[ride_id]),citibike[Month]="May" && citibike[Year]=2022)
    RETURN DIVIDE(citibike[0523 Total]-py,py)
* Duration.
  Duration = DATEDIFF(citibike[started_at],citibike[ended_at],MINUTE)
