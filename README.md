1. Selezionare tutti gli studenti nati nel 1990 (160)
SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = 1990;

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
SELECT * FROM `courses` WHERE `cfu`> 10;

3. Selezionare tutti gli studenti che hanno più di 30 anni

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
SELECT * FROM `courses` WHERE `year`= 1 AND `period` LIKE "I %";

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
SELECT * FROM `exams` WHERE `hour` LIKE '14%' AND `date`='2020-06-20';
//SOLO 7 RISULTATI