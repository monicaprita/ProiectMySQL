## Database Project for **Books**
 The scope of this project is to use all the SQL knowledge gained throught the Software Testing course and apply them in practice.

Application under test: Books

Tools used: MySQL Workbench

Database description: I created a database named Books. In this database, I created 5 tables named: Autori, Edituri, Gen Carti, Carti si Autori carti. I added and deleted different datas, I created principal and foreign keys, I made different joins between tables and I created a subquerie.

  1. Database Schema

     You can find below the database schema that was generated through Reverse Engineer and which contains all the tables and the relationships between them.
    ![Diagrama](https://github.com/monicaprita/ProiectMySQL/assets/154963887/1434da52-bff6-4dfd-b287-175c9846f274)

      The tables are connected in the following way:

     * **Autori** is connected with **Autori_carti** through a **one to many** relationship which was implemented through **Autori.ID_autori** as a primary key and 
      **Autori_carti.ID_autori** as a foreign key
     * **Carti** is connected with **Autori_carti** through a **many to one** relationship which was implemented through **Carti.ID_carte** as a primary key and 
      **Autor_carti.ID_carte** as a foreign key
     * **Carti** is connected with **Gen_carti** through a **many to one** relationship which was implemented through **Gen_carti.ID_gen** as a primary key and 
      **Carti.ID_gen** as a foreign key
     * **Carti** is connected with **Edituri** through a **one to one** relationship which was implemented through **Edituri.ID_editura** as a primary key and 
      **Carti.ID_editura** as a foreign key
    
       
   2. Database Queries
      
      i. DDL (Data Definition Language)
      
         The following instructions were written in the scope of CREATING the structure of the database (CREATE INSTRUCTIONS)
      
      * create database Books;
      * create table Autori(
       ID_autori int not null auto_increment primary key,
       Nume_autor varchar(20) not null,
       Prenume_autor varchar(20) not null
);
      * create table Edituri(
	  ID_editura int not null auto_increment primary key,
    Nume_editura varchar(50)
);
      * create table Gen_carti(
     ID_gen int not null auto_increment primary key,
     Nume_categorie varchar(30)
);
      * create table Carti(
      ID_carte int not null auto_increment primary key,
      Titlu varchar (50),
      An_publicare date not null,
      ID_editura int not null,
      ID_gen int not null,
      constraint fk_Carti_Edituri foreign key (ID_editura) references Edituri (ID_editura), constraint fk_Carti_Gen_carti foreign key (ID_gen) references Gen_carti (ID_gen)	
);
      * create table Autori_carti(
        ID_autori int not null,
        ID_carte int not null,
        constraint fk_Autor_carti_Autori foreign key (ID_autori) references Autori(ID_autori), constraint fk_Autor_carti_Carti foreign key (ID_carte) references Carti(ID_carte)
);
         
      ii. DML (Data Manipulation Language)
       In order to be able to use the database I populated the tables with various data necessary in order to perform queries and manipulate the data. In the testing process, this necessary data is identified in 
the Test Design phase and created in the Test Implementation phase.

       Below you can find all the insert instructions that were created in the scope of this project:
       * insert into Autori (Nume_autor, Prenume_autor)
values 
   ('Hill', 'Napoleon'),
   ('Batchelor', 'Doug'),
   ('Riordan', 'Rick'),
   ('Dostoievschi', 'Feodor'),
   ('Aristocles', 'Platon'),
   ('Kwik', 'Jim'),
   ('Einat', 'Nathan'),
   ('Dobson', 'James'),
   ('Shetty', 'Jay'),
   ('Kiyosaki', 'Robert');
       * insert into Edituri (Nume_editura)
values
    ('Curtea Veche'),
    ('Litera'),
    ('Imago Dei'),
    ('Lifestyle'),
    ('Editura pentru literatura universala'),
    ('IRI'),
    ('Arthur'),
    ('Viata si Sanatate'),
    ('Librex');
      * insert into Gen_carti (Nume_categorie)
values 
	('Literatura clasica'),
	('Dezoltare personala'),
	('Parenting'),
	('Autobiografie'),
	('Fantasy'),
  ('Filosofie'),
  ('Psihologie practica');
       * insert into Carti(Titlu, An_publicare, ID_editura, ID_gen)
values
    ('Cria si pedeapsa', 2022, 2, 1),
    ('Adolescentul', 1957, 5, 1),
    ('Fara limite', 2021, 4, 2),
    ('Baietii, cum sa-i crestem', 2010, 3, 3),
    ('Indrazneste sa disciplinezi', 2010, 3, 3),
    ('Tot ce am mai drag', 2022, 1, 3),
    ('Cel mai bogat om din pestera', 2013, 8, 4),
    ('Tata bogat, tata sarac', 2019, 1, 2),
    ('Gandeste ca un calugar', 2020, 2, 2),
    ('Eroul pierdut', 2021, 7, 5),
    ('Dialoguri', 1998, 6, 6),
    ('Gandeste si vei fi bogat', 2023, 9, 7);
        * insert into Autor_carti (ID_autori, ID_carte)
values 
     (1, 12),
     (2, 7),
     (3, 10),
     (4, 1),
     (5, 11),
     (6, 3),
     (7, 6),
     (8, 4),
     (9, 9),
     (10, 8),
     (4, 2),
     (8, 5);


	  iii. DQL (Data Query Language)
               In order to simulate various scenarios that might happen in real life I created the following queries that would cover multiple potential real-life situations:
         * Return all data from the Autori table:
           
           ```sql
           select * from Autori;
           ```
         * Return all data from the Edituri table:
           ```sql
           select * from Edituri;
           ```
         * Return all data from the Gen_carti table:
           ```sql
           select * from Gen_carti;
           ```
         * Return all data from the Carti table:
           ```sql
            *select * from Carti;
           ```
         * Return all data from the Autori_carti table:
           ```sql
           select * from Autori_carti;
           ```
         * Return all data from the Carti table and Edituri table, ordered by ID_editura:
           ```sql
           select * from carti inner join edituri on carti.ID_editura = edituri.ID_editura;
           ```
         * Return all data from the Carti table and Edituri table, ordered by ID_carte:
           ```sql
           select * from carti left join edituri on carti.ID_editura = edituri.ID_editura;
           ```
         * Return data from the carti table and edituri table and the ID_editura is null:
           ```sql
           select * from carti left join edituri on carti.ID_editura = edituri.ID_editura where edituri.ID_editura is null;
           ```
         * Return data from the carti table and edituri table and the ID_editura is not null:
           ```sql
           select * from carti left join edituri on carti.ID_editura = edituri.ID_editura where edituri.ID_editura is not null;
           ```
         * Return all data from edituri table with the name 'Iamgo Dei':
           ```sql
           select * from edituri where Nume_editura = 'Imago Dei';
           ```
         * Return all data from the Carti table and Edituri table that have Nume_editura = 'Imago Dei':
           ```sql
           select * from carti left join edituri on carti.ID_editura = edituri.ID_editura where Nume_editura = 'Imago Dei';
           ```
         * Return all names from Autori table who contains letter 'r':
           ```sql
           select * from Autori where Nume_autor like "%r%";
           ```
         * Returns all data from Carti table where An_publicare starts with 2 and the title of the book contains letter 'e':
           ```sql
           select * from carti where An_publicare like '2%' and Titlu like '%e%';
           ```
         * Return all data from Carti where Id_gen is not 1 or 7:
           ```sql
           select * from CArti where not ID_gen = '1' and not ID_gen = '7';
           ```
         * Return the lowest year of publication from carti table:
           ```sql
           select min(An_publicare) from Carti;
           ```
         * Return the number of the books from carti table:
           ```sql
           select count(*) from Carti;
           ```
         * Returning the lowest year of publication and the ID_editura from Carti table:
           ```sql
           select min(An_puclicare), ID_editura from Carti group by ID_editura;
           ```
         * Return of the data from the Carti table in ascending order of the year of publication:
         ```sql
         select * from Carti order by An_publicare;
         ```
        * Return of 5 datas from the Carti table in ascending order of the year of publication:
          ```sql
          select * from Carti order by An_publicare limit 5;
          ```
        * Return of a list of books from the Carti table but with only names from nume_editura that contains "i":
          ```sql
          select ID_editura, Titlu, An_publicare from Carti where ID_editura in (select ID_editura from Edituri where Nume_editura like '%i%');
          ```
        * Return of a list of books from the Carti table but with only names from nume_editura that contains "i" using inner join:
          ```sql
          select ID_editura, Titlu, An_pubicare from Carti c inner join edituri e on c.ID_editura = e.ID_editura where e.Nume_editura like '%i%';
          ```
        * Return of all columns of Edituri table, where publishers has books with An_publicare at least 2021:
          ```sql
          select *from Edituri e where ID_edituri in (select ID_editura drom Edituri e inner join Carti c on E.ID_editura = C.ID_editura where extract (year from c.An_publicare)>2021;
          ```
       
  4. Conclusions
     
     The creation of the "Books" database signifies an important step towards building a robust and scalable system for managing book-related information. It provides a structured framework that will support the development of applications, reporting tools, or any other systems that rely on accurate and organized book data.
