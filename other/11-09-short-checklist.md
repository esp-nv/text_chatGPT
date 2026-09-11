````text
може ли съкратения списък

ChatGPT said:
Разбира се. Ето съкратения списък дотук, без подробните обяснения — само като бърза шпаргалка за това, което минахме. 👇

C# — съкратен checklist
Типове и променливи
value type → копира се стойността.
reference type → променливата държи референция към обект.
var → C# извежда типа от израза вдясно от =.
const → стойността не може да се променя.
static → принадлежи на класа, не на конкретен обект.
public → достъп отвсякъде според контекста.
private → достъп само в класа.
protected → класът + наследниците.
ref → подава съществуваща променлива по референция.
out → методът трябва да върне стойност чрез параметъра; използва се например при TryParse, TryGetValue.
OOP
Animal → базов клас.
Dog : Animal → Dog наследява Animal.
virtual → позволява на наследника да промени/override-не поведението.
abstract class → не се създава директно; може да има abstract методи, които наследникът трябва да реализира.
interface → договор какво трябва да предоставя класът.
Casting → интересува ни реалният тип на обекта.
is → проверява дали обектът е от даден тип.
Properties
field → самата променлива/стойност
property → контролира достъпа до нея

get → четене.
set → задаване.
private set → отвън може да се чете, но не и директно да се променя.
Generics
List<T>

→ T е типът на елементите.

List<int>    → само int
List<string> → само string

where T : class

→ constraint: ограничение какъв тип може да бъде T.

LINQ — най-важното
Where       → КОИ да останат?
Select      → КАКВО да получа?
OrderBy     → КАК да ги подредя?
ThenBy      → допълнително сортиране при равенство
First       → ДАЙ първия
FirstOrDefault → ДАЙ първия или default
Last        → ДАЙ последния
LastOrDefault → ДАЙ последния или default
Single      → трябва да има ТОЧНО един
SingleOrDefault → 0 или 1, но не повече от един
Any         → ИМА ЛИ поне един?
All         → ВСИЧКИ ЛИ отговарят?
Count       → КОЛКО?
Sum         → СУМАТА
Average     → СРЕДНОТО
Min         → НАЙ-МАЛКАТА
Max         → НАЙ-ГОЛЯМАТА
Contains    → ИМА ЛИ тази стойност?
IndexOf     → КЪДЕ е първото ѝ срещане?
GroupBy     → ГРУПИРАЙ по...
Distinct    → ПРЕМАХНИ повторенията
Skip        → ПРОПУСНИ първите N
Take        → ВЗЕМИ първите N
ElementAt   → елементът на даден индекс
ElementAtOrDefault → елементът или default

LINQ и IEnumerable
IEnumerable<T>
→ нещо, което може да се обхожда едно по едно

List<T> може да бъде IEnumerable<T>.
IEnumerable<T> е по-общ/ограничен тип от List<T>.
List<T> има допълнителни възможности като Add, Remove, индексатор и др.
Deferred execution
var result = numbers.Where(n => n > 15);

→ заявката обикновено се изпълнява при обхождане.

var result = numbers.Where(n => n > 15).ToList();

→ изпълнява се сега и се създава реален List<T>.

Where(...)          → sequence
Where(...).ToList() → List<T>

null
?. → ако обектът не е null, продължи
?? → ако е null, използвай другата стойност
??= → ако е null, присвои другата стойност

Пример:

person?.Name ?? "Unknown"

→ ако person/Name липсва → "Unknown".

Nullable
int?

→ int, който може да бъде и null.

age.HasValue → има ли стойност?
age.Value    → вземи стойността

default
int     → 0
bool    → false
string  → null
class   → null

Collections
Dictionary:

Dictionary<TKey, TValue>

Key → ключ
Value → стойност

ContainsKey → ИМА ЛИ този ключ?
ContainsValue → ИМА ЛИ тази стойност?
TryGetValue → намери стойността по ключ → true/false + out

List:

Add       → добави
Remove    → премахни по стойност
RemoveAt  → премахни по индекс
Clear     → изчисти всички елементи
Count     → брой елементи
list[i]   → елемент на индекс i

Skip + Take
numbers.Skip(2).Take(2)

→ пропусни първите 2 → вземи следващите 2.

Reverse
List.Reverse()

→ променя самия List.

LINQ Reverse() → връща обърната sequence.

Това е съкратеният checkpoint дотук. След почивката можем директно да продължим с въпросите от следващата тема. ☕
