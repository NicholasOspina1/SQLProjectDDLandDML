# SQL Project: DDL & DML (ISM4210)


-------

# Description <a name="description">

For this deliverable, you will be creating the database for EventsByEventz in MySQL. This database will be based on the relational model below. Do not include any columns or constraints that are not in this relational model.

<p align="center">
EventsByEventz: <br/>
<img src="https://i.imgur.com/FOKHeFL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

STEP 1:
Create a new database in MySQL called EBE_LastNameFirstName using your Last name and first name e.g., EBE_GatorAlbert.
You can create the tables described in Step 2 in this database.

STEP 2:
Create the tables as follows:

- Write the CREATE statements for the table corresponding to each of the relations. You must decide which data types (and field size, when applicable) will be appropriate for each column in each table.  Each table must have a Primary Key and the appropriate Foreign keys (if applicable).
- Write at least two ALTER statements to either add columns or Primary Key or Foreign Key constraints to any of the tables. Do include any columns or constraints that are not in the relational model shown above. HINT: When writing the CREATE statements, leave out the columns or constraints that you will add with the ALTER statements.
- Execute all the CREATE and ALTER statements in MySQL.

STEP 3:
Insert data into your tables as follows:

- Write one INSERT statement for each of the tables (you may use any dummy data that you can make up).
- Execute the INSERT statements in MySQL.  HINT: The order in which you insert data into your tables is important – so pay attention to the Foreign Keys and the referential integrity constraints.

STEP 4:
Create ONE text file with the following SQL statements. .

- CREATE DATABASE EBE_LastNameFirstName;
- USE DATABASE EBE_LastNameFirstName;
- The CREATE, INSERT and ALTER statements you created in Step 2 and Step 3.

# My Answer  <a name="scenario">

```ruby
CREATE DATABASE EBE_OspinaNicholas;
USE EBE_OspinaNicholas;
CREATE TABLE Venue(
VenueID INTEGER,
VenueName VARCHAR(30),
Capacity INTEGER,
Street VARCHAR(50),
City VARCHAR(30),
State VARCHAR(2),
Zip VARCHAR(5),
Parking BOOLEAN,
LocationContactName VARCHAR(20),
CONSTRAINT PK_Venue
PRIMARY KEY (VenueID));

ALTER TABLE Venue
ADD COLUMN LocationContactPhone INTEGER;

CREATE TABLE Clients(
ClientID INTEGER,
ClientName VARCHAR(30),
Street VARCHAR(50),
City VARCHAR(30),
State VARCHAR(2),
Zip VARCHAR(5),
PRIMARY KEY (ClientID));

CREATE TABLE Event(
EventCode INTEGER PRIMARY KEY,
EventName VARCHAR (30),
Description VARCHAR (100),
EventDate DATE,
StartTime TIME,
EndTime TIME,
Ticket BOOLEAN,
VenueID INTEGER,
ClientID INTEGER,
CONSTRAINT FK_Event_Venue FOREIGN KEY (VenueID)
      REFERENCES Venue (VenueID),
CONSTRAINT FK_Event_Clients FOREIGN KEY (ClientID)
      REFERENCES Clients (ClientID));

CREATE TABLE Contact(
ClientID INTEGER,
ContactName VARCHAR(20),
ContactPhone INTEGER,

CONSTRAINT PK_Contact
PRIMARY KEY (ContactName),
CONSTRAINT FK_Contact_Clients FOREIGN KEY (ClientID)
      REFERENCES Clients (ClientID));

ALTER TABLE Contact
ADD COLUMN ContactEmail VARCHAR(320);

CREATE TABLE Event_Contact(
ClientID INTEGER,
ContactName VARCHAR(20),
EventCode INTEGER);

ALTER TABLE Event_Contact
ADD CONSTRAINT FK_Event_Contact_Client
FOREIGN KEY (ClientID) REFERENCES Clients(ClientID);

ALTER TABLE Event_Contact
ADD CONSTRAINT FK_Event_Contact_Person
FOREIGN KEY (ContactName) REFERENCES Contact(ContactName);

ALTER TABLE Event_Contact
ADD CONSTRAINT FK_Event_Contact
FOREIGN KEY (EventCode) REFERENCES Event(EventCode);

CREATE TABLE Ticketed_Event(
EventCode INTEGER,
TicketPrice INTEGER,
TicketsAvailable INTEGER,
TicketsSold INTEGER,
WristBands BOOLEAN,
HandStamp BOOLEAN,
CONSTRAINT FK_Ticketed_Event FOREIGN KEY (EventCode)
      REFERENCES Event (EventCode));

CREATE TABLE Nonticketed_Event(
EventCode INTEGER,
GuestList BOOLEAN,
ExpectedAttendance INTEGER,
ActualAttendance INTEGER,
CONSTRAINT FK_Nonticketed_Event FOREIGN KEY (EventCode)
      REFERENCES Event (EventCode));

INSERT INTO Venue (VenueID)
      VALUE ('1016');

INSERT INTO Clients (ClientID)
      VALUE ('1234');

INSERT INTO Event (EventCode)
      VALUE ('0987');

INSERT INTO Contact (ContactName)
      VALUE ('Bob');

INSERT INTO Ticketed_Event (TicketPrice)
      VALUE ('20');

INSERT INTO Nonticketed_Event (ExpectedAttendance)
      VALUE ('100');


```
