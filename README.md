CREATE TABLE student(
BrIndeks VARCHAR (5) PRIMARY KEY NOT NULL,
Ime  VARCHAR (15) NOT NULL,
Prezime  VARCHAR (15) NOT NULL,
Komentar  TEXT
);
DROP TABLE student	/*KOMENTAR - pravi tabelu*/

INSERT INTO student VALUES('001','Veljko','Krstic');
INSERT INTO student VALUES('002','Dragan','Danilovic');
INSERT INTO student VALUES('003','Dragana','Danilovic');
INSERT INTO student VALUES('004','Dragano','Danilovic','sa sela');
INSERT INTO student VALUES('005','Draganu','Danilovic','nema pernicu');

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

