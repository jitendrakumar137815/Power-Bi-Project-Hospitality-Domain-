# Power-Bi-Project-Hospitality-Domain-
# Problem Statement:-
<br>
AtliQ Grands owns multiple five-star hotels across India. They have been in the hospitality industry for the past 20 years. Due to strategic moves from other competitors and ineffective decision-making in management, AtliQ Grands is losing its market share and revenue in the luxury/business hotels category. As a strategic move, the managing director of AtliQ Grands wanted to incorporate “Business and Data Intelligence” to regain their market share and revenue. However, they do not have an in-house data analytics team to provide them with these insights.
<br>
Their revenue management team had decided to hire a 3rd party service provider to provide them with insights from their historical data.

# Steps Followed
# Data Loadind :-
Load the data into power BI from MS Excel.
# Data Transformation :-
Data Transformation Using Power Query .
<img width="1234" height="638" alt="image" src="https://github.com/user-attachments/assets/6ab39f2f-4d4d-4374-8f12-1c42c13e7b41" />


# Data Analysis Expression :
using DAX created new columns <br>
In the dim_date data table,Created two new columns "wn" and "day type" using the following formulas-<br>
Wn =
<br>
WEEKNUM(dim_date[date]) <br>
day type = 
 
 Var wkd = WEEKDAY(dim_date[date],1)

 return
 IF(
 wkd>5, "Weekend", "Weekday")
# Building Metrics Using DAX : <br>
1. Revenue = SUM(fact_bookings[revenue_realized])
2. Total Booking = Count(fact_bookings[booking_id])
3. Total Capacity = SUM(fact_aggregated_bookings[capacity])
4. Total Succesful Bookings = SUM(fact_bookings[succcesful_bookings])
5. Occupancy % = DIVIDE([Total Succesful Bookings],[Total Capacity],0)
6. Average Rating = AVERAGE(fact_bookings[rating_given])
7. No. of days = DATEDIFF(MIN(dim_date[date]),MAX(dim_date[date]),DAY) +1
8. Total cancelled bookings =CALCULATE([TotalBookings],fact_bookings[booking_status]="Cancelled") 
9. Cancellation % = DIVIDE([Total cancelled bookings],[Total Bookings])
10. Total Checked Out = CALCULATE([Total Bookings],fact_bookings[booking_status]="Checked Out")
11. Total no show bookings = CALCULATE([Total Bookings],fact_bookings[booking_status]="No Show")
12. No Show rate % = DIVIDE([Total no show bookings],[Total Bookings])
13. Booking % by Platform = DIVIDE([Total Bookings],
 CALCULATE([Total Bookings], 
 ALL(fact_bookings[booking_platform])
  ))*100
14. Booking % by Room class = DIVIDE([Total Bookings],
 CALCULATE([Total Bookings], 
 ALL(dim_rooms[room_class])
  ))*100
15. Realisation % = 1- ([Cancellation %]+[No Show rate %])
16. ADR = DIVIDE( [Revenue], [Total Bookings],0)
17. RevPAR = DIVIDE([Revenue],[Total Capacity])
18. DBRN = DIVIDE([Total Bookings], [No of days])
19. DSRN = DIVIDE([Total Capacity], [No of days])
20. DURN = DIVIDE([Total Checked Out],[No of days])
21. Revenue WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Revenue],dim_date[wn]= selv)
var revpw =  CALCULATE([Revenue],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
22. Occupancy WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Occupancy %],dim_date[wn]= selv)
var revpw =  CALCULATE([Occupancy %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
23. ADR WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([ADR],dim_date[wn]= selv)
var revpw =  CALCULATE([ADR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
24. Revpar WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([RevPAR],dim_date[wn]= selv)
var revpw =  CALCULATE([RevPAR],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
25. Realisation WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([Realisation %],dim_date[wn]= selv)
var revpw =  CALCULATE([Realisation %],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1
26. DSRN WoW change % = 
Var selv = IF(HASONEFILTER(dim_date[wn]),SELECTEDVALUE(dim_date[wn]),MAX(dim_date[wn]))
var revcw = CALCULATE([DSRN],dim_date[wn]= selv)
var revpw =  CALCULATE([DSRN],FILTER(ALL(dim_date),dim_date[wn]= selv-1))

return


DIVIDE(revcw,revpw,0)-1 <br>
Here <br>
RevPAR - Revenue per available room <br>
DSRN -Daily sellable room nights
<br>
ADR - Average Daily Rate <br>
DBRN - Daily Booked Room Nights <br>
DURN- Daily Utilized Room Nights
# Data Modelling : 
![capture_250702_231555](https://github.com/user-attachments/assets/e40817b6-ea7f-4374-9ec5-921cb92af86a)
# DashBoard Snapshot :-

<img width="1101" height="658" alt="capture_250708_220317" src="https://github.com/user-attachments/assets/35bafe29-ee3c-4791-af05-7b508f1c72c7" />
<img width="1306" height="587" alt="capture_250708_220354" src="https://github.com/user-attachments/assets/0b0a0273-586d-4807-95d6-85ec1b63a657" />
<img width="1360" height="633" alt="capture_250708_220417" src="https://github.com/user-attachments/assets/d0b25df6-c4d3-47d1-869c-5ab589243961" />
