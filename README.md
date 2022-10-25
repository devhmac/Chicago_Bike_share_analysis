# Divvy Bikeshare Ridership Analysis

This project utilized various technologies to clean, manipulate, transform, analyze and finally visualize a bike share ridership dataset. 

- Python: Cleaning, transforming, enhancing and analyzing our dataset. 

- SQL: Validation, and exploratory, impromptu analysis.

- Tableau: Visualization and Dashboard creation. 

<div align="center"> 
  
## [Tableau Dashboard linked here](https://public.tableau.com/app/profile/devmac/viz/ChicagoBikeShareAnalysis/BikeUsageDashboard) 
### [Code linked here](https://github.com/devhmac/Chicago_Bike_share_analysis/blob/main/chicago_bike_share_analysis.ipynb)
  
</div>

## Business Case

Divvy is a Chicago-based bike share company using the Lyft platform to allow users to hop on and ride one of over 16 000 bikes at over 800 different station locations across the city. Members are the more profitable segment, so exploring the difference between the two user groups will be the focus of our analysis. 

1. How do annual members and casual riders use Divvy bikes differently?
2. Why would casual riders buy annual memberships?
3. How can the business use digital media to influence casual riders to become members?

## Data

A first-hand [dataset](https://divvy-tripdata.s3.amazonaws.com/index.html), containing trip information for over 5 million trips between Sept 2021 to Aug 2022. Data going back to 2019 is available, but for this project, we have decided on the most current 12-month range available. 

The dataset used came in 12 individual CSV files, containing each individual month's trip data. 

**Licence:** Lyft has provided a royalty-free, limited, perpetual license to access, reproduce, analyze, copy, modify, distribute in your product or service and use the Data for any lawful purpose.

### Data credibility and limitations

With over 5 million trips tracked across 12 months, this dataset is quite robust and provides enough of a sample to represent overall user trends. But we are limited in additional user information, such as the intention of a trip etc. that might help us make a more personalized user segment analysis. 

Initially- The dataset contains; a unique trip ID. bike type, trip start & end time, latitude & longitude of trip start and stop, as well as info on most start and stop stations. 

## Data setup and merging

We completed our data cleaning and processing work in Python, with the pandas and numpy libraries. 

<img src="https://user-images.githubusercontent.com/52307383/197649632-c3587abe-54f2-4b13-8625-70d9bf1bf5f5.png">
<img src="https://user-images.githubusercontent.com/52307383/197649649-94be0e94-761e-4926-855a-3b538b3ef69d.png">

After importing our data we explored each set to confirm column names and data types were compatible. Once confirmed, we merged all 12 sets.

<img src="https://user-images.githubusercontent.com/52307383/197649747-ee990681-7f89-4e3c-b492-1fb36247a9e3.png">

## Cleaning

- Started with confirming the data types of our columns.
<img src="https://user-images.githubusercontent.com/52307383/197649800-944ea2fb-e181-48a4-aad8-5cdaeb899084.png">

- First, we checked for and dropped duplicate rows (there were none). We then noted that start and end times were objects. We translated them to datetime to perform calculations on them for additional data points.

<img src="https://user-images.githubusercontent.com/52307383/197650034-d39d997b-1b5a-422e-a906-88417be8d4f3.png">

Next we added 3 new columns to our dataset, which will provide additional value during the analysis process. 

- Changed the name of the “member_casual” column to “rider_type”.
- Added “Weekday” column, tracking the day of the week each trip took place.
- Added “Month” column, tracking the month of each ride.
- Calculated the trip duration of each ride using the start and end date column of each row. We decided to store this in minutes, rounded to 2nd decimal point.

<img src="https://user-images.githubusercontent.com/52307383/197650061-7e56e96e-b463-44e9-94e9-90f4b1853707.png">

The Jupyter notebook Deepnote allows for the use of SQL on dataframes, which allows for an incredibly efficient combo of the two languages. We leveraged this to perform a few quick data validation queries to check if our set had any incomplete or corrupted trip data. 

See a few of these queries below;

<img src="https://user-images.githubusercontent.com/52307383/197650105-ce0e522b-1224-4786-b8e6-9dedb968e698.png">

Luckily all rows appeared to have complete trip data. Many rows were missing station names and ID’s, but even in those cases Lat and Long of both start and end locations were still recorded. 

Next, we checked the trip duration, to confirm our trip lengths made sense contextually. 

<img src="https://user-images.githubusercontent.com/52307383/197650143-9f3fad20-774a-4924-8fbd-fb5234db1ff8.png">

We found 110578 trips with a duration below 1 minute, which seemed potentially problematic. After some research on Divvy’s data capture techniques, we found they recommend that trips under 1 minute be considered false starts of errors, so we dropped these from our set. 

<img src="https://user-images.githubusercontent.com/52307383/197650167-230ad308-5f5a-4dfa-be72-1e9d3dd50e63.png">

Now confident in our data, I split our set in two, one with location data removed for a customer-focused analysis, and the other for a future project to analyze location-based ridership trends and geo-mapping. 

## Analysis and visualization

Focusing our analysis on the difference between membership and casual rider use trends uncovered to some interesting findings. 

<img src="https://user-images.githubusercontent.com/52307383/197650230-abbc861f-abdd-46c0-b3c3-f0897aa1df76.png">

- Of the total 5 million trips, 57.79% were taken by members (2,917,645).
- More interesting, however, despite accounting for the majority of all rides, member ride only account for 42.34% of the total time spent riding bikes. 626,269.6 of 1,479,144 hours annually. Let's dig into this trend further.

<img src="https://user-images.githubusercontent.com/52307383/197650287-3dc3c7ca-9f8e-4936-bd1e-60ae6ea2ad6b.png">

- After further analysis, on average the length of casual rider trips are almost double that of member rides.

This is interesting in addition to the result above. It adds further context\ further context to why members are the more profitable user group. Despite using the product more frequently than casual riders they are on the bikes less per trip, enabling the bikes to be more readily available for the next user.  

<img src="https://user-images.githubusercontent.com/52307383/197650345-b1ec62aa-aa20-4cb8-9244-9c81c7199fc0.png">

A quick analysis of the types of bikes ridden over the last year shows the docked bikes were the least popular, and actually accounting for no rides in the member segment. Despite being relatively close, members seem to lean towards the classic bikes, where as casual riders prefer electric. 

<img src="https://user-images.githubusercontent.com/52307383/197650372-593fc548-f6d9-4a69-811c-896b57f697ad.png">

During weekdays (Mon - Fri) casual riders take significantly more trips than casual users. 

- Peaking on Tuesday at almost double (458,070 member vs  239,663 casual)

This pattern is biased towards the start of the week, as it goes on the gap between the two rider groups slightly narrows. By the weekend, casual rider trips actually exceed those of the member segment. 

A trend is emerging in the visualizations above. With casual riders taking longer trips on average, and exceeding member trips on weekends, I predict these rides represent leisure activities - compared to the member segment taking expedient trips on weekdays, which seems to represent commuting behaviour.

<img src="https://user-images.githubusercontent.com/52307383/197650481-4ffbddd9-7478-4c50-b83b-6e3e7eb21c30.png">

When comparing trips to time of day, our above thesis is reinforced. 

- Member rides peak at prime commuting times, 6am-9am and 5pm. In evening the gap between the rider groups reduces.
- On weekends, after 11am casual rides exceed member rides for almost the rest of the day.

User interviews should be conducted to confirm the different use patters, but the above plot clearly demonstrates the difference between the casual rides and the more commute focused member rides. 

<img src="https://user-images.githubusercontent.com/52307383/197650537-0dc3626d-8bef-4174-bc6e-aa18e7ff9855.png">

Unsurprisingly, we see total rides are much higher in the warmer months. In the off months, Oct - April, we see the biggest gaps between segments. The largest differences being Oct-Dec. 

- Apr. - Jul. we see a steady growth in both groups rides, until August, where member rides continue to climb, but casual rides drop. This would be a great spot to market towards casual users and attempt to increase their ridership.

Additional data should be collected on the reason for Casual rider reduction during this summer month. 

- In July, casual and member rides are almost neck and neck, this would be an excellent opportunity to try to convert some of the high casual users to members.
- Member riders are much higher users in the colder months, approximating that the segment is using the service less for pleasure/leisure acitivies, and more as an effective form of transportation, particularly in these months where outdoor activities are less desirable.

## Overall Trends

Member riders take shorter rides, peaking Monday - Friday during commuting hours. Members continue to ride into the colder months at a much higher rate than the casual counterparts. 

The casual segment have a take longer rides, with their highest ridership on on Saturday and Sunday afternoons, without the distinct peaks during commuting times. 

Member ridership increases steadily all the way to August, where it begins to decline during the colder months. Casual ridership sees a notable drop in August, when compared to the steady increase in use leading up to July. This would be an interesting month for further analysis. 

- One possibility is we are converting a section of the casual rider group into members during this month, but the increase in member rides seen does not quite equate to the reduction in casual rides, so there are additional factors at play.

Customer interviews would confirm or disprove our hypothesis that Member riders use the service primarily for functional transportation and commuting, where as casual riders use leans more towards, leisure activities and pleasure, with a focus on weekends, warmer summer months, and longer rides overall. 

## High-level Recommendations

- Add additional perks or incentive to membership, specifically for the recreational evenings and weekend ride behaviours. Perhaps monthly ‘bring a friend for free’ passes, which could also expand the overall user network.
- Evaluate alternate membership types providing more value for casual user ride trends. For example a summer seasonal, or weekend & Evening specific members passes might help target and convert this demographic.
- Run membership sale during peak use months where casual use is at its highest, where the largest largest quantity of non members are interacting with your product. This would give you the best chance at converting non-members due to the high service utilization.
- Re-evaluate fee structure targeting casual use trends. For example, increasing cost on weekends, or implementing a pay-by-ride-length which could increase the perceived value of membership option, encouraging higher membership conversion.
- Launch Social media marketing campaign leading up to peak months peak months, and again after (April and September/October) leaning on the benefits active transportation methods provide to the users and the environment. Encouraging a subset of casual users to utilize the service to commute to work VIA Divvy bike share. As the commuter use patterns highly correlates to membership holders.

There is more data we could draw insights from. Trip location data could give us insights on common trip locations for members versus non-members, enabling more specificity when targeting each user subset by perks or marketing campain. For example allowing for a station popularity based fee structure. I would like to explore these potential avenues in the future!
