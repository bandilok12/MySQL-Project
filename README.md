# Smart Traffic & Accident Analytics (MySQL)

## Project Overview

Smart Traffic & Accident Analytics is a MySQL database project that stores and analyzes traffic observations, road accidents, weather conditions, vehicles, traffic violations, and fines.

The project uses SQL queries to identify locations with higher recorded accident counts, summarize traffic conditions, analyze violations, and compare traffic observations around recorded accidents.

**Database:** `SmartTrafficAnalytics`  
**Technology:** MySQL 8.0+  
**Tool:** MySQL Workbench  
**Core tables:** 7

## Project Aim

The main aim of Smart Traffic & Accident Analytics is to analyze traffic patterns and road accident records using MySQL, identify accident-prone locations, and investigate the relationship between traffic density, vehicle speed, weather conditions, and accidents. The system also analyzes traffic violations and fines to support better traffic monitoring and road-safety decisions.

## Objectives

- Identify locations with higher recorded accident counts.
- Analyze vehicle counts, average speed, and traffic density.
- Explore accident records under different weather conditions.
- Compare traffic observations within 30 minutes before or after an accident when data is available.
- Analyze traffic violations, fines, and payment statuses.
- Demonstrate SQL concepts such as joins, indexes, views, stored procedures, and triggers.

## Database Tables

| Table | Purpose |
|---|---|
| `Locations` | Stores location name, city, address, area type, and description. |
| `Roads` | Stores road name, road type, speed limit, length, and location reference. |
| `Weather` | Stores weather observations, date, time, temperature, visibility, and precipitation. |
| `Vehicles` | Stores vehicle number, type, manufacturer, model, and manufacture year. |
| `Traffic_Records` | Stores traffic observations, vehicle count, average speed, and traffic density. |
| `Accidents` | Stores accident date/time, location, road, severity, injuries, fatalities, and cause. |
| `Traffic_Violations` | Stores violation type, fine amount, violation date, and payment status. |

## Important Attributes

### 1. Locations
- `location_id` — Primary Key (PK)
- `location_name`
- `city`
- `address`
- `area_type`
- `description`

### 2. Roads
- `road_id` — PK
- `road_name`
- `road_type`
- `speed_limit`
- `length_km`
- `location_id` — Foreign Key (FK)

### 3. Weather
- `weather_id` — PK
- `observation_date`
- `observation_time`
- `weather_condition`
- `temperature`
- `visibility_km`
- `precipitation_mm`

### 4. Vehicles
- `vehicle_id` — PK
- `vehicle_number` — Unique
- `vehicle_type`
- `manufacturer`
- `model`
- `manufacture_year`

### 5. Traffic_Records
- `traffic_id` — PK
- `location_id` — FK
- `road_id` — FK
- `weather_id` — Nullable FK
- `observation_date`
- `observation_time`
- `vehicle_count`
- `avg_speed`
- `traffic_density`

### 6. Accidents
- `accident_id` — PK
- `location_id` — FK
- `road_id` — FK
- `vehicle_id` — Nullable FK
- `weather_id` — Nullable FK
- `accident_date`
- `accident_time`
- `severity`
- `injuries`
- `fatalities`
- `cause`
- `description`

### 7. Traffic_Violations
- `violation_id` — PK
- `vehicle_id` — FK
- `location_id` — FK
- `violation_type`
- `fine_amount`
- `violation_date`
- `payment_status`
- `description`

**Note:** Both `Weather` and `Traffic_Records` contain `observation_date` and `observation_time`. These describe when weather and traffic were observed, respectively. The relationship between these tables is established through `Traffic_Records.weather_id`, not by directly connecting the date/time attributes.

## Entity Relationships

- `Locations` → `Roads`: One-to-many (1:N)
- `Locations` → `Traffic_Records`: One-to-many (1:N)
- `Roads` → `Traffic_Records`: One-to-many (1:N)
- `Weather` → `Traffic_Records`: One weather record can be linked to many traffic records; a traffic record may have no weather reference.
- `Locations` → `Accidents`: One-to-many (1:N)
- `Roads` → `Accidents`: One-to-many (1:N)
- `Weather` → `Accidents`: One weather record can be linked to multiple accidents; the weather reference may be unknown.
- `Vehicles` → `Accidents`: One vehicle can be linked to multiple accidents; the vehicle reference may be unknown.
- `Locations` → `Traffic_Violations`: One-to-many (1:N)
- `Vehicles` → `Traffic_Violations`: One-to-many (1:N)

PK means Primary Key, FK means Foreign Key, and 1:N means one-to-many.

## Main SQL Analyses

- Count accidents by location.
- Group accident records by severity.
- Calculate traffic statistics by road.
- Explore accidents associated with different weather conditions.
- Compare traffic measurements within 30 minutes before or after an accident at the same location and date.
- Calculate total fines and summarize paid, pending, and overdue violations.

The traffic-around-accident query can compare vehicle count, average speed, and traffic density. It can reveal patterns in the available records but cannot prove that an accident caused congestion.

## SQL Concepts Used

- `CREATE DATABASE` and `CREATE TABLE`
- Primary keys, foreign keys, and constraints
- `SELECT`, `WHERE`, and `ORDER BY`
- `JOIN` and `LEFT JOIN`
- `GROUP BY` and `HAVING`
- `COUNT()`, `SUM()`, and `AVG()`
- Indexes
- Views
- Stored procedures
- Triggers and audit records

## How to Run the Project

1. Install MySQL Server 8.0 or later.
2. Open MySQL Workbench and connect to your server.
3. Open `project_mysql_queries.txt`.
4. Execute the script in order on a fresh database.
5. Check that the database and tables exist:

   ```sql
   USE SmartTrafficAnalytics;
   SHOW TABLES;
   ```

6. Execute the queries and inspect the views, stored procedures, and trigger demonstrations.

## Limitations

- The sample data is illustrative, not official traffic data.
- Results depend on the records available in the database.
- Missing weather or traffic observations can limit comparisons.
- The schema is simplified for a student project.
- SQL analysis identifies patterns but does not establish causation.
- The project analyzes stored records; it does not predict accidents.

## Future Enhancements

- Integrate verified traffic and accident datasets.
- Collect traffic observations over longer periods.
- Build a dashboard for traffic and accident summaries.
- Improve the road model to represent road segments and endpoints.
- Explore predictive models after collecting sufficient quality data.

## Conclusion

Smart Traffic & Accident Analytics demonstrates how MySQL can organize traffic, accident, weather, vehicle, and violation records and use SQL to investigate road-safety patterns. It combines relational database design with practical analytical queries while acknowledging the limitations of the available data.
