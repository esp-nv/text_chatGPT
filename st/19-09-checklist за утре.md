````text
# Checklist – 2026-09-20

## Course Model

- [ ] Създаване на `Course.cs`
- [ ] Определяне на properties:
  - [ ] `Id`
  - [ ] `Code`
  - [ ] `Name`
  - [ ] `Description`
- [ ] Определяне на validation правилата за Course
- [ ] Определяне на максималните дължини на текстовите полета
- [ ] Добавяне на Course constants в `StudentConstants` или отделен `CourseConstants`

## Student ↔ Course

- [ ] Премахване на свободния текстов `Course` от `Student`
- [ ] Определяне на Many-to-Many relationship
- [ ] Създаване на `StudentCourse` entity
- [ ] Добавяне на `DbSet<Course>`
- [ ] Добавяне на `DbSet<StudentCourse>`, ако е необходимо
- [ ] Конфигуриране на връзката в `ApplicationDbContext`
- [ ] Проверка на EF Core model

## Database

- [ ] Проверка на генерираната migration
- [ ] Уверяване, че migration-ът не съдържа нежелани промени
- [ ] Създаване на Course migration
- [ ] Update-ване на database
- [ ] Проверка на таблиците:
  - [ ] `Courses`
  - [ ] `StudentCourses`
  - [ ] `Students`
- [ ] Проверка на foreign keys
- [ ] Проверка на primary keys
- [ ] Проверка на unique constraint/index за `Course.Code`, ако бъде взето решение да бъде unique

## Course Service

- [ ] Създаване на `ICourseService`
- [ ] Създаване на `CourseService`
- [ ] Реализиране на:
  - [ ] Get all courses
  - [ ] Get course by ID
  - [ ] Create course
  - [ ] Update course
  - [ ] Delete course

## Course UI

- [ ] Създаване на `CoursesController`
- [ ] Създаване на Course Views
- [ ] Create Course
- [ ] Edit Course
- [ ] Delete Course
- [ ] List Courses
- [ ] Details, ако е необходимо

## Student UI – Multi-select

- [ ] Премахване на старото свободно текстово поле за Course
- [ ] Добавяне на multi-select за Courses в `Create.cshtml`
- [ ] Добавяне на multi-select за Courses в `Edit.cshtml`
- [ ] Зареждане на наличните Courses
- [ ] Запазване на избраните Courses
- [ ] Зареждане на вече избраните Courses при Edit
- [ ] Проверка, че един Student може да има множество Courses
- [ ] Проверка, че един Course може да има множество Students

## Validation

- [ ] Проверка на `Code`
- [ ] Проверка на `Name`
- [ ] Проверка на `Description`
- [ ] Required полета да имат `*` в UI
- [ ] Model validation и database constraints да са синхронизирани

## Testing / Verification

- [ ] Build
- [ ] Create Course
- [ ] Edit Course
- [ ] Delete Course
- [ ] Create Student с един Course
- [ ] Create Student с няколко Courses
- [ ] Edit Student и промяна на Courses
- [ ] Проверка на Many-to-Many записите в `StudentCourses`
- [ ] Проверка на database schema
- [ ] Проверка на UI validation

## Не правим утре

- [ ] `CourseOffering`
- [ ] Година на провеждане
- [ ] Месец на провеждане
- [ ] Teacher
- [ ] CourseVersion
- [ ] Topics
- [ ] Enrollment

Тези неща остават за бъдеща версия, докато базовият `Course` Many-to-Many модел не бъде завършен и проверен.
