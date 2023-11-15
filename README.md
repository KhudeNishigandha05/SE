Abhishek Taprial 23112001 took set B from part 2
Nishigandha Khude 23112017 took set A from part 2
Rohit Ranaware 23112032 took set C from part 2

INTERCITY ASSIGNMENT
Key points of database

1 - Trains have coaches which we consider as in sequence and each coach has capacity of 30 seats
2 - As we need to keep the data of passengers so we created passenger table and as some tickets are also booked by travel agents so we created travel_agent table also and we take passenger_id and travel_agent_id from passenger table and travel_agent table into ticket table and travel_agent_id can be null if ticket is not booked by travel_agent
3 - ticket table contains information like passenger_id, travel_agent_id, seat_id, price etc.
4 - As many trains goes from many stations so we created many-to-many relation and took goes_to relationship as a table
5 - A train is scheduled to go from routes and as many trains are scheduled to go from many routes we created table of schedule relationship.
5 - We have taken 20 trains with 5 coach each as there 100 coaches.
6 -  Coach has coach_id, train_id, mileage and month so to track the data of coach of a particular train which has certain mileage in a particular month.
7 - A ticket is for particular seat of a coach from train. 
8 - We have taken seats_sold table for to calculate number of seats sold in particular schedule.
9 - All seats are currently avaliable and we update seats which are booked.


We have uploaded er diagram image as er_diagram.jpg

DATABASE CREATE AND INSERT STATEMENTS.

create database intercity;

use intercity;

-- staff table
create table staff(staff_id varchar(20) primary key,staff_name varchar(20),contact int,adress varchar(20));

-- passenger table 
create table passenger(pass_id varchar(20) primary key,pass_name varchar(20),pass_contact int,age int,type varchar(20));

--trains table
create table trains(train_id varchar(20) primary key,train_name varchar(20));

-- travel_agent table
create table travel_agent(agent_id varchar(20) primary key,agent_name varchar(20),contact int,confirmed_bookings int);

-- station table
create table station(station_id varchar(20) primary key,station_name varchar(20));

-- seat table
create table seat(coach_seat_id varchar(20) primary key,isAvailable varchar(1));

-- coach table
create table coach(coach_id varchar(20) primary key,train_id varchar(20),mileage int,mentenance_month int, foreign key(train_id) references trains(train_id));

-- contains table
create table contains(coach_id varchar(20) primary key, train_id varchar(1), foreign key(train_id) references trains(train_id), foreign key(coach_id) references coach(coach_id));

-- goes_to table
create table goes_to(schedule_id varchar(20),train_id varchar(20),mileage
int,route_id varchar(20),act_arrival_time time,act_reach_time time,is_late varchar(20), foreign key(train_id) references trains(train_id),foreign key(route_id) references route(route_id),foreign key(schedule_id) references schedule(schedule_id));

-- schedule table
create table schedule(schedule_id varchar(20) primary key,train_id varchar(20),route_id varchar(20),exp_arrival_time time,exp_reach_time time,scheduled_date date,driver varchar(20),co_driver varchar(20), foreign key(train_id) references trains(train_id),foreign key(route_id) references route(route_id), foreign key(driver) references staff(staff_id), foreign key(co_driver) references staff(staff_id));

-- maintenance
 create table maintenance(maintenance_id varchar(20) primary key, coach_id varchar(1), last_mentenance_date date,next_mentenance_date date, foreign key(coach_id) references coach(coach_id));

-- route table
create table route(route_id varchar(20) primary key,distance int,avg_travel_time time,operating_days varchar(20),starting_station varchar(20),last_station varchar(20),foreign key(starting_station) references station(station_id), foreign key(last_station) references station(station_id));

-- seat_sold table
create table seats_sold(schedule_id varchar(20), sold int,foreign key(schedule_id) references schedule(schedule_id));

-- ticket table
create table ticket(ticket_id varchar(20) primary key,price int,passenger_id varchar(20),seat_id varchar(20),discount int,travel_agent_id varchar(20),booking_date date,schedule_id varchar(20),commission int, foreign key(schedule_id) references schedule(schedule_id),foreign key(passenger_id) references passenger(pass_id), foreign key(travel_agent_id) references travel_agent(agent_id))





--insert queries
LOAD DATA local INFILE '<fillepath>/ticket.csv' INTO TABLE ticket FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/goes_to.csv' INTO TABLE goes_to. FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/passenger.csv' INTO TABLE passenger FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/travel_agent.csv' INTO TABLE travel_agent FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/route.csv' INTO TABLE route FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/seats-sold.csv' INTO TABLE seats_sold FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/maintenance.csv' INTO TABLE maintenance FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/schedule.csv' INTO TABLE schedule FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/station.csv' INTO TABLE station FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
LOAD DATA local INFILE '<fillepath>/trains.csv' INTO TABLE trains FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';

All the queries from part 2 are submitted through txt file

 

