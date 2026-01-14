🔢 Core Performance Measures
-- Total Restaurants
Total Restaurants =
DISTINCTCOUNT(zomato[RestaurantID])

-- Total Votes
Total Votes =
SUM(zomato[Votes])

-- Average Rating
Average Rating =
AVERAGE(zomato[Rating])

-- Votes per Restaurant
Votes per Restaurant =
DIVIDE(
    [Total Votes],
    [Total Restaurants]
)

🌍 Country-Level Analysis Measures
-- Country Average Rating
Country Avg Rating =
CALCULATE(
    [Average Rating],
    ALL(zomato)
)

-- Country Rank by Rating
Country Rank =
RANKX(
    ALL(country[Country Name]),
    [Average Rating],
    ,
    DESC
)

📦 Delivery & Digital Adoption Measures

-- Online Delivery Restaurants
Online Delivery Restaurants =
CALCULATE(
    DISTINCTCOUNT(zomato[RestaurantID]),
    zomato[Has_Online_delivery] = "yes"
)

-- Offline Delivery Restaurants
Offline Delivery Restaurants =
CALCULATE(
    DISTINCTCOUNT(zomato[RestaurantID]),
    zomato[Has_Online_delivery] = "no"
)

-- Online Delivery %
Online Delivery % =
DIVIDE(
    [Online Delivery Restaurants],
    [Total Restaurants]
)

-- Offline Delivery %
Offline Delivery % =
DIVIDE(
    [Offline Delivery Restaurants],
    [Total Restaurants]
)

-- Total Delivery Ratio
Total Delivery Ratio =
DIVIDE(
    [Offline Delivery Restaurants],
    [Online Delivery Restaurants]
)

⭐ Popularity & Engagement Measures

-- Popular Restaurants
Popular Restaurants =
CALCULATE(
    DISTINCTCOUNT(zomato[RestaurantName]),
    zomato[Votes] >= 1000
)

-- Not Popular Restaurants
Not Popular Restaurants =
CALCULATE(
    DISTINCTCOUNT(zomato[RestaurantName]),
    zomato[Votes] < 1000
)

💰 Pricing & Premium Analysis Measures
-- Premium Restaurants
Premium Restaurants =
CALCULATE(
    DISTINCTCOUNT(zomato[RestaurantID]),
    zomato[Average_Cost_for_two] >= 1500
)

-- Not Premium Restaurants
Not Premium Restaurants =
CALCULATE(
    DISTINCTCOUNT(zomato[RestaurantID]),
    zomato[Average_Cost_for_two] < 1500
)

-- Price Range Share %
Price Range Share % =
DIVIDE(
    COUNT(zomato[RestaurantID]),
    CALCULATE(
        COUNT(zomato[RestaurantID]),
        ALL(zomato[Price_range])
    )
)

⚠️ Risk Identification Measures 
-- High Risk Restaurants
High Risk Restaurants =
CALCULATE(
    COUNT(zomato[RestaurantID]),
    FILTER(
        zomato,
        zomato[Rating] < 3 &&
        zomato[Votes] < 50
    )
)

-- Luxury Risk Restaurants
Luxury Risk Restaurants =
CALCULATE(
    COUNT(zomato[RestaurantID]),
    zomato[Price_Range] = "Luxury",
    zomato[Rating] < 3.5
)

🧩 Data Quality Measures
-- Duplicate Restaurant Name Count
Duplicate Restaurant Name Count =
CALCULATE(
    COUNT(zomato[RestaurantID]),
    ALLEXCEPT(
        zomato,
        zomato[RestaurantName]
    )
)

