CREATE TABLE student(
BrIndeks VARCHAR (5) PRIMARY KEY NOT NULL,
Ime  VARCHAR (15) NOT NULL,
Prezime  VARCHAR (15) NOT NULL,
Komentar  TEXT
);
DROP TABLE student	/*KOMENTAR - brise tabelu*/

INSERT INTO student VALUES('001','Veljko','Krstic');
INSERT INTO student VALUES('002','Dragan','Danilovic');
INSERT INTO student VALUES('003','Dragana','Danilovic');
INSERT INTO student VALUES('004','Dragano','Danilovic','sa sela');
INSERT INTO student VALUES('005','Draganu','Danilovic','nema pernicu');

UPDATE student 			/*Zamena podatka prema definiciji*/		
SET prezime='Slavuj'
WHERE BrIndeks='003'

SELECT *
FROM student
ORDER BY BrIndeks ASC		/*Podesavanje redosleda alphabetic*/

SELECT *
FROM student
ORDER BY BrIndeks DESC		/*Podesavanje redosleda kontra*/


SELECT *
FROM student
WHERE prezime='Danilovic'

SELECT komentar  			/*Svi komentari sa prezimenom Danilovic*/
FROM student
WHERE prezime='Danilovic'

SELECT komentar as Komentari 			/*Menjamo naziv polja komentar*/
FROM student
WHERE prezime='Danilovic'

SELECT * 							/*SELEKTUJEMO SVE SA IC*/
FROM student
WHERE prezime LIKE '%ic'			/* % zamenjuje deo teksta ispred*/


SELECT * 							
FROM student
WHERE prezime LIKE 'D%ic'			



CREATE TABLE automobili(
BrSasije VARCHAR (20) PRIMARY KEY NOT NULL,
proizvodjac  VARCHAR (15) NOT NULL,
model  VARCHAR (15) NOT NULL,
cena  INTEGER
);
DROP TABLE automobili	/*KOMENTAR - brise tabelu*/

INSERT INTO automobili VALUES('5456465','Audi','a6',5000);
INSERT INTO automobili VALUES('5455436465','Audi','a4',15000);
INSERT INTO automobili VALUES('5456464455','porsche','911',25000);
INSERT INTO automobili VALUES('545644365','Mercedes','c',635000);
INSERT INTO automobili VALUES('545646665','BMW','x5',45000);


SELECT *
FROM automobili

/*Prikazati sve automobile preko 10 000*/
/*Sve automobile ciji naziv pocinje na P*/

SELECT *
FROM automobili
WHERE model LIKE 'c%'

SELECT *
FROM automobili
WHERE cena > 10000

UPDATE automobili
SET cena = NULL
WHERE proizvodjac = 'Mercedes' AND model = 'c'
