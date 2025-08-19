# HOTEL ANALYSIS  USING(SQL ,SQLite,DBeaver and Power Bi)
This is a data analysis Project focusing mainly on international hotels insights to give a satisfying retationship  among the data that may help a hotel business on how to navigate  in this ecosystem . It mainly includes Three Tables which are Hotels, Users and Reviews.
## Tools  Used
The Language Used is *SQL* .Together with Darabase Management Tool of  DBeaver, SQLite Database  and Power Bi

## Project Objective
The main objective of this project was to analyze hotel review data to uncover trends in customer satisfaction, benchmark hotel performance across different states and cities, and provide insights together with  visualization  that can help the hotel user to  make informed choices and hotel managers improve their services.

 ## Project Flow 

| Step | Action                                                                                         |
| ---- | ---------------------------------------------------------------------------------------------- |
| 1    | Project Overview                                                                               |
| 2    | ER Diagram – visual of relationships.                                                          |
| 3    | Schema Design – table definitions and constraints.                                             |
| 4    | Sample Data & Queries – realistic scenarios.                                                   |
| 5    | Insights/Findings – e.g., “Hotel X was the highest rated in 2023 with an average of 4.9 stars.”|
| 6    | Challenges & Solutions – importing, cleaning, indexing, constraints.                           |


  ##  ER DIAGRAM
  This Shows the Relationships within the tables of the database which ar One To Many Relationships dominating the data.
  * One Hotel can have many Reviews
  * A user can leave multiple reviews
  * A hotel can have multiple and many users as they can.
  * Multiple hotels can also have multiple users and multiple reviews.

## SCHEMA DESIGN
The dataset is structured around three core tables that can be easily linked:

* hotels.csv: This table serves as the hotel catalog, containing unique hotels with key attributes like hotel_id, name, city, and star_rating. This provides the foundational context for all other data, allowing you to analyze hotel performance based on location and quality.

* users.csv: This file provides a list of unique customers, offering essential demographic insights with columns such as user_id, country, and age. This data is vital for segmenting customers and understanding how demographics influence review behavior.

* reviews.csv: As the central transactional table, it is the heart of the dataset. It links users to the hotels they reviewed, capturing crucial details like review_id, hotel_id, user_id, and a numerical review_score. This table is particularly valuable for its focus on quantitative feedback.

* Primary Keys(PK) Allocations.
Selected Primary keys from the tables are as per their uniqueness from the tables ,compared to other tables.
Hotel_ID for hotels table.
Users_ID for Users table.
Reviews_ID for Reviews Table.

##   Sample Data & Queries

* Rank based on their Review rank
-SELECT h.hotel_id, h.hotel_name, AVG(h.star_rating ) AS Avg_rating
FROM Hotels h
JOIN Reviews r ON h.hotel_id = r.hotel_id
GROUP BY h.hotel_id, h.hotel_name
ORDER BY Avg_rating DESC
LIMIT 5;

* Hotel ranks based on their general score out of 10
-SELECT h.hotel_id, h.hotel_name, AVG(r.score_overall) AS HotelScore
FROM Hotels h
JOIN Reviews r ON h.hotel_id = r.hotel_id
GROUP BY h.hotel_id, h.hotel_name
ORDER BY HotelScore DESC
LIMIT 5;

* How may users as per Gender ,Gave more reviews in a particular month.
  -SELECT u.user_id, u.user_gender , strftime('%Y-%m', r.review_date) AS review_month,
       COUNT(r.review_id) AS review_count
FROM Users u
JOIN Reviews r ON u.user_id = r.user_id
GROUP BY u.user_id, review_month 
HAVING COUNT(r.review_id) > 3;

* Hotelswith no reviews
-SELECT h.hotel_id, h.hotel_name, h.city
FROM Hotels h
LEFT JOIN Reviews r ON h.hotel_id = r.hotel_id
WHERE r.review_id IS NULL;

* Average Rating based on City
-SELECT h.city, AVG(r.score_overall ) AS avg_rating
FROM Hotels h
JOIN Reviews r ON h.hotel_id = r.hotel_id
GROUP BY h.city
ORDER BY avg_rating DESC;

* Countries with most review
SELECT u.country ,COUNT(r.review_id ) AS Count
FROM users u 
JOIN reviews r ON u.user_id = r.user_id 
GROUP BY u.country
ORDER BY Count  DESC;

## INSIGHTS & FINDINGS.
- Most of the overall hotel scores are of high ,which is good for most of the hotels.From 8.5 ,the limit being 10.
- The star ratings of most hotels are 5 ,no less than 4.55
- United States is the country with the most reviews.
- There are 25 hotels in the database

###  CHALLENGES AND SOLUTIONS
* When Assigning primary  keys ,since the database data  has not been assigned primary keys,so we assign Virtual primary keys so as to be able to create ERD Diagrams for Analysis and Visualization.
* The star ratings out of 5 are high and the overall hotel scores are high ,whivh makes it hard in grouping the lower rated data ,since they are few and nee to be closest to decimal value.
* Linking the database with it's server to the power Bi for visualization.
* Due to many data being close up becomes a problem ,when visualizing a graph you have to adjust the scale to reduce some values.

