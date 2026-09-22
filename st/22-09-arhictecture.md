````text
архитектурата до момента, като я разделям на модели, връзки, база и бизнес правила.

1. Общата архитектура
StudentManagement
│
├── Models
│   ├── Student
│   ├── Area
│   ├── StudyProgram
│   ├── Module
│   ├── Course
│   ├── CourseOffering
│   └── Enrollment
│
├── Data
│   └── ApplicationDbContext
│
├── Common
│   ├── Constants
│   └── Enums
│       └── EnrollmentStatus
│
├── Migrations
│
└── UI
    └── Student CRUD

2. Основните връзки
Архитектурата на учебната част в момента е:

Area
 │
 └── 1 : N
       │
       ▼
StudyProgram
 │
 └── 1 : N
       │
       ▼
Module
 │
 └── N : N
       │
       ▼
Course
 │
 └── 1 : N
       │
       ▼
CourseOffering
 │
 └── 1 : N
       │
       ▼
Enrollment
       ▲
       │ N : 1
       │
     Student

Тоест:

една Area има много StudyProgram;

един StudyProgram има много Module;

един Module може да участва в много Course;

един Course може да има много CourseOffering;

едно CourseOffering има много Enrollment;

един Student може да има много Enrollment.

3. Area
Area
├── Id
├── Code
├── Name
├── Description
├── IsDeleted
└── StudyPrograms

Имаме ограничения чрез constants + DataAnnotations:

Code
Name
Description

4. StudyProgram
StudyProgram
├── Id
├── AreaId
├── Code
├── Name
├── Description
├── IsDeleted
├── Area
└── Modules

Връзката е:

Area 1 ─────── N StudyProgram

и в базата е:

ON DELETE NO ACTION

т.е. Restrict.

5. Module
Module
├── Id
├── StudyProgramId
├── Name
├── Description
├── IsDeleted
├── StudyProgram
└── Courses

Връзката:

StudyProgram 1 ─────── N Module

и:

Module N ─────── N Course

се реализира чрез междинната таблица:

CourseModule
├── CoursesId
└── ModulesId

И двете FK връзки са Restrict.

6. Course
Course
├── Id
├── Code
├── Name
├── Description
├── IsDeleted
└── Modules

За V1 умишлено го държим прост.

Не сме добавили още:

Online/OnSite;

Hybrid;

Schedule;

Attendance;

Exams;

Payments;

Assignments.

Тези неща могат да дойдат във V2.

7. CourseOffering
Това е конкретното провеждане на даден курс.

CourseOffering
├── Id
├── CourseId
├── StartDate
├── EndDate
├── Year
├── Capacity
├── IsDeleted
└── Course

Year не се пази в базата:

public int Year => StartDate.Year;

Така няма риск някой да зададе:

StartDate = 2026
Year = 2027

Имаме и правило:

EndDate >= StartDate

То е защитено на две нива:

UI / Model
    ↓
IValidatableObject

Database
    ↓
CHECK CONSTRAINT
CK_CourseOffering_EndDate_After_StartDate

8. Enrollment
Това е връзката между Student и конкретно CourseOffering.

Enrollment
├── Id
├── StudentId
├── CourseOfferingId
├── EnrollmentDate
├── Status
├── IsDeleted
├── Student
└── CourseOffering

Това е много важен модел, защото представлява целия жизнен цикъл на записването.

9. EnrollmentStatus
В:

Common/Enums

имаме:

public enum EnrollmentStatus
{
    Pending = 1,
    Active = 2,
    Cancelled = 3,
    Completed = 4,
    Failed = 5,
    NotAttended = 6
}

Числата са умишлени.

Така ако по-късно някой добави нов статус, съществуващите стойности няма да се разместят.

В SQL Server:

Status int

10. Най-важната защита — двойно записване
В ApplicationDbContext имаме:

modelBuilder.Entity<Enrollment>()
    .HasIndex(e => new { e.StudentId, e.CourseOfferingId })
    .IsUnique();

В базата:

IX_Enrollments_StudentId_CourseOfferingId
UNIQUE

Следователно:

Student 1 → CourseOffering 5   ✅
Student 1 → CourseOffering 6   ✅
Student 2 → CourseOffering 5   ✅
Student 1 → CourseOffering 5   ❌

Това е защита на database level, не разчитаме само на UI.

11. Delete поведението
В ApplicationDbContext имаме глобално:

foreach (var foreignKey in modelBuilder.Model
    .GetEntityTypes()
    .SelectMany(e => e.GetForeignKeys()))
{
    foreignKey.DeleteBehavior = DeleteBehavior.Restrict;
}

Така всички FK връзки са:

ON DELETE NO ACTION

Нямаме Cascade Delete.

Това е особено подходящо при нашия модел, защото използваме:

IsDeleted

за soft delete.

12. Капацитетът
Към момента:

CourseOffering
      │
      └── Capacity

А бизнес правилото, което уточнихме, е:

Pending       → не заема капацитет
Active        → заема капацитет
Cancelled     → не заема
Completed     → не заема
Failed        → не заема
NotAttended   → не заема

Тоест:

CurrentCapacity =
COUNT(Enrollment WHERE Status == Active)

Но още не сме написали тази логика, което е правилно — първо изясняваме архитектурата.

При онлайн курс по-късно можем да разширим начина, по който се определя капацитетът.

13. Жизнен цикъл на Enrollment
В момента концептуално:

                 ┌─────────────┐
                 │   Pending   │
                 └──────┬──────┘
                        │
                 Manager approves
                        │
                        ▼
                 ┌─────────────┐
                 │    Active   │
                 └──────┬──────┘
                        │
            ┌───────────┼───────────┐
            ▼           ▼           ▼
       Completed      Failed    NotAttended

И:

Pending → Cancelled

Може да има и:

Active → Cancelled

според бизнес правилата, които ще уточним.

14. Какво имаме реално в базата
Вече са приложени migrations за:

Areas
Students
StudyPrograms
Modules
Courses
CourseModule
CourseOfferings
Enrollments

И имаме:

__EFMigrationsHistory

която следи приложените migrations.

15. Архитектурният принцип, който следваме
Досега всъщност изграждаме нещата на няколко нива:

             USER / UI
                 │
                 ▼
        DataAnnotations
                 │
                 ▼
        Business Logic
                 │
                 ▼
          EF Core Model
                 │
                 ▼
            SQL Server

А за важните ограничения използваме повече от едно ниво.

Например:

EndDate >= StartDate

UI/Model
   +
IValidatableObject
   +
Database CHECK constraint

и:

Student + CourseOffering = unique

Business logic
   +
Database UNIQUE INDEX

Това е добра основа за V1, защото ако UI има грешка, базата пак има защита.

А V2
Не е нужно да го изграждаме сега, но архитектурата позволява по-късно около CourseOffering да добавим:

CourseOffering
│
├── DeliveryType
├── Schedule
├── Attendance
├── Assignments
├── Exams
├── Payments
└── Grades

без да разрушаваме основната връзка:

Student
   ↓
Enrollment
   ↓
CourseOffering
   ↓
Course

Това е състоянието на архитектурата ни в момента — V1 е сравнително проста, но имаме добра основа за V2.
