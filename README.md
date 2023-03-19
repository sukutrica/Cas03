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


/* sa casa */

CREATE TABLE grad(
Postanski_Broj INTEGER PRIMARY KEY NOT NULL,
Naziv VARCHAR (15) NOT NULL,
BrStanovnika INTEGER NOT NULL
);


CREATE TABLE zgrada(
BR_Zgrada INTEGER NOT NULL,  				/*povezivanje sa drugim tabelama*/
Adresa VARCHAR (30) NOT NULL,
Postanski_Broj INTEGER NOT NULL,
PRIMARY KEY (BR_Zgrada),  					/*povezivanje sa drugim tabelama*/
FOREIGN KEY (Postanski_Broj) REFERENCES grad (PostanskiBroj)  /*referenciranje sa grad tabelom*/
);

CREATE TABLE stan(
	BR_Stana INTEGER NOT NULL,  				/*povezivanje sa drugim tabelama*/
	BR_Zgrada INTEGER NOT NULL,
	Cena INTEGER NOT NULL,
	Kvadratura INTEGER NOT NULL,
	PRIMARY KEY (BR_Stana),  					/*povezivanje sa drugim tabelama*/
	FOREIGN KEY (BR_Zgrada) REFERENCES zgrada (BR_Zgrada)  /*referenciranje sa grad tabelom*/
	);



INSERT INTO grad VALUES(11000,'Beograd',2000000);
INSERT INTO grad VALUES(21000,'Novi Sad',500000);
INSERT INTO grad VALUES(15000,'Sabac',55000);

INSERT INTO ZGRADA VALUES(1,'Nikole Pasica 28',11000);
INSERT INTO ZGRADA VALUES(2,'Nade Dimic 4',11000);
INSERT INTO ZGRADA VALUES(3,'Safarikova 21',21000);
INSERT INTO ZGRADA VALUES(4,'Mihajla Pupina bb',21000);
INSERT INTO ZGRADA VALUES(5,'Stefana Prvovencanog 1',15000);
INSERT INTO ZGRADA VALUES(6,'Zike Popovica 69',15000);
INSERT INTO ZGRADA VALUES(7,'Vojislava Ilica 15',15000);

INSERT INTO stan VALUES(1,1,100000,50);
INSERT INTO stan VALUES(2,1,90000,40);
INSERT INTO stan VALUES(3,2,100000,80);
INSERT INTO stan VALUES(4,3,50000,40);
INSERT INTO stan VALUES(5,4,20000,35);
INSERT INTO stan VALUES(6,5,100000,100);
INSERT INTO stan VALUES(7,6,50000,60);
INSERT INTO stan VALUES(8,7,20000,30);
INSERT INTO stan VALUES(9,3,100000,120);
INSERT INTO stan VALUES(10,5,100000,50);



SELECT * FROM student
WHERE prezime LIKE 'D%ic'





SELECT * FROM Grad

SELECT * FROM ZGRADA

SELECT * FROM stan


SELECT PostanskiBroj  						/*prikazati postanksi broj za Beograd*/
FROM grad
WHERE Naziv='Beograd'

SELECT  BR_Zgrada							/*prikazati sve zgrade na Pos 15000*/
FROM zgrada
WHERE Postanski_Broj = 15000			

SELECT kvadratura 							/*prikazati kvadraturu u zgradu 5*/
FROM stan
WHERE BR_Zgrade = 5	

SELECT * 									/*SELEKTUJEMO SVE SA IC*/
FROM stan
WHERE BR_Zgrade = 6 or BR_Zgrade = 7 	

SELECT Cena/Kvadratura AS "Cena po kvadratu" 			/*proveriti sto ne radi*/
FROM stan
WHERE BR_Zgrade=1 

select BR_Zgrada,BR_Zgrade,Z.Adresa,GR.Naziv
FROM ZGRADA Z,GRAD GR
WHERE Z.Postanski_Broj=GR.Postanski_Broj

/*PRIKAZATI PB NAZIV GRADA I ADRESU ZA SVE ZGRADE*/
SELECT GR.POSTANSKIBROJ, GR.NAZIV AS GRAD, Z.ADRESA
FROM GRAD GR, ZGRADA Z 
WHERE GR.POSTANSKIBROJ=Z.POSTANSKI_BROJ

/* PRIAZATI BROJ STANA, POSTANSKI BROJ I CENU ZA SVAKI STAN */
SELECT S.BR_STANA,Z.Postanski_Broj,Z.ADRESA,S.CENA
FROM STAN S, ZGRADA Z
WHERE S.BR_Zgrade=Z.BR_Zgrada

/* prikazati br stana naziv grada adresu i cenu za svaki stan*/

SELECT S.BR_Stana, GR.Naziv, Z.Adresa, S.Cena
FROM GRAD GR, ZGRADA Z, STAN S
WHERE GR.Postanski_Broj = Z.Postanski_Broj AND S.BR_Zgrade = Z.BR_Zgrada



DROP TABLE ZGRADA
DROP TABLE grad
DROP TABLE STAN




CREATE TABLE GRAD(
PB INTEGER PRIMARY KEY NOT NULL,
NAZIV VARCHAR (15) NOT NULL
);
INSERT INTO GRAD VALUES(11000,'Beograd');
INSERT INTO GRAD VALUES(21000,'Novi Sad');
INSERT INTO GRAD VALUES(13000,'Pancevo');
INSERT INTO GRAD VALUES(10000,'Mirijevo');
INSERT INTO GRAD VALUES(15000,'Sabac');

CREATE TABLE KAFIC(
IDLOKAL INTEGER NOT NULL,
ADRESA VARCHAR (40) NOT NULL,
PB INTEGER NOT NULL,
PRIMARY KEY (IDLOKAL),
FOREIGN KEY (PB) REFERENCES GRAD (PB) 
);
INSERT INTO KAFIC VALUES(1,'Marsala Birjuzova',11000);
INSERT INTO KAFIC VALUES(2,'Glavna',11000);
INSERT INTO KAFIC VALUES(3,'Glavna',15000);
INSERT INTO KAFIC VALUES(4,'Mocartova',15000);
INSERT INTO KAFIC VALUES(5,'Brace Ribnikar',21000);
INSERT INTO KAFIC VALUES(6,'Stefana Stefanovica',21000);

/* PRIKAZATI ADRESU KAFICA BR 5 */
/* PRIKAZATI GRAD U KOJEM JE KAFIC BR 5 */
/* NAZIV GRADA I ADREU U KOJOJ JE KAFIC 2 */
/* PRIKAZATI SVE KAFICE SORTIRANE PO ID OPADAJUCE */

SELECT ADRESA
FROM KAFIC
WHERE IDLOKAL=5

SELECT GR.NAZIV
FROM KAFIC KA, GRAD GR
WHERE KA.IDLOKAL=5 AND KA.PB=GR.PB

SELECT KA.ADRESA,GR.NAZIV
FROM KAFIC KA, GRAD GR
WHERE KA.IDLOKAL=2 AND KA.PB=GR.PB

SELECT 
FROM KAFIC KA, GRAD GR
WHERE KA.IDLOKAL=2 AND KA.PB=GR.PB

SELECT *
FROM KAFIC
ORDER BY IDLOKAL DESC

SELECT * FROM GRAD
SELECT * FROM KAFIC

DROP TABLE GRAD
DROP TABLE KAFIC

