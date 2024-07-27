# AggregationFunctions

## Тема: Функции агрегирования.

### Запросы

1. Вывести количество преподавателей кафедры “Software Development”.

### Скрипт запроса:
SELECT COUNT(*) AS num_teachers
FROM Teachers t
JOIN Lectures l ON t.Id = l.TeacherId
JOIN Departments d ON l.SubjectId = d.Id
WHERE d.Name = 'Software Development';
### Результат:

2. Вывести количество лекций, которые читает преподаватель “Dave McQueen”.

### Скрипт запроса:
SELECT COUNT(*) AS num_lectures
FROM Lectures l
JOIN Teachers t ON l.TeacherId = t.Id
WHERE t.Name = 'Dave McQueen' AND t.Surname = 'McQueen';
### Результат:

3. Вывести количество занятий, проводимых в аудитории “D201”.

### Скрипт запроса:
SELECT COUNT(*) AS num_lectures
FROM Lectures
WHERE LectureRoom = 'D201';
### Результат:

4. Вывести названия аудиторий и количество лекций, проводимых в них.

### Скрипт запроса:
SELECT LectureRoom, COUNT(*) AS num_lectures
FROM Lectures
GROUP BY LectureRoom;
### Результат:

5. Вывести количество студентов, посещающих лекции преподавателя “Jack Underhill”.

### Скрипт запроса:
SELECT COUNT(*) AS num_students
FROM Groups g
JOIN GroupsLectures gl ON g.Id = gl.GroupId
JOIN Lectures l ON gl.LectureId = l.Id
JOIN Teachers t ON l.TeacherId = t.Id
WHERE t.Name = 'Jack' AND t.Surname = 'Underhill';
### Результат:

6. Вывести среднюю ставку преподавателей факультета “Computer Science”.

### Скрипт запроса:
SELECT AVG(t.Salary) AS avg_salary
FROM Teachers t
JOIN Lectures l ON t.Id = l.TeacherId
JOIN Departments d ON l.SubjectId = d.Id
JOIN Faculties f ON d.FacultyId = f.Id
WHERE f.Name = 'Computer Science';
### Результат:

7. Вывести минимальное и максимальное количество студентов среди всех групп.

### Скрипт запроса:
SELECT
MIN(g.Year) AS min_students,
MAX(g.Year) AS max_students
FROM Groups g;
### Результат:

8. Вывести средний фонд финансирования кафедр.

### Скрипт запроса:
SELECT AVG(Financing) AS avg_financing
FROM Departments;
### Результат:

9. Вывести полные имена преподавателей и количество читаемых ими дисциплин.

### Скрипт запроса:
SELECT
CONCAT(t.Name, ' ', t.Surname) AS full_name,
COUNT(l.Id) AS num_subjects
FROM Teachers t
JOIN Lectures l ON t.Id = l.TeacherId
GROUP BY CONCAT(t.Name, ' ', t.Surname);
### Результат:

10. Вывести количество лекций в каждый день недели.

### Скрипт запроса:
SELECT
gl.DayOfWeek,
COUNT(*) AS num_lectures
FROM GroupsLectures gl
GROUP BY gl.DayOfWeek;
### Результат:

11. Вывести номера аудиторий и количество кафедр, чьи лекции в них читаются.

### Скрипт запроса:
SELECT
l.LectureRoom,
COUNT(DISTINCT l.SubjectId) AS num_departments
FROM Lectures l
GROUP BY l.LectureRoom;
### Результат:

12. Вывести названия факультетов и количество дисциплин,которые на них читаются.

### Скрипт запроса:
SELECT
f.Name AS faculty_name,
COUNT(DISTINCT s.Id) AS num_subjects
FROM Faculties f
JOIN Departments d ON f.Id = d.FacultyId
JOIN Lectures l ON d.Id = l.SubjectId
JOIN Subjects s ON l.SubjectId = s.Id
GROUP BY f.Name;
### Результат:
