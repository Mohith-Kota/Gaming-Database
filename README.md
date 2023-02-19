# Gaming-Database

USE CASE PROBLEM DEFINITION:
A) Business Problem and Requirement:
Now-a-days Video games are going digital. Most of the store platforms, whether
online or offline, have their own databases to record all the Sales data. Some of them
can be accessed by the public, like Steam DB, but all the data on different stores are
not linked, which could bring a lot of trouble for Business Investigation and Analytics.
Boston Consulting group decided to build a database to store the Sales data, as a
consulting tool and open to their customer.
The database is solving practical problems in the gaming industry. For the publisher, it
will help them to decide the publishing region while planning for a potential profit
game. With this database they will get more data support rather than only relying on
experience. When conducting competitive analysis, by searching for region, revenue,
cooperated developers and other data of games published by their competitors they
will stand a greater chance in the fierce competition.
The database is also an ideal tool for developers. They can find more business
opportunities from different regions by catering specific needs of customers. By
analyzing customers, they will have a clearer direction in the development.
In this database, the following relationship should be followed while implementing:

1. Developer group focuses on developing games. They can develop multiple
games and a game can be developed by multiple developer groups. And in
most circumstances they will have a cooperation relationship with the
publisher. Developer group can cooperate with multiple publishers, vice versa.
For each developer group, they have a unique group number. The size and
name of the developer group are also required for recording.

2. We can divide Developer groups into two types: In-Publisher Developer group
and Freelancers. In-Publisher Developer Groups work for specific publishers.
For freelancers, they may have contracts with one or multiple publishers,
publishing different games developed by them. A developer group can’t be
freelancers and an In-Publisher Developer group at the same time. Freelancers
can negotiate with stores directly, once the store allows, they can sell games
directly on the store. In this process free-lancers should give a recommended
price for the game.

3. Publishers publish games. They can publish multiple games and have them
running at the same time. And publisher will tie up with at least 1 store as a
platform to sell their games. For publisher we need to store their unique
number (PBN), name, size, address and games they have published. A
publisher can have multiple addresses and multiple published game.

4. Store can be divided into online store and offline store. Some stores are online
and offline at the same time, like GameStop. A store can cooperate with
multiple publishers, and sometimes can be 0. Store sells games to players. At
different times, a game might be on discount. Games can have different prices
in different stores. Players buy games from the store. They can buy from
multiple stores while stores can of course have multiple customers. We should
store STN as a unique number for the store, as well as their name. Besides, the 
platform they are on should be required. A store can have multiple platforms.
(e.g. PlayStation Store is only available on PlayStation while Xbox Store is
available on PC and XBOX. ). For offline stores we need to store their
addresses, which could be more than one. The website of an online store is
required too.

5. Games can be divided into 2 types: Account Required Game and Account Not
Required Game. Players must register an account to access the Account
Required Game they buy. They can create accounts with the same name in
different games. For account the storage of Account number, Balance,
Creating time and Game number are required. An account belongs to a
specific game. For Account Not Required Game, players can directly enjoy it
after purchasing. However, for Free- Lancers, they can only develop Account
Not Required Game due to lack of publishers. We need tables to store the
unique game number, name, genre, version, and license status and publisher
number.

6. Players can buy games from various stores. To do further analysis, we need
some information, including SSN, Age, Name, address and birthdate.
B) Conceptual Data Modeling
EER MODEL
UML MODEL
C) Mapping Conceptual Model to Relational Model
PLAYER( SSN, Name, Birthdate, Address, Age)
ACCOUNT( ACN, GMN, SSN, Balance, Creating Time, Login Time)
- GMN foreign key refers to GMN in GAMES, NOT NULL
- SSN Foreign key refers to SSN in PLAYER, NOT NULL
ACCOUNT REQUIRED( AR.GMN, …)
- AR.GMN Foreign key refers to GMN in GAMES, NOT NULL
ACCOUNT NOT REQUIRED(ANR.GMN, …)
- ANR.GMN Foreign key refers to GMN in GAMES, NOT NULL
PLAY DIRECTLY( SSN, GMN)
- SSN Foreign key refers to SSN in PLAYER, NOT NULL
- GMN foreign key refers to GMN in GAMES, NOT NULL
STORE(STN, Name, Platform)
ONLINE STORE( Online.STN, Website, …)
- Online.STN Foreign key refers to STN in STORE, NOT NULL
PHYSICAL STORE( Physical.STN, Address, …)
- Physical.STN Foreign key refers to STN in STORE, NOT NULL
BUY GAMES FROM( SSN, STN, Membership Status)
- STN Foreign key refers to STN in STORE, NOT NULL
- SSN Foreign key refers to SSN in PLAYER, NOT NULL
SELL( GMN, STN, Price, Time)
- STN Foreign key refers to STN in STORE, NOT NULL
- GMN foreign key refers to GMN in GAMES, NOT NULL
TIE-UP( PBN, STN)
- STN Foreign key refers to STN in STORE, NOT NULL
- PBN Foreign key refers to PBN in PUBLISHER, NOT NULL
COLLABORATE( STN, FLG.DGN, Recommended Price)
- STN Foreign key refers to STN in STORE, NOT NULL
- FLG.DGN Foreign key refers to DGN in DEVELOPER GROUP, NOT NULL
GAMES( GMN, Name, Genre, Version, License Status, Account, Region, PBN)
- PBN Foreign key refers to PBN in PUBLISHER, NOT NULL
PUBLISHER( PBN, Name, Size, Games,
Address ) DEVELOPER GROUP( DGN,
Name, Size)
IN-PUBLISHER DEVELOPER GROUP( IP.DGN, PBN, …)
- PBN Foreign key refers to PBN in PUBLISHER, NOT NULL
FREELANCER GROUP( FLG.DGN,
…) CO-OPERATION( PBN,
DGN )
- PBN Foreign key refers to PBN in PUBLISHER, NOT NULL
- DGN Foreign key refers to DGN in DEVELOPER GROUP, NOT NULL
CONTRACT( PBN, FLG.DGN, Fee, Revenue Distribution)
- PBN Foreign key refers to PBN in PUBLISHER, NOT NULL
- FLG.DGN Foreign key refers to DGN in DEVELOPER GROUP, NOT NULL
DEVELOPED(GMN, DGN)
- GMN foreignkey refers to GMN in GAMES, NOT NULL
- DGN Foreign key refers to DGN in DEVELOPER GROUP, NOT NULL
DESIGN( FLG.DGN, ANR.GMN )
- ANR.GMN foreign key refers to GMN in GAMES, NOT NULL
- FLG.DGN Foreign key referstoDGNinDEVELOPER GROUP, NOT
NULL DESIGNER GROUP( DGN )

D) Implementation of Relation Model via MySQL & NoSQL
