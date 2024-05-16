GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(id) AS `iscritti`, YEAR(`enrolment_date`) AS `anno` FROM `students` GROUP BY `anno`;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(id) AS `numero_insegnanti`, `office_address` AS `ufficio` FROM `teachers` GROUP BY `ufficio`;

3. Calcolare la media dei voti di ogni appello d'esame
SELECT `exam_id`, AVG(`vote`) AS `media_voto` FROM `exam_student` GROUP BY `exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT COUNT(`name`)AS `numero_corsi`, `department_id` AS `dipartimento` FROM `degrees` GROUP BY `dipartimento`;


JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT `students`.`name`, `students`.`surname`,`degrees`.`name` FROM `students` INNER JOIN `degrees` ON `students`.`degree_id`=`degrees`.`id` WHERE `degrees`.`name`='Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze


3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.