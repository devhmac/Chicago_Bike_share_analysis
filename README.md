# Divvy Bikeshare Ridership Analysis

This project utilized various technologies to clean, manipulate, transform, analyze and finally visualize a bike share ridership dataset. 

Python - Cleaning, transforming, enhancing and analyzing our dataset. 

SQL - Validation, and exploratory, impromptu analysis.

Tableau for Visualization and Dashboard creation. 

<div align="center"> 
## Tableau Dashboard linked here 
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

<img src="https://s3-us-west-2.amazonaws.com/secure.notion-static.com/956400c3-f74a-42fd-94f6-b36b4cbef064/Untitled.png">

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/956400c3-f74a-42fd-94f6-b36b4cbef064/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/acf6d6aa-e48f-4f1b-b0e3-a58a490a4afb/Untitled.png)

After importing our data we explored each set to confirm column names and data types were compatible. Once confirmed, we merged all 12 sets.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/073aee04-129b-461a-8c1e-4c3c7610a7d6/Untitled.png)

## Cleaning

- Started with confirming the data types of our columns.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/639be36c-95e9-478c-9b91-6bc1f7db1399/Untitled.png)

- First, we checked for and dropped duplicate rows (there were none). We then noted that start and end times were objects. We translated them to datetime to perform calculations on them for additional data points.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2f179987-f0ac-4fbc-9507-56f75645eb4c/Untitled.png)

Next we added 3 new columns to our dataset, which will provide additional value during the analysis process. 

- Changed the name of the “member_casual” column to “rider_type”.
- Added “Weekday” column, tracking the day of the week each trip took place.
- Added “Month” column, tracking the month of each ride.
- Calculated the trip duration of each ride using the start and end date column of each row. We decided to store this in minutes, rounded to 2nd decimal point.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/298d16c3-2ef2-40e5-9e46-551727be7cb9/Untitled.png)

The Jupyter notebook Deepnote allows for the use of SQL on dataframes, which allows for an incredibly efficient combo of the two languages. We leveraged this to perform a few quick data validation queries to check if our set had any incomplete or corrupted trip data. 

See a few of these queries below;

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/947f08f6-349a-477e-87bb-42ab68490b14/Untitled.png)

Luckily all rows appeared to have complete trip data. Many rows were missing station names and ID’s, but even in those cases Lat and Long of both start and end locations were still recorded. 

Next, we checked the trip duration, to confirm our trip lengths made sense contextually. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1da1da88-5c35-4dfe-9ea7-c979d8ed7013/Untitled.png)

We found 110578 trips with a duration below 1 minute, which seemed potentially problematic. After some research on Divvy’s data capture techniques, we found they recommend that trips under 1 minute be considered false starts of errors, so we dropped these from our set. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bd54d7eb-81c8-470c-b772-44dd53873634/Untitled.png)

Now confident in our data, I split our set in two, one with location data removed for a customer-focused analysis, and the other for a future project to analyze location-based ridership trends and geo-mapping. 

## Analysis and visualization

Focusing our analysis on the difference between membership and casual rider use trends uncovered to some interesting findings. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e33a1674-32fd-4b5c-ac38-52b101a4b6d2/Untitled.png)

- Of the total 5 million trips, 57.79% were taken by members (2,917,645).
- More interesting, however, despite accounting for the majority of all rides, member ride only account for 42.34% of the total time spent riding bikes. 626,269.6 of 1,479,144 hours annually. Let's dig into this trend further.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1b971137-5c41-40e5-bf6c-40157cea41a5/Untitled.png)

- After further analysis, on average the length of casual rider trips are almost double that of member rides.

This is interesting in addition to the result above. It adds further context\ further context to why members are the more profitable user group. Despite using the product more frequently than casual riders they are on the bikes less per trip, enabling the bikes to be more readily available for the next user.  

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/59c15d1c-8f5e-494a-89ee-d9e82d984227/Untitled.png)

A quick analysis of the types of bikes ridden over the ast year showed the docked bikes were the least popular, actually accounting for no rides in the member segment. Despite being relatively close, members seem to lean towards the classic bikes, where as casual riders prefer electric. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e89e7b5f-4153-4ee3-842c-24a83e3e1b03/Untitled.png)

During weekdays (Mon - Fri) casual riders take significantly more trips than casual users. 

- Peaking on Tuesday at almost double (458,070 member vs  239,663 casual)

This pattern is biased towards the start of the week, as it goes on the gap between the two rider groups slightly narrows. By the weekend, casual rider trips actually exceed those of the member segment. 

A trend is emerging in the visualizations above. With casual riders taking longer trips on average, and exceeding member trips on weekends, I predict these rides represent leisure activities - compared to the member segment taking expedient trips on weekdays, which seems to represent commuting behaviour.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ecf5cbb6-554e-4303-a1b1-4777b4844c1e/Untitled.png)

When comparing trips to time of day, our above thesis is reinforced. 

- Member rides peak at prime commuting times, 6am-9am and 5pm. In evening the gap between the rider groups reduces.
- On weekends, after 11am casual rides exceed member rides for almost the rest of the day.

User interviews should be conducted to confirm the different use patters, but the above plot clearly demonstrates the difference between the casual rides and the more commute focused member rides. 

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8d8371ed-31e6-4836-b10d-f463d8a6b406/Untitled.png)

Unsurprisingly, we see total rides are much higher in the warmer months. In the off months, Oct - April, we see the biggest gaps between segments. The largest differences being Oct-Dec. 

- Apr. - Jul. we see a steady growth in both groups rides, until August, where member rides continue to climb, but casual rides drop. This would be a great spot to market towards casual users and attempt to increase their ridership.

Additional data should be collected on the reason for Casual rider reduction during this summer month. 

- In July, casual and member rides are almost neck and neck, this would be an excellent opportunity to try to convert some of the high casual users to members.
- Member riders are much higher users in the colder months, approximating that the segment is using the service less for pleasure/leisure acitivies, and more as an effective form of transportation, particularly in these months where outdoor activities are less desirable.

### Overall Trends

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
