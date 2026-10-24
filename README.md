# Skyline-Air-On-Time-Performance-Analysis
Excel and Power Query analysis of 1,000 airline flights: cleaning raw data, PivotTable analysis and an interactive dashboard to find why on-time performance is declining and where to act first.
# Skyline Air On-Time Performance Review

An Excel and Power Query analysis of one year of airline flight records, built to find out why on-time performance has been slipping and where an operations team should look first.

![Skyline Air on-time dashboard](https://github.com/ritaonuoha-portfolio/skyline-air-on-time-performance-analysis/commit/8951938fb894318772e074050b98f7175b7ba244)

## Project Overview

Skyline Air is a fictional mid-sized U.S. airline that operates domestic flights between major airports. This project was my Month 1 capstone for the Excel for Data Analytics course. I received a raw export of flight records, assessed its quality, cleaned it in Power Query, analyzed it with PivotTables, and presented the results in an Excel dashboard, a written report and a management presentation.

## Business Problem

Over the past year the airline's on-time performance has declined, customer complaints have increased and management has become concerned. The operations team has no single view of when delays happen, where they are concentrated or which factors contribute most. The data it had was an unstandardized export with duplicates, inconsistent labels and invalid values.

## Project Objectives

- Assess the quality of the data and document how each issue was handled
- Measure overall on-time performance and how it changes over time
- Find the airports, days, times of day and aircraft types most affected by delays
- Identify the most common delay causes and separate those the airline can influence from those it cannot
- Recommend where management should focus first, with evidence from the data

## Dataset Description

The dataset is a fictional raw export provided with the course brief. It has 1,012 rows and 13 columns. After removing duplicates it holds 1,000 unique flights from 1 September 2025 to 31 August 2026.

| Column | Description |
|---|---|
| FlightID | Unique identifier for each flight |
| FlightDate | Date of the flight |
| FlightNumber | Airline flight number |
| Origin / Destination | Departure and arrival airports |
| AircraftType | Aircraft used (Airbus A320, Boeing 737-800, Embraer E175, CRJ900) |
| ScheduledDeparture / ActualDeparture | Planned and actual departure times |
| DepartureDelayMin / ArrivalDelayMin | Delay in minutes at departure and arrival |
| DelayCause | Recorded cause of the delay |
| Status | Completed or cancelled |
| DistanceMiles | Flight distance |

**On-time definition:** a completed flight with an arrival delay of 15 minutes or less. Cancelled flights, and completed flights with no arrival data, are left out of on-time calculations, which leaves 957 flights.

## Tools Used

- **Excel Power Query** for cleaning and transformation
- **PivotTables and PivotCharts** for analysis
- **Slicers and conditional formatting** for interactivity and the heatmap
- **Excel dashboard** for the summary view
- **Word and PowerPoint** for the written report and the presentation

## Data Cleaning and Preparation

All cleaning was done in Power Query, so every step is recorded under Applied Steps and the original data stays untouched.

| Problem | Why it mattered | What I did |
|---|---|---|
| 12 duplicate flight records | Double-counted flights would distort every rate | Removed duplicates on FlightID (1,012 to 1,000 rows) |
| Airports written as codes, lowercase, with trailing spaces, or as city names | The same airport would appear as several in a PivotTable | Trimmed, converted to uppercase and mapped to 12 full airport names |
| Delay causes spelled many ways (for example WX, Carrier Delay, LateAircraft) and blanks written as null, none or None | Causes would be split across duplicate categories | Standardized to Carrier, Late Aircraft, Weather, ATC, Security and None |
| 6 impossible departure delays (for example 2,880 and -600 minutes) | They did not match the scheduled and actual times | Set to blank so they would not distort averages |
| 4 flights with a distance of 0 miles | Not physically possible | Set to blank; distance was not needed for the questions |
| 21 cancelled flights and 22 completed flights with no arrival data | No delay can be measured for them | Kept in the data, excluded from on-time calculations |

I then added five columns: Month, DayOfWeek, TimeOfDay (Morning, Afternoon, Evening, Night), OnTime (1 or 0) and Controllable (Carrier and Late Aircraft versus Weather, ATC and Security). Final check: 1,000 unique FlightIDs and 18 columns with no errors.

## Data Analysis Process

I built one PivotTable and chart for each business question:

1. **Overall performance:** average of the OnTime column, flight count, average arrival delay and cancellation share
2. **Monthly trend:** on-time rate by month, with dates grouped by months and years
3. **Airports:** on-time rate by origin airport
4. **Days and times:** on-time rate by day of week and time of day, shown as a color-scale heatmap
5. **Aircraft:** on-time rate by aircraft type
6. **Delay causes:** share of delays by cause
7. **Controllable factors:** controllable versus less controllable causes

## Dashboard Overview

The dashboard sheet has a title banner, three slicers (time of day, aircraft type, origin airport), four KPI cards and six visuals:

| Visual | Chart type | Question it answers |
|---|---|---|
| KPI cards: 74.8% on-time, 1,000 flights, 12.5 min average delay, 2.1% cancelled | Cards | How is the airline performing overall? |
| Monthly Trend | Line chart | How has performance changed over time? |
| Airports by On-time | Horizontal bar | Which airports struggle most? |
| Day by time-of-day grid | Heatmap | When do delays cluster? |
| Aircraft by On-Time | Column chart | Do some aircraft types perform worse? |
| Delay Causes | Column chart | What causes delays most often? |
| Controllable | Doughnut | How much can the airline influence? |

A line suits the monthly trend because time runs left to right. Bars rank airports and aircraft clearly. The heatmap shows two dimensions at once, and the doughnut shows a simple share of a whole.

## Key Findings

- **On-time performance is 74.8%** with an average arrival delay of 12.5 minutes and 2.1% of flights cancelled.
- **It has declined over the year.** The September to December 2025 average was about 80%, falling to about 72% for January to August 2026 and about 69% for May to August 2026. October 2025 was the best month (85.0%); February and May 2026 were the lowest (66.7%).
- **Atlanta is the weakest airport** at 65.4%, followed by Seattle (68.0%) and Los Angeles (71.9%). Las Vegas is the best at 86.0%.
- **Delays build through the day.** Morning departures are on time 79% of the time, afternoons 76%, evenings 68% and nights 66%. Night flights are few, so that figure is less reliable.
- **Aircraft differences are modest.** The A320 is lowest (71.3%) and the CRJ900 highest (78.9%), which may reflect the routes each aircraft flies.
- **Late Aircraft (32.2%) and Carrier (27.0%) are the top causes**, together about 59% of delay records. Weather accounts for 20.9%, Air Traffic Control 10.8% and Security 3.9%.

## Business Recommendations

1. **Start with Atlanta.** It has the lowest on-time rate and the heaviest traffic, so improvements there reach the most flights. Review turnaround and ground handling.
2. **Add schedule buffers in the afternoon and evening.** Late Aircraft is the top cause and evenings run 11 points behind mornings. This suggests delays are passed from one flight to the next, which should be tested with aircraft rotation data.
3. **Audit carrier-caused delays.** At 27% of delays and directly controllable, crew scheduling, maintenance planning and boarding are worth reviewing.
4. **Plan for weather.** It cannot be controlled, but contingency buffers at exposed airports can reduce its impact.
5. **Record a cause for every delay.** Some late flights have no cause recorded, which limits future analysis.

## Challenges and Solutions

- **A custom column to recalculate departure delay returned errors.** I switched to a simpler rule that blanks values outside a sensible range, and documented the choice, since on-time performance depends on arrival delay and is not affected.
- **Delay causes had several versions of "no cause" (null, None, blank).** I trimmed and capitalized the text first, then replaced each variant with one label.
- **Months sorted alphabetically.** Grouping the date field by months and years put them in calendar order across 2025 and 2026.
- **Cancellations were mixed in with completed flights.** A PivotTable on Status with values shown as a percentage of the grand total gave the cancellation rate.
- **Some groups are small.** Night flights and individual day-and-time cells contain few flights, so I flagged them as less reliable instead of building recommendations on them.

## Conclusion

The decline in on-time performance is concentrated rather than spread evenly: it is worst at Atlanta, gets worse later in the day, and is driven mostly by causes the airline can influence. Acting first on Atlanta's operations, schedule buffers and carrier-related processes offers the clearest route to recovery. The analysis also has limits: on-time is defined by arrival delay of 15 minutes, the data is fictional and simplified, and aircraft and airport comparisons show association, not proof of cause.

## Repository Structure

```
skyline-air-on-time-performance-analysis/
├── README.md
├── data/
│   └── Skyline_Air_Flight_Data.xlsx
├── excel/
│   └── Skyline_Air_Dashboard.xlsx
├── report/
│   └── Skyline_Air_Documentation_Report.docx
├── presentation/
│   └── Skyline_Air_Presentation.pptx
└── images/
    └── dashboard.png
```

## How to Explore the Project

1. Look at the dashboard screenshot at the top of this page for the summary.
2. Open `excel/Skyline_Air_Dashboard.xlsx` and use the slicers to filter by time of day, aircraft type or airport.
3. Open the PivotTable sheets to see the calculation behind each chart.
4. In Power Query (Data, Get Data, Launch Power Query Editor), open the cleaned query and read Applied Steps for the full cleaning process.
5. Read the report in `report/` for the method and findings in detail, or the presentation for the management summary.

## Author

**Rita Onuoha**, data analyst in training (Excel, SQL, Power BI, Python basics)
LinkedIn: [linkedin.com/in/ritachidimmaonuoha](https://www.linkedin.com/in/ritachidimmaonuoha)
