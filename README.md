# Vehicle Booking System SQL Queries

## Project Overview
This project is a **Vehicle Booking System** database implemented using SQL. The system allows managing **users, vehicles, and bookings**, and includes queries to retrieve, analyze, and manage booking data.

The database contains the following tables:

- **Users**: Stores user details including role, name, email, password, and phone.
- **Vehicles**: Stores vehicle details including type, model, registration number, price per day, and availability status.
- **Bookings**: Stores booking information including start and end dates, booking status, total cost, and foreign keys linking to users and vehicles.

---

## SQL Queries

### **Query 1: JOIN**

**Purpose**: Retrieve booking information along with customer name and vehicle name.  

```sql
SELECT 
    b.booking_id,
    u.name AS customer_name,
    v.vehicle_name,
    b.start_date,
    b.end_date,
    b.booking_status,
    b.total_cost
FROM 
    Bookings b
INNER JOIN 
    Users u ON b.user_id = u.user_id
INNER JOIN 
    Vehicles v ON b.vehicle_id = v.vehicle_id;



### **Query 2: NOT EXISTS**


SELECT 
    v.vehicle_id,
    v.vehicle_name,
    v.vehicle_type
FROM 
    Vehicles v
WHERE NOT EXISTS (
    SELECT 1
    FROM Bookings b
    WHERE b.vehicle_id = v.vehicle_id
);

### **Query 3: WHERE**


SELECT 
    vehicle_id,
    vehicle_name,
    model,
    registration_number,
    price_per_day
FROM 
    Vehicles
WHERE 
    vehicle_type = 'Car' 
    AND availability_status = 'Available';

### **Query 4: GROUP BY & HAVING**


SELECT 
    v.vehicle_name,
    COUNT(b.booking_id) AS total_bookings
FROM 
    Vehicles v
INNER JOIN 
    Bookings b ON v.vehicle_id = b.vehicle_id
GROUP BY 
    v.vehicle_name
HAVING 
    COUNT(b.booking_id) > 2;



