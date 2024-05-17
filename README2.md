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
SELECT `students`.`name`, `students`.`surname`,`degrees`.`name` 
FROM `students` 
INNER JOIN `degrees`
ON `students`.`degree_id`=`degrees`.`id`
WHERE `degrees`.`name`='Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze
SELECT `departments`.*, `degrees`.*
FROM `departments` 
INNER JOIN `degrees` 
ON `departments`.`id` = `degrees`.`department_id` 
WHERE `departments`.`name`='Dipartimento di Neuroscienze' 
AND `degrees`.`level`= 'magistrale';

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT `courses`.`name`AS `corso`, CONCAT(`teachers`.`name`,'',`teachers`.`surname`)AS `nome_insegnante` 
FROM `teachers` 
INNER JOIN `course_teacher` 
ON `teachers`.`id`= `course_teacher`.`teacher_id` 
INNER JOIN `courses` 
ON `course_teacher`.`course_id`=`courses`.`id` 
WHERE `teacher_id` = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome
SELECT CONCAT(`students`.`surname`,' ',`students`.`name`)AS `nome_studente`, `degrees`.*, `departments`.`name`AS `nome_dipartimento` 
FROM `students` 
INNER JOIN `degrees` 
ON `students`.`degree_id`= `degrees`.`id` 
INNER JOIN `departments` 
ON `degrees`.`department_id`= `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name` ASC;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT `degrees`.`name` AS `corso_di_laurea`, `courses`.`name` AS `corso`, CONCAT(`teachers`.`name`,' ',`teachers`.`surname`)AS `nome_insegnante` 
FROM `degrees` 
INNER JOIN `courses`
ON `degrees`.`id`= `courses`.`degree_id` 
INNER JOIN `course_teacher` 
ON `courses`.`id`= `course_teacher`.`course_id` 
INNER JOIN `teachers` 
ON `course_teacher`.`teacher_id`= `teachers`.`id`;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)

SELECT `teachers`.`name`, `teachers`.`surname`, `departments`.`name`
FROM `teachers`
    INNER JOIN `course_teacher`
        ON `teachers`.`id`=`course_teacher`.`teacher_id`
    INNER JOIN `courses`
        ON `course_teacher`.`course_id`=`courses`.`id`
    INNER JOIN `degrees`
        ON `courses`.`degree_id`=`degrees`.`id`
    INNER JOIN `departments`
        ON `degrees`.`department_id`=`departments`.`id`
WHERE `departments`.`name`= 'Dipartimento di Matematica';


7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.

SELECT `students`.`id`, `students`.`name`, `students`.`surname`, MAX(`exam_student`.`vote`) AS `voto_max`, `courses`.`name` AS `course_name`, COUNT(*) AS `tentativi`
FROM `students`
    INNER JOIN `exam_student`
        ON `students`.`id`= `exam_student`.`student_id`
    INNER JOIN `exams`
        ON `exam_student`.`exam_id`= `exams`.`id`
    INNER JOIN `courses`
        ON `courses`.`id` =`exams`.`course_id`
    GROUP BY `students`.`id`, `course`.`id`
    HEAVING `voto_max`>= 18;