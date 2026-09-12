````text
Чеклист — какво остава
🟢 LINQ — основата е покрита
 Where
 Select
 OrderBy / OrderByDescending
 Take / Skip
 First / FirstOrDefault
 Last / LastOrDefault
 Single / SingleOrDefault
 Any / All
 Count
 Sum / Average
 Min / Max
 Distinct
 Reverse
 Concat
 ToList
 LINQ верига и ред на изпълнение
 &&, ||, % и сложни условия
 условие с думи → сама да напишеш LINQ
 GroupBy
 SelectMany
 Join — ако е част от материала ти
 по-сложни комбинации на горните
Тук утре бихме продължили точно от това, което започнахме:
условие → логика → LINQ, без входни данни.

🟡 След LINQ — речници
Това според мен е естествената следваща стъпка.

Dictionary<TKey, TValue>
 какво е key и value
 създаване
 добавяне
 достъп по key
 промяна на value
 ContainsKey
 TryGetValue
 Remove
 Count
 Keys
 Values
 foreach през dictionary
 разлика между KeyValuePair и само value
 какво става при несъществуващ key
 LINQ върху dictionary
И точно както каза по-рано — ако нещо не си учила, казваш ми и първо ти давам основното със схеми и примери.

🟡 След речниците
След това бих подредил нещата така:

Dictionary
HashSet
List / Array / Dictionary / HashSet — кога кое използвам
по-сложен LINQ върху колекции
lambda expressions — по-сложни случаи
C# OOP
класове
обекти
constructors
properties
encapsulation
inheritance
polymorphism
interfaces
abstract classes
exceptions
generics
delegates / Func / Action — ако са в материала ти
async/await — ако е част от подготовката ти
интервю задачи — смесени, без да ти казвам кой метод трябва да използваш
🎯 А утре?
Не бих започнал с нов материал веднага.

Бих започнал с:

LINQ: „Условие → напиши LINQ“
Първо лесни:

условие
→ логика
→ LINQ

После:

сложно условие
→ && / ||
→ Where / Select
→ LINQ

И накрая подвеждащи интервю задачи, където няма да ти казвам:

„Тук използвай Where.“

Ти сама ще трябва да разпознаеш:

„Това е филтриране → Where.“
„Това е преобразуване → Select.“

След като това стане стабилно, преминаваме към Dictionary.

Така няма да учим хаотично метод след метод, а ще изграждаме умението „получавам задача → разбирам какво се иска → избирам правилния инструмент“. Това е много по-близо до реалното програмиране и интервю.



