GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(id) AS `iscritti`, YEAR(`enrolment_date`) AS `anno` FROM `students` GROUP BY `anno`;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(id) AS `numero_insegnanti`, `office_address` AS `ufficio` FROM `teachers` GROUP BY `ufficio`;

3. Calcolare la media dei voti di ogni appello d'esame
SELECT `exam_id`, AVG(`vote`) AS `media_voto` FROM `exam_student` GROUP BY `exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento