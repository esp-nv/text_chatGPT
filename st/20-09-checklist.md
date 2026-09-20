````text
бих разделил проекта на V1 = работеща основа за реално записване и V2 = разширяване на учебната структура.

Това е важно, защото иначе рискуваме още сега да построим прекалено сложна система.

V1 — това бих направил сега
Целта на V1:

Да мога да създам курсове, да ги организирам в основна структура и да записвам един студент за конкретно обучение, включително за курсове от различни области.

1. Student
Оставяме съществуващия Student.

Student
---------
Id
FirstName
LastName
Email
Age
DateOfBirth
...

Тук махаме старото:

Course

като string.

Вместо него връзката ще бъде през Enrollment.

2. Area
Бих добавил още във V1:

Area
---------
Id
Code
Name
Description

Примери:

LANG
IT
DESIGN
BUSINESS

Причината е, че ти изрично искаш системата да не бъде само за програмиране.

3. Program
Program
---------
Id
AreaId
Code
Name
Description

Например:

LANG → ENGLISH
IT → CSHARP
DESIGN → GRAPHIC-DESIGN

4. Course
Course
---------
Id
ProgramId
Code
Name
Description

Например:

ENGLISH
 ├── A1
 ├── A2
 ├── B1
 └── B2

или:

CSHARP
 ├── FUND
 ├── ADV
 └── OOP

Тук Code е само кодът на курса.

Не съдържа година, месец или отстъпка.

5. CourseOffering
Това според мен също трябва да е във V1.

CourseOffering
----------------
Id
CourseId
Year
Month
Status

Например:

C# OOP
2027
09
Open

Това е конкретното обучение, в което студентът може да се запише.

6. Enrollment
Това е най-важната таблица за твоята идея.

Enrollment
----------------
Id
StudentId
CourseOfferingId
Status
EnrollmentDate
DiscountPercent

Всеки запис е:

един студент + едно конкретно обучение.

Например:

#101 Иван → C# Fundamentals → Active
#102 Иван → C# OOP         → Active
#103 Иван → English A2     → Active

Точно както поиска.

А checkbox-ите?
Да, във V1.

Например:

C# Development

☑ Fundamentals
☑ Advanced
☐ OOP

Save създава:

Enrollment #101 → Fundamentals
Enrollment #102 → Advanced

А ако студентът избере:

English
☑ A2
☐ B1

се създава отделен:

Enrollment #103 → English A2

Така студентът може едновременно да учи:

IT
 ├── C# Fundamentals
 └── C# Advanced

Languages
 └── English A2

Какво бих оставил за V2
Тук бих преместил неща, които не са необходими, за да заработи основният процес.

V2 — Module
Program
   ↓
Module
   ↓
Course

Причината е, че първоначално можем да имаме:

C# Development
 ├── FUND
 ├── ADV
 └── OOP

без Module.

Когато видим реалната нужда от:

C# Development
 ├── Fundamentals
 │    ├── C# Basics
 │    └── OOP
 │
 └── Advanced
      ├── LINQ
      └── ASP.NET

добавяме Module.

V2 — сложна система за Discount
За V1:

DiscountPercent
0–100

е напълно достатъчно.

Във V2 можем да направим:

Discount
---------
Id
Name
Percent
ValidFrom
ValidTo

и например:

Early Bird
Student Discount
Group Discount
Special Promotion

V2 — Program Enrollment
В началото не бих създавал отделно:

ProgramEnrollment

Защото основната единица е:

Student → CourseOffering

А checkbox-ите могат да изберат всички курсове от дадена програма.

По-късно, ако се окаже, че трябва да следим:

„Иван е официално записан в програмата C# Development“

тогава добавяме:

ProgramEnrollment

и можем да следим прогреса му по програмата.

V2 — prerequisites
Например:

A1 → A2 → B1 → B2

или:

C# Fundamentals → C# Advanced → C# OOP

Това може да стане чрез:

CoursePrerequisite

Но не бих го правил във V1.

V2 — оценки, посещаемост и сертификати
Следващ слой:

Enrollment
   ├── Attendance
   ├── Grade
   ├── Exam
   └── Certificate

Това вече е друга функционална област.

Така бих разделил версиите
| Функционалност                   | V1  | V2  |
| :------------------------------- | :-- | :-- |
| Student                          | ✅  |     |
| Area                             | ✅  |     |
| Program                          |✅   |     |
| Course                           | ✅  |     |
| CourseOffering                   | ✅  |     |
| Enrollment                       | ✅   |     |
| ‡аписване в различни области     | ✅   |     |
| Checkbox за избор на курсове     | ✅  |     |
| Ћтделен Enrollment за всеки курс | ✅   |     |
| Year / Month                     | ✅  |     |
| Basic Discount %                 | ✅   |     |
| Module                           |     | ✅  |
| ProgramEnrollment                |     | ✅  |
| ‘ложни Discount правила          |     | ✅  |
| Prerequisites                    |     | ✅  |
| Attendance                       |     | ✅  |
| Grades/Exams                     |     | ✅  |
| Certificates                     |     | ✅   |


А специалният код?
Тук бих бил малко по-предпазлив.

V1 бих запазил истинските данни отделно, например:

Enrollment
StudentId
CourseOfferingId
DiscountPercent

и бих могъл да генерирам display/reference код:

ENGLISH|A2-2027-09-0
CSHARP|OOP-2027-09-10

Но не бих направил този string основен ключ на базата.

Така ако във V2 променим формата:

ENGLISH-A2-2027-09

няма да трябва да мигрираме цялата база.

И най-важното
Това означава, че първоначалният ни checklist трябва леко да се преработи.

Първоначално говорехме за:

Student ↔ Course

Но след днешното уточняване по-правилната V1 концепция е:

Student
   │
   ▼
Enrollment
   │
   ▼
CourseOffering
   │
   ▼
Course
   │
   ▼
Program
   │
   ▼
Area

Това е съществена архитектурна промяна.

Аз бих направил точно това преди да започнем кодирането: да преработим checklist-а за V1 така, че да отразява тази вече уточнена архитектура. После пак работим една стъпка наведнъж, както поиска.



Вие казахте:

специалният код това беше само предложение заради остъпката

ChatGPT каза:
Точно — тогава махаме специалния код от архитектурата. Беше пример как да се представи информацията, а не изискване към системата.

И това всъщност опростява V1 доста.

V1 бих го оставил така
Area
  ↓
Program
  ↓
Course
  ↓
CourseOffering
  ↓
Enrollment
  ↑
Student

Course
Съдържа само информацията за самия курс:

Course
----------------
Id
ProgramId
Code
Name
Description

Примери:

ENGLISH → A1
ENGLISH → A2
ENGLISH → B1

CSHARP → FUND
CSHARP → ADV
CSHARP → OOP

CourseOffering
Тук вече е конкретното провеждане:

CourseOffering
----------------
Id
CourseId
Year
Month
Status

Например:

English A2
September 2027
Open

Enrollment
Тук е конкретното записване:

Enrollment
----------------
Id
StudentId
CourseOfferingId
EnrollmentDate
Status
DiscountPercent

Например:

Иван → English A2 → 10%
Иван → C# OOP    → 0%

Това е много по-чисто.

А отстъпката
Ако на този етап условието е просто:

„Студентът може да получи отстъпка между 0 и 100%“

тогава:

public int DiscountPercent { get; set; }

в Enrollment е достатъчно.

Защото отстъпката може да е различна за различните записвания на един и същ студент.

Например:

Иван
│
├── English A2 → 10%
├── English B1 → 0%
└── C# OOP    → 20%

Това е важна причина да не я слагаме в Course.

И специалният код отпада
Няма нужда от:

CSHARP|FUND|ADV-2027-09-10

като част от модела.

Ако някой ден искаме reference number за Enrollment, можем да добавим отделно:

EnrollmentNumber

например:

ENR-000123

но това е съвсем различно от структурата на курсовете.

Така според мен вече имаме достатъчно ясна V1 концепция.

Следващата ни стъпка нека бъде да преработим checklist-а само за V1,
като извадим нещата, които остават за V2. След това се връщаме към кода
и продължаваме буквално по една стъпка, без да прескачаме.
