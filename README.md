# IT5015D_Assesment_2_20220987
## Assessment 2: Application of Information Systems to Business Brief
&nbsp;
## Task 1: Develop the Data Model – Logical Design 
&nbsp;
A -

![New Horizon Cnema ERD](/assets/NewHorizonCinemaERD.jpg "New Horizon Cnema ERD")
&nbsp;

B - List and describe all the entities that will be used to create the ERD. 
- **Cinema Complex:** a table to store information about each cinema complex New Horizon owns.
- **Theatre:** a table with information for all theatres on all different Cinemas. 
- **Movie:** information about the movies that are being screened.
- **Schedule:** A time table for each movie and theatre.

H - For each relationship, define which referential constraints apply. List the relationships and their constraints.

- A CinemaComplex ***can have*** many Theatres. 
- A group of Theatres ***belong*** to one CinemaComplex
- A Theatre ***screens*** many movies
- A movie ***can be screened*** on many theatres. 
- Each movie ***is part of*** a Schedule
- Each Theatre ***has*** a Schedule
- Each CinemaComplex ***has*** a Schedule

I - Normalisation Criteria

1 NF

- Attributes for each Entity are defined. There are no blanks or missing data in the tables.
- Every row and colum have only one data value instead of a set of values
- All attributes are dependat of the Key Attribute

2 NF

- There are no partial dependencies, all non-key field are dependant of a key field, also knonw as Primary Keys.

3 NF

- There are no transitive dependencies as the Primary Key has been carefully chosen.

&nbsp;


## Task 2: Design Data Queries 
&nbsp;


|           Function            |   Queries    |
|            :---               |    :----    |
| Search for CinemaComplex      |   searchCinemaByCity <br> searchCinemaByName  <br> searchTheatreByCapacity  <br> searchCinemaBySuburb  |
| Show Cinema Information       |   showCinemaPhoneNumber <br> showCinemaCity <br> showCinemaEmail |
| Search for Movie              |   searchMovieByTitle <br> searchMovieByReleaseYear <br> searchMovieByTheater |
| Show Movie Information        |   showMovieTitle <br> showMovieDuration <br> showMovieSchedule |
| Show Schedule                 |   showScheduleByTheatre <br> showScheduleByMovieTitle |
 

&nbsp;

- Note any question you have and any point you need to clarify with the customer/tutor.  
    - Table Names, table relationships, extra tables that might not be necessary. Foreign Keysfor some tables. 
- Review your database design and adjust it to make sure that it will enable these queries.  
- It is normal to make changes after looking at more detailed requirements.  
- Explain one of the changes you had to make.  
    - I had two tables that were making my ERD messy, I have now removed them and therefore simplified it.
    - I have also added Foreing Keys on tables that were missing them.
    - Relationship were corrected from one to one, to one to many when necessary.

&nbsp;

## Task 3: Prepare Data Content 
&nbsp;

![Database-1](/assets/NewHorizonDB-1.png )
![Database-2](/assets/NewHorizonDB-2.png )

&nbsp;

## Part 2: Database Implementation
&nbsp;


A - Enter the test data from Part 1: Task 3 to the tables (at least 5 records in each table).

```SQL
CREATE TABLE CinemaComplex (
    CinemaID int NOT NULL PRIMARY KEY,
    CinemaName varchar(255) NOT NULL,
    PhoneNumber varchar(255),
    Email varchar(255),
    StreetName varchar(255),
    StreetNumber varchar(255),
    Suburb varchar(255),
    City varchar(255)
);

INSERT INTO CinemaComplex (CinemaID, CinemaName, PhoneNumber, Email, StreetName, StreetNumber, Suburb, City)
VALUES (1,'New Horizon Newmarket', '93829517', 'newmarket@newhorizon.co.nz', 'Broadway', '169', 'Newmarket','Auckland');
INSERT INTO CinemaComplex (CinemaID, CinemaName, PhoneNumber, Email, StreetName, StreetNumber, Suburb, City)
VALUES (2,'New Horizon Queen', '92785612', 'queenst@newhorizon.co.nz', 'Queen Street', '297', 'Auckland CBD','Auckland');
INSERT INTO CinemaComplex (CinemaID, CinemaName, PhoneNumber, Email, StreetName, StreetNumber, Suburb, City)
VALUES (3,'New Horizon Albany', '92905345', 'albany@newhorizon.co.nz', 'Don Mickonon Drive', '219', 'Albany','Auckland');
INSERT INTO CinemaComplex (CinemaID, CinemaName, PhoneNumber, Email, StreetName, StreetNumber, Suburb, City)
VALUES (4,'New Horizon Miramar', '43855555', 'miramar@newhorizon.co.nz', 'Park Road', '5', 'Miramar','Wellington');
INSERT INTO CinemaComplex (CinemaID, CinemaName, PhoneNumber, Email, StreetName, StreetNumber, Suburb, City)
VALUES (5,'New Horizon Te Aro', '43986202', 'tearo@newhorizon.co.nz', 'Courtney Place', '100', 'Te Aro','Wellington');

CREATE TABLE Theatre (
    TheatreID int NOT NULL PRIMARY KEY,
    TheatreName varchar(255),
    SeatingCapacity int,
    SoundSystem varchar(255),
    CinemaID int,
    CONSTRAINT FK_CinemaID FOREIGN KEY (CinemaID)
    REFERENCES CinemaComplex(CinemaID)
);
INSERT INTO Theatre (TheatreID, TheatreName, SeatingCapacity, SoundSystem, CinemaID)
VALUES (1,'Newmarket Gold Class', 40, 'Dolby Atom', 1);
INSERT INTO Theatre (TheatreID, TheatreName, SeatingCapacity, SoundSystem, CinemaID)
VALUES (2,'Westcity IMAX', 300, 'Dolby Digital', 4);
INSERT INTO Theatre (TheatreID, TheatreName, SeatingCapacity, SoundSystem, CinemaID)
VALUES (3,'Queen Deluxe', 80, 'Dolby Atom', 2);
INSERT INTO Theatre (TheatreID, TheatreName, SeatingCapacity, SoundSystem, CinemaID)
VALUES (4,'Queen The Grande', 200, 'Dolby Atom', 2);
INSERT INTO Theatre (TheatreID, TheatreName, SeatingCapacity, SoundSystem, CinemaID)
VALUES (5,'Te Aro Boutique', 40, 'Dolby Atom', 5);

CREATE TABLE Movie (
    MovieID int NOT NULL PRIMARY KEY,
    MovieTitle varchar(255),
    Director varchar(255),
    ReleaseYear int,
    Duration int,
    LinkToIMDb varchar(255),
    Price int
);
INSERT INTO Movie (MovieID, MovieTitle, Director, ReleaseYear, Duration, LinkToIMDb, Price)
VALUES (1,'Avatar: The Way of Water', 'James Cameron', 2022, 192, 'https://www.imdb.com/title/tt1630029/?ref_=fn_al_tt_1', 25);
INSERT INTO Movie (MovieID, MovieTitle, Director, ReleaseYear, Duration, LinkToIMDb, Price)
VALUES (2,'Puss In Boots: The Last Wish', 'Joel Crowford', 2022, 102, 'https://www.imdb.com/title/tt3915174/?ref_=fn_al_tt_1', 25);
INSERT INTO Movie (MovieID, MovieTitle, Director, ReleaseYear, Duration, LinkToIMDb, Price)
VALUES (3,'Operation Fortune: Ruse De Guerre', 'Guy Ritchie', 2023, 114, 'https://www.imdb.com/title/tt7985704/?ref_=fn_al_tt_1', 25);
INSERT INTO Movie (MovieID, MovieTitle, Director, ReleaseYear, Duration, LinkToIMDb, Price)
VALUES (4,'M3GAN', 'Gerard Jonhstone', 2023, 102, 'https://www.imdb.com/title/tt8760708/?ref_=fn_al_tt_1', 25);
INSERT INTO Movie (MovieID, MovieTitle, Director, ReleaseYear, Duration, LinkToIMDb, Price)
VALUES (5,'The Amazing Maurice', 'Toby Genkel', 2023, 93, 'https://www.imdb.com/title/tt10473036/?ref_=fn_al_tt_1', 15);

CREATE TABLE Schedule (
    ScheduleID int NOT NULL PRIMARY KEY,
    Day date,
    MovieTime time,
    MovieID int,
    TheatreID int,
    CinemaID int,
    CONSTRAINT FK_MovieID FOREIGN KEY (MovieID) REFERENCES Movie(MovieID),
    CONSTRAINT FK_TheatreID FOREIGN KEY (TheatreID) REFERENCES Theatre(TheatreID),
    CONSTRAINT FK_ScheduleCinemaID FOREIGN KEY (CinemaID) REFERENCES CinemaComplex(CinemaID)   
);
INSERT INTO Schedule (ScheduleID, Day, MovieTime, MovieID, TheatreID, CinemaID)
VALUES (1, '2023-01-19', '10:30', 5, 2, 1);
INSERT INTO Schedule (ScheduleID, Day, MovieTime, MovieID, TheatreID, CinemaID)
VALUES (2, '2023-01-19', '13:00', 1, 3, 4);
INSERT INTO Schedule (ScheduleID, Day, MovieTime, MovieID, TheatreID, CinemaID)
VALUES (3, '2023-01-19', '15:30', 2, 5, 5);
INSERT INTO Schedule (ScheduleID, Day, MovieTime, MovieID, TheatreID, CinemaID)
VALUES (4, '2023-01-19', '20:30', 4, 2, 3);
INSERT INTO Schedule (ScheduleID, Day, MovieTime, MovieID, TheatreID, CinemaID)
VALUES (5, '2023-01-19', '18:30', 3, 4, 2);
```

B- Create and run ten queries you have identified previously in Part 1: Task 2 (these include the sample queries provided), at least two per function. <br>
C - For each query you are implementing, you are must: <br>
D - Describe in words what the query is expected to do <br>
E - What variable inputs it takes. <br>


```sql
SELECT MovieTitle, Price FROM Movie Where MovieID=2;
-- D: show movie title and price for movieID 2, from table Movie
-- E: MovieId = 2
```

```sql
SELECT CinemaName FROM CinemaComplex WHERE city='Auckland';
-- D: show name of cinema for every cinema complex in Auckland
-- E: Auckland (city)
```
```sql
SELECT TheatreName FROM Theatre WHERE SeatingCapacity=40;
-- D: name of theatre for all theatres with a seating capacity equal to 40
-- E: seating capacity = 40
```
```sql
SELECT PhoneNumber FROM CinemaComplex WHERE city="Wellington";
-- D: show phone numbers for each cinema complex
-- E: Wellington (city)
```
```sql
SELECT Suburb FROM CinemaComplex WHERE city="Auckland";
-- D: show suburb information for all the cinemas in Auckland
-- E: Auckland (city)
```
```sql
SELECT * FROM Movie WHERE MovieTitle='The Amazing Maurice';
-- D: show all the information for the movie The Amazing Maurice
-- E: movie title
```
```sql
SELECT * FROM Movie WHERE ReleaseYear=2022;
-- D: show al the movies released in 2022
-- E: 2022 (release year)
```
```sql
SELECT Duration FROM Movie WHERE MovieTitle='M3GAN';
-- D: show duration of the movie M3GAN
-- E: movie title = M3GAN
```
```sql
SELECT * FROM Schedule WHERE MovieID=1;
-- D: show the schedule for the movie with ID = 1
-- E: movie ID = 1
```
```sql
select * FROM Schedule WHERE TheatreID=2;
-- D: shoe the schedule for theatre with ID = 1
-- E: theatre ID = 1
```
&nbsp;


## Part 3 Contextualised Summary
&nbsp;

### Write a 250-word summary of the information technology legislation

&nbsp;


## NZ information technology legislation

First it is important to understand how laws are created in NZ.

The Parliament is the suprime legislative power in New Zealand. 
It is made up of two parts: the sovereign (the governor general who officially sings off laws once Parliament has pass them), and the house of representatives.

For a bill to become a law, it must be introduced to the Parliament and have a first reading debate. If the majority of the MPs vote for the bill, It’s sent to a cross-party select committee for closer scrutiny and public submissions. The bill is reported back to the house with any recommended changes, and a second reading debate is held. 
After its second reading vote, MPs will debate the bill part by part, being this the last chance to change the bill. Then it goes for its third and final reading. If it passes, it is sent to the Governor General for royal assent before becoming New Zealand law.

the Key New Zealand laws are:
   
- Electronic Transactions Act 2002 : This act is primarily aimed at clarifying that electronic transactions do have legal recognition. It also contains Sections related to IT staff securely implementing solutions for electronic transactions (legal or commercial). As an IT Security professional working with an e-commerce system, the ETA will help you achieve : Authentication, Integrity of data and Non-reputation by providing Authentication & Integrity.Additional the act covers Times of dispatch & Receipt to allow for time critical transactions.
 

- Privacy Act of 2020 : it governs how organisations and businesses can collect, store, use and share your information. It ensures that you know when your information is being collected, used and shared appropriately.

- Harmful Digital Communications Act 2015 : tackles some of the ways people use technology to hurt others . It aims to prevent and reduce the impact of online bullying, harassment and other forms of abuse and intimidation.


- Public Records Act 2005 : establishes a regulatory framework for information and records management across the public sector.

- Copyright Act 1994 : allows copyright owners to control certain activities to the use and dissemination of their works.

&nbsp;


### Write a 250-word summary the ethical considerations you, as an IT professional, must consider.  This includes the organisational context and the impact of IT in the context of the New Horizons Cinema case study. 

&nbsp;

Professional ethics are the principles that dictate the behaviour of a person or group in a business environment. It provides rules on how a person should behave towards other people and institutions in such and environment. 

The ITC Code of Ethics is issued under the ITP (Institute of IT Professionals NZ Inc).
The 8 principles of the Code of Ethics are:

**Good faith :** treat people with dignity, good faith and equality.

**Integrity :** act in the execution of their profession with integrity, dignity and honour to merit the trust of the community and the profession.

**Community-focus :** responsibility for the welfare and rights of the community shall come before their responsibility to their profession.

**Skills :** apply skills and knowledge in the interests of their clients or employers

**Continuos Development :** develop knowledge, skills and expertise continuously through their careers.

**Informed Consent :** take reasonable steps to inform themselves, their clients or employers of the economic, social, environmental or legal consequences which may arise from their actions.

**Managed Conflicts of Interest :** inform their clients or employers of any interest which may be, or may be perceived as being, in conflict with the interests of their clients or employers, or which may affect the quality of service or impartial judgement

**Competence :** follow recognised professional practice, and provide services and advice carefully and diligently only within their areas of competence.


*I believe as IT professional we must always act with honesty, loyalty, respect for others, adherence to the law, doing good and avoiding harm to others and being accountable. This will provide benefits to the public, clients and members of the profession.*

*Regarding the impact on the New Horizon Cinema case study, following a professional ethic behaviour will set the right culture, by fostering an environment of trust, ethical behaviour, integrity, and excellence.
It will also build a good reputation for us and last but not least, it’ll help remain in compliance with laws and regulations.*









 







