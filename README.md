# Project_Spotify
# Spotify-Dashboard

## Problem Statement

This Power BI dashboard helps Spotify gain deeper insights into their users' listening habits and preferences. It enables Spotify to understand how often songs are streamed and the characteristics that make them popular, such as dance vibes, acoustics, and energy levels. By visualizing these metrics, Spotify can identify areas for improvement and enhance their music recommendation algorithms.

Through various visualizations, including bar graphs, heat-bar chart combos, and gauge charts, Spotify can track streaming trends, evaluate song attributes, and monitor the popularity of different artists. The inclusion of song cover images adds an engaging and intuitive element to the data presentation.

The dashboard's interactivity allows Spotify to filter data dynamically and drill down into specific metrics. This capability helps pinpoint trends and areas needing improvement. For instance, if certain song attributes are consistently less popular, Spotify can adjust their music curation strategies to better match user preferences.

Overall, this Power BI dashboard provides Spotify with the tools to enhance user satisfaction by tailoring music recommendations based on detailed streaming and song attribute analysis. As a result, Spotify can continuously improve their service by addressing identified areas of improvement and delivering a more personalized listening experience.

By using this dashboard, Spotify has identified key insights such as:

    User Engagement: Understanding which songs and artists are most popular based on streaming counts.
    Song Attributes: Analyzing how characteristics like danceability, acoustics, and energy impact song popularity.
    Performance Metrics: Monitoring the distribution of song attributes to refine music recommendations.

### Steps followed for making the base for making DASHBOARD:

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Select the tables you want to load and check for any errors in the data.
- Step 3 : Create the date column along with that create the necessary columns for the analysis.
- Step 4 : Create the measures for CALCULATING AVERAGE STREAM PER YEAR for all the songs which are streamed till 2023.
- Step 5 : Create the measure for CALCULATING MOST PLAYED SONGS for all the songs which are streamed till 2023. 
- Step 6 : Create the measure for FINDING THE TOP SONGS STREAMED till 2023.
- Step 7 : Create the measure for CALCULATING THE DIFFERENCE BETWEEN TOP vs AVERAGE SONGS for analyzing the reason for famousness and reason for song not being known as much it should have been.
- Step 8 : Create the measure for INSERTING IMAGE FOR COVER IMAGE OF SONGS.
- Step 9 : Create the measure for CALCULATING THE SONG'S ENERGY which would be displayed in gauge chart.  
- Step 10: Create the measure for CALCULATING THE NUMBER OF TRACKS which we have in our dataset.

### Steps for creating DASHBOARD:

        Once we have created measures we will start creating graphs and charts in order to start making DASHBOARD interactive and here's how we are going to do this:

- Step 1: We are going to create a BAR-CHART by using streams and the track name this would give us an interactive but it wold be the basic one but we will make it attractive later on.
- Step 2: We are going to create a LINE-CHART by using dates and tracks for helping us analyzing on the basis of the song's release date as it would help us in comparing with other songs which were released on the same day/date.                                               
- Step 3: We are going to create a KPI-CARD for displaying the average time the song was streamed per year since it was released.
- Step 4: We are going to create another KPI-CARD for displaying the percentage of Top vs Avg songs that would help us analzye the percentage of number of times the songs were streamed on the basis of the top songs which were streamed and average songs streamed. 
- Step 5: We will create the pie chart visual which would display the percentage of the energy in the song and also the shaded area would also be displayed. This visual would be created with the help of DENEB-VISUAL pack.
- Step 6: We will create a KPI-CARD visual which would be displaying the TRACK name, ARTIST NAME, RELEASE DATE, NUMBER of STREAMS and how many artists contributed to this particular track.
- Step 7: We will create another KPI-CARD visual which would be displaying the ACCOUSTICNESS, DANCEABILITY, LIVELINESS, SPEECHINESS and VALANCE of the songs.
- Step 8: We will create some slicers for the dashboard so that it would be used as filters which would help making the dashboard more interactive and those filter's would be consisted of Date, Trak name, Artists name, and Years.
- Step 9: We will create a heatmap and bargraph combo from DENEB-VISUAL pack which would consisted of MONTH, DAY of WEEK, TRACK for helping us understanding that when the song was released on the basis of day and month to track the number of releases in the same month and same day for  
- Step 10: Now we would create the background for the dashboard on POWER-POINT we can use the designer function in the power-point for creating the designer image in order to create an interactive dashboard and we would insert the shapes for creating the space for placing the visualizations in the dashboard. After inserting shapes and images we would be changing the colour scheme of the background and the image would be changed to resemble with the spotify's background and colour scheme. Since, we have changed the colour and inserted the shapes we would be adding the logo of the Spotify's logo and name along with the refresh logo for the dashboard refreshing it.	

Following are the DAX expressions used while creating these dashboards,
1) Average stream/year = CALCULATE(AVERAGE('spotify-2023'[streams]),ALLEXCEPT('spotify-2023','Date'[Year]))
2) Date = DATE([released_year],[released_month],[released_day])
3) Most Played songs = MAX('spotify-2023'[streams])
4) Top Songs Stream = CALCULATE(SUM('spotify-2023'[streams]),'spotify-2023'[streams]=MAX('spotify-2023'[streams]))
5) Top vs Avg Song = 
 VAR x =[Top vs avg val]RETURN

 IF(x>0,
 FORMAT(x,"#.0%")& "  " & UNICHAR(9650),
 FORMAT(x,"#.0%")& "  " & UNICHAR(9660))

6) Top vs avg val = DIVIDE([Top Songs Stream]-[Average stream/year],[Average stream/year])
7) Image_HTML = 
VAR x =
CALCULATE(
    MAX('Table 1 (Spotify Dataset)'[cover_url]),
    'Table 1 (Spotify Dataset)'[streams]=MAX('Table 1 (Spotify Dataset)'[streams])
)
RETURN

"<!DOCTYPE html> <html lang= 'en'>
<head>
	<meta charset='UTF-8'>
	<title>Image Cropping</title> <style>
	.image-container {
	width: 458px; /* Width of the container */
	height: 140px; /* Height of the container */
	overflow: hidden; /* Hide parts of the image that don't fit */ border-radius: 15px; /* Rounded corners */
	position: relative; /* Relative positioning for the child element */
	}

	.image {
	object-fit: cover; /* Cover the entire container */
	object-position: center; /* Center the image */
	width: 100%; /* Full width */
	height: 100%; /* Full height */
	}
	</style>
</head>
<body>
  <div class='image-container'>
    <img src='"&x&"' alt='Album Cover' class='image'>
  </div>
</body>
</html>
 "

8) Percentage_Value = 
AVERAGE('Table 1 (Spotify Dataset)'[energy_%])

9) Track_ = COUNT('Table 1 (Spotify Dataset)'[track_name])

10) Heat Map-Bar Chart = {
  "$schema": "https://vega.github.io/schema/vega-lite/v5.json",
  "usermeta": {
    "deneb": {
      "build": "1.4.0.0",
      "metaVersion": 1,
      "provider": "vegaLite",
      "providerVersion": "5.4.0"
    },
    "interactivity": {
      "tooltip": true,
      "contextMenu": true,
      "selection": true,
      "highlight": true,
      "dataPointLimit": 50
    },
    "information": {
      "name": "heatmap with bars - themed",
      "description": "Heatmap, uses the 5th theme color as bar chart, 8th color for font, and sentiment colors for gradient. X and Y axis are using Date table from Bravo, and are sorted for X= Month, Y = Day of Week. If you are using a different ordinal column, please make sure the columns are properly sorted",
      "author": "Injae Park",
      "uuid": "57ee5f3a-4a51-4230-8885-7db391a05805",
      "generated": "2022-10-19T11:12:58.962Z"
    },
    "dataset": [
      {
        "key": "__0__",
        "name": "Day of Week",
        "description": "From Bravo, is 3 character abbreviation, i.e. Mon, Tue, Wed",
        "type": "text",
        "kind": "column"
      },
      {
        "key": "__1__",
        "name": "Month",
        "description": "From Bravo, is 3 character abbreviation, i.e. Jan, Feb, Mar",
        "type": "text",
        "kind": "column"
      },
      {
        "key": "__2__",
        "name": "KPIa",
        "description": "",
        "type": "numeric",
        "kind": "measure"
      }
    ]
  },
  "config": {
    "autosize": {
      "type": "fit",
      "contains": "padding"
    },
    "view": {"stroke": "transparent"}
  },
  "data": {"name": "dataset"},
  "spacing": 15,
  "bounds": "flush",
  "vconcat": [
    {
      "height": 60,
      "mark": {
        "type": "bar",
        "stroke": null,
        "cornerRadiusEnd": 4,
        "tooltip": true,
        "color": {"expr": "pbiColor(4)"}
      },
      "encoding": {
        "x": {
          "field": "__1__",
          "sort": [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
            "Nov",
            "Dec"
          ],
          "axis": null
        },
        "y": {
          "field": "__2__",
          "aggregate": "mean",
          "axis": null
        }
      }
    },
    {
      "spacing": 15,
      "bounds": "flush",
      "hconcat": [
        {
          "mark": {
            "type": "rect",
            "stroke": "white",
            "tooltip": true,
            "cornerRadius": 6
          },
          "encoding": {
            "y": {
              "field": "__0__",
              "type": "ordinal",
              "title": "",
              "sort": [
                "mon",
                "tue",
                "wed",
                "thu",
                "fri",
                "sat",
                "sun"
              ],
              "axis": {
                "domain": false,
                "ticks": false,
                "labels": true,
                "labelAngle": 0,
                "labelPadding": 5,
                "labelColor": {
                  "expr": "pbiColor(7)"
                }
              }
            },
            "x": {
              "field": "__1__",
              "type": "ordinal",
              "title": "Time",
              "sort": [
                "Jan",
                "Feb",
                "Mar",
                "Apr",
                "May",
                "Jun",
                "Jul",
                "Aug",
                "Sep",
                "Oct",
                "Nov",
                "Dec"
              ],
              "axis": {
                "domain": false,
                "ticks": false,
                "labels": true,
                "labelAngle": 0,
                "labelColor": {
                  "expr": "pbiColor(7)"
                },
                "titleColor": {
                  "expr": "pbiColor(7)"
                }
              }
            },
            "color": {
              "aggregate": "mean",
              "field": "__2__",
              "type": "quantitative",
              "title": "Orders",
              "scale": {
                "scheme": "pbiColorLinear"
              },
              "legend": {
                "direction": "vertical",
                "titleColor": {
                  "expr": "pbiColor(7)"
                },
                "labelColor": {
                  "expr": "pbiColor(7)"
                },
                "gradientLength": 100
              }
            }
          }
        },
        {
          "mark": {
            "type": "bar",
            "stroke": null,
            "cornerRadiusEnd": 4,
            "tooltip": true,
            "color": {
              "expr": "pbiColor(4)"
            }
          },
          "width": 60,
          "encoding": {
            "y": {
              "field": "__0__",
              "axis": null,
              "sort": [
                "mon",
                "tue",
                "wed",
                "thu",
                "fri",
                "sat",
                "sun"
              ]
            },
            "x": {
              "field": "__2__",
              "type": "quantitative",
              "aggregate": "mean",
              "axis": null
            }
          }
        }
      ]
    }
  ]
}

After all the steps the final dashboard should look something like:
https://github.com/Akulv19/Project_Spotify/assets/171360978/58238882-99c4-47c2-a7ac-af31bcd4faf3

