# 🧮 Business Classification Columns
### Country Group
Country Group =
IF(
    zomato[CountryCode] = 1,
    "India Market",
    "International Market"
)

### Cleaned Cuisines
Cuisines Cleaned =
TRIM(zomato[Cuisines])

### Currency Type
Currency Type =
IF(
    zomato[Currency] = "Indian Rupees(Rs.)",
    "Domestic Currency",
    "International Currency"
)

### Customer Experience
Customer Experience =
SWITCH(
    TRUE(),
    zomato[Rating] >= 4.5, "Exceptional",
    zomato[Rating] >= 4, "Very Good",
    zomato[Rating] >= 3, "Average",
    "Poor"
)

### Popularity Category
Popularity Category =
IF(
    zomato[Votes] >= 100,
    "Popular",
    "Not Popular"
)

### Price Segment
Price Segment =
IF(
    zomato[Average_Cost_for_two] <= 500, "Budget",
    IF(
        zomato[Average_Cost_for_two] <= 1500,
        "Mid Range",
        "Premium"
    )
)

### Rating Category
Rating Category =
IF(
    zomato[Rating] >= 4,
    "High Rating",
    "Low Rating"
)

### Restaurant Performance
Restaurant Performance =
SWITCH(
    TRUE(),
    zomato[Rating] >= 4.5, "Excellent",
    zomato[Rating] >= 3.5, "Good",
    "Needs Improvement"
)

