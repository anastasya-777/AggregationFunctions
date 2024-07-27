# AggregationFunctions

## Тема: Функции агрегирования.

## Данные в таблицах:

<img width="812" alt="image" src="https://github.com/user-attachments/assets/f3ba77fd-0b43-4ed0-9d6e-1bef60ff7082">

<img width="784" alt="image" src="https://github.com/user-attachments/assets/f8deae1d-2607-45ea-abf3-a8e37475f3e6">

### Запросы по заданию:

1. Вывести количество преподавателей кафедры “Software Development”.

### Скрипт запроса:

* SELECT COUNT(*) AS num_teachers
* FROM Teachers t
* JOIN Lectures l ON t.Id = l.TeacherId
* JOIN Departments d ON l.SubjectId = d.Id
* WHERE d.Name = 'Software Development';

### Результат:

<img width="589" alt="image" src="https://github.com/user-attachments/assets/6d7327ac-1c44-47c7-83db-58ab7797f596">

2. Вывести количество лекций, которые читает преподаватель “Dave McQueen”.

### Скрипт запроса:

* SELECT COUNT(*) AS num_lectures
* FROM Lectures l
* JOIN Teachers t ON l.TeacherId = t.Id
* WHERE t.Name = 'Dave McQueen' AND t.Surname = 'McQueen';

### Результат:

<img width="713" alt="image" src="https://github.com/user-attachments/assets/b2fa27f0-8084-4562-a4f1-bc42fd7cce50">

3. Вывести количество занятий, проводимых в аудитории “D201”.

### Скрипт запроса:

* SELECT COUNT(*) AS num_lectures
* FROM Lectures
* WHERE LectureRoom = 'D201';

### Результат:

<img width="659" alt="image" src="https://github.com/user-attachments/assets/6558491b-b708-4233-b938-63dd537ee383">

4. Вывести названия аудиторий и количество лекций, проводимых в них.

### Скрипт запроса:

* SELECT LectureRoom, COUNT(*) AS num_lectures
* FROM Lectures
* GROUP BY LectureRoom;

### Результат:

<img width="688" alt="image" src="https://github.com/user-attachments/assets/b9293702-c362-44cb-abdc-ef33d1cb79ea">

5. Вывести количество студентов, посещающих лекции преподавателя “Jack Underhill”.

### Скрипт запроса:

* SELECT COUNT(*) AS num_students
* FROM Groups g
* JOIN GroupsLectures gl ON g.Id = gl.GroupId
* JOIN Lectures l ON gl.LectureId = l.Id
* JOIN Teachers t ON l.TeacherId = t.Id
* WHERE t.Name = 'Jack' AND t.Surname = 'Underhill';

### Результат:

<img width="629" alt="image" src="https://github.com/user-attachments/assets/2bee5262-776b-4573-a47f-222cf418a610">

6. Вывести среднюю ставку преподавателей факультета “Computer Science”.

### Скрипт запроса:

* SELECT AVG(t.Salary) AS avg_salary
* FROM Teachers t
* JOIN Lectures l ON t.Id = l.TeacherId
* JOIN Departments d ON l.SubjectId = d.Id
* JOIN Faculties f ON d.FacultyId = f.Id
* WHERE f.Name = 'Computer Science';

### Результат:

<img width="696" alt="image" src="https://github.com/user-attachments/assets/e002345f-4a3f-4b9d-9902-e01a86408523">

7. Вывести минимальное и максимальное количество студентов среди всех групп.

### Скрипт запроса:

* SELECT
* MIN(g.Year) AS min_students,
* MAX(g.Year) AS max_students
* FROM Groups g;

### Результат:

<img width="698" alt="image" src="https://github.com/user-attachments/assets/5256fe33-0343-4405-884c-c09a35f75dd9">

8. Вывести средний фонд финансирования кафедр.

### Скрипт запроса:

* SELECT AVG(Financing) AS avg_financing
* FROM Departments;

### Результат:

<img width="682" alt="image" src="https://github.com/user-attachments/assets/7eb6180f-af83-4e97-bcf5-290894cec012">

9. Вывести полные имена преподавателей и количество читаемых ими дисциплин.

### Скрипт запроса:

* SELECT
* CONCAT(t.Name, ' ', t.Surname) AS full_name,
* COUNT(l.Id) AS num_subjects
* FROM Teachers t
* JOIN Lectures l ON t.Id = l.TeacherId
* GROUP BY CONCAT(t.Name, ' ', t.Surname);

### Результат:

<img width="698" alt="image" src="https://github.com/user-attachments/assets/4decf851-a316-46a9-913e-fcca1ea83ca2">

10. Вывести количество лекций в каждый день недели.

### Скрипт запроса:

* SELECT
* gl.DayOfWeek,
* COUNT(*) AS num_lectures
* FROM GroupsLectures gl
* GROUP BY gl.DayOfWeek;

### Результат:

<img width="760" alt="image" src="https://github.com/user-attachments/assets/c5b5569b-2bb9-4dc7-beb4-295fbcc16f2c">

11. Вывести номера аудиторий и количество кафедр, чьи лекции в них читаются.

### Скрипт запроса:

* SELECT
* l.LectureRoom,
* COUNT(DISTINCT l.SubjectId) AS num_departments
* FROM Lectures l
* GROUP BY l.LectureRoom;

### Результат:

<img width="754" alt="image" src="https://github.com/user-attachments/assets/69f2be92-2034-487c-9c8a-3e01b2c5a674">

12. Вывести названия факультетов и количество дисциплин,которые на них читаются.

### Скрипт запроса:

* SELECT
* f.Name AS faculty_name,
* COUNT(DISTINCT s.Id) AS num_subjects
* FROM Faculties f
* JOIN Departments d ON f.Id = d.FacultyId
* JOIN Lectures l ON d.Id = l.SubjectId
* JOIN Subjects s ON l.SubjectId = s.Id
* GROUP BY f.Name;

### Результат:

<img width="781" alt="image" src="https://github.com/user-attachments/assets/07f3b982-e11b-4979-b1cb-4cba63ba8213">

