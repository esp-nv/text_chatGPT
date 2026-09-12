# C# / LINQ — Обобщение

| № | Тема | Какво да запомниш | Схема | Пример + резултат |
|---:|---|---|---|---|
| 1 | **Value type vs Reference type** | Value type копира стойността. Reference type копира референцията към обекта. | `Type a = value;`<br>`Type b = a;` | `int a = 10;`<br>`int b = a;`<br>`b = 20;`<br>**Резултат:** `a = 10`, `b = 20` |
| 2 | **ref** | Методът работи със същата променлива. Промяната вътре в метода се отразява на оригиналната променлива. | `void Method(ref Type value)`<br>`{`<br>&nbsp;&nbsp;`value = ...;`<br>`}`<br>`Method(ref variable);` | `void Change(ref int number)`<br>`{`<br>&nbsp;&nbsp;`number = 50;`<br>`}`<br><br>`int x = 10;`<br>`Change(ref x);`<br>`Console.WriteLine(x);`<br><br>**Резултат:** `50` |
| 3 | **out** | Методът трябва да присвои стойност на `out` параметъра. Подходящо е за връщане на допълнителен резултат. | `void Method(out Type value)`<br>`{`<br>&nbsp;&nbsp;`value = ...;`<br>`}`<br>`Method(out variable);` | `void GetNumber(out int number)`<br>`{`<br>&nbsp;&nbsp;`number = 50;`<br>`}`<br><br>`GetNumber(out int x);`<br>`Console.WriteLine(x);`<br><br>**Резултат:** `50` |
| 4 | **Наследяване** | Един клас наследява свойства и методи от друг клас. | `class Child : Parent`<br>`{ }` | `class Animal`<br>`{`<br>&nbsp;&nbsp;`public void Eat() => Console.WriteLine("Eating");`<br>`}`<br><br>`class Dog : Animal { }`<br><br>`Dog dog = new Dog();`<br>`dog.Eat();`<br><br>**Резултат:** `Eating` |
| 5 | **virtual + override** | `virtual` позволява методът да бъде променен в наследник. `override` го предефинира. | `class Parent`<br>`{`<br>&nbsp;&nbsp;`public virtual void Method() { }`<br>`}`<br><br>`class Child : Parent`<br>`{`<br>&nbsp;&nbsp;`public override void Method() { }`<br>`}` | `class Animal`<br>`{`<br>&nbsp;&nbsp;`public virtual void Speak() => Console.WriteLine("Animal");`<br>`}`<br><br>`class Dog : Animal`<br>`{`<br>&nbsp;&nbsp;`public override void Speak() => Console.WriteLine("Woof");`<br>`}`<br><br>`Animal animal = new Dog();`<br>`animal.Speak();`<br><br>**Резултат:** `Woof` |
| 6 | **abstract class** | Не може да се създаде директно обект от abstract class. Може да съдържа abstract методи. | `abstract class Parent`<br>`{`<br>&nbsp;&nbsp;`public abstract void Method();`<br>`}` | `abstract class Animal`<br>`{`<br>&nbsp;&nbsp;`public abstract void Speak();`<br>`}`<br><br>`class Dog : Animal`<br>`{`<br>&nbsp;&nbsp;`public override void Speak() => Console.WriteLine("Woof");`<br>`}`<br><br>`new Dog().Speak();`<br><br>**Резултат:** `Woof` |
| 7 | **Interface** | Interface е договор, който класът трябва да изпълни. | `interface IName`<br>`{`<br>&nbsp;&nbsp;`void Method();`<br>`}`<br><br>`class MyClass : IName`<br>`{ ... }` | `interface IAnimal`<br>`{`<br>&nbsp;&nbsp;`void Speak();`<br>`}`<br><br>`class Dog : IAnimal`<br>`{`<br>&nbsp;&nbsp;`public void Speak() => Console.WriteLine("Woof");`<br>`}`<br><br>**Резултат:** `Woof` |
| 8 | **Casting** | Позволява да използваме обект чрез друг съвместим тип. | `Parent obj = new Child();`<br>`Child child = (Child)obj;` | `Animal animal = new Dog();`<br>`Dog dog = (Dog)animal;`<br><br>`Console.WriteLine(dog.GetType().Name);`<br><br>**Резултат:** `Dog` |
| 9 | **is** | Проверява дали обектът е от даден тип. | `object is Type` | `Animal animal = new Dog();`<br><br>`Console.WriteLine(animal is Dog);`<br><br>**Резултат:** `True` |
| 10 | **var** | Компилаторът автоматично определя типа. Типът все пак е статичен. | `var variable = value;` | `var number = 10;`<br>`Console.WriteLine(number.GetType().Name);`<br><br>**Резултат:** `Int32` |
| 11 | **dynamic** | Типът се проверява по време на runtime. | `dynamic variable = value;` | `dynamic value = 10;`<br>`Console.WriteLine(value + 5);`<br><br>**Резултат:** `15` |
| 12 | **Access modifiers** | Контролират достъпа до класове, методи и полета. | `public`<br>`private`<br>`protected`<br>`internal` | `class Person`<br>`{`<br>&nbsp;&nbsp;`private string name = "Ivan";`<br>`}`<br><br>**Резултат:** `name` е достъпен само вътре в `Person`. |
| 13 | **Property** | Property контролира четенето и записването на стойност. | `public Type Name { get; set; }` | `class Person`<br>`{`<br>&nbsp;&nbsp;`public string Name { get; set; }`<br>`}`<br><br>`Person p = new Person();`<br>`p.Name = "Ivan";`<br>`Console.WriteLine(p.Name);`<br><br>**Резултат:** `Ivan` |
| 14 | **static** | Принадлежи на класа, а не на конкретна инстанция. | `static Type Name;`<br>`static void Method() { }` | `class Counter`<br>`{`<br>&nbsp;&nbsp;`public static int Count = 0;`<br>`}`<br><br>`Counter.Count++;`<br>`Console.WriteLine(Counter.Count);`<br><br>**Резултат:** `1` |
| 15 | **const** | Константата не може да бъде променяна след дефинирането си. | `const Type Name = value;` | `const int Max = 100;`<br>`Console.WriteLine(Max);`<br><br>**Резултат:** `100` |
| 16 | **Generics — List<T>** | Позволява създаване на колекции с конкретен тип. | `List<T> list = new List<T>();` | `List<int> numbers = new List<int> { 10, 20, 30 };`<br>`Console.WriteLine(numbers[0]);`<br><br>**Резултат:** `10` |
| 17 | **Generic constraint** | Ограничават какви типове могат да се използват като `T`. | `where T : class`<br>`where T : struct`<br>`where T : new()`<br>`where T : BaseClass` | `void Print<T>(T value) where T : class`<br>`{`<br>&nbsp;&nbsp;`Console.WriteLine(value);`<br>`}`<br><br>`Print("Hello");`<br><br>**Резултат:** `Hello` |
| 18 | **LINQ — основни методи** | LINQ позволява обработка на колекции чрез заявки. | `collection.Method(x => condition)` | `numbers.Where(n => n > 10)`<br><br>**Резултат:** елементите, които са `> 10` |
| 19 | **Where** | Филтрира елементите. | `collection.Where(x => condition)` | `List<int> numbers = new() { 5, 10, 15, 20 };`<br>`var result = numbers.Where(n => n > 10);`<br><br>**Резултат:** `15, 20` |
| 20 | **Select** | Избира/трансформира елементите. | `collection.Select(x => expression)` | `var names = people.Select(p => p.Name);`<br><br>**Резултат:** списък/sequence само с имената |
| 21 | **Any** | Проверява дали поне един елемент отговаря на условие. | `collection.Any(x => condition)` | `int[] numbers = { 5, 10, 20 };`<br>`numbers.Any(n => n > 15);`<br><br>**Резултат:** `True` |
| 22 | **All** | Проверява дали всички елементи отговарят на условие. | `collection.All(x => condition)` | `int[] numbers = { 10, 20, 30 };`<br>`numbers.All(n => n > 5);`<br><br>**Резултат:** `True` |
| 23 | **Count** | Връща броя на елементите. | `collection.Count()`<br>`collection.Count(x => condition)` | `int[] numbers = { 10, 20, 30, 40 };`<br>`numbers.Count();`<br><br>**Резултат:** `4` |
| 24 | **First** | Връща първия елемент. Ако няма такъв → exception. | `collection.First()`<br>`collection.First(x => condition)` | `int[] numbers = { 10, 20, 30 };`<br>`numbers.First();`<br><br>**Резултат:** `10` |
| 25 | **FirstOrDefault** | Връща първия елемент или `default`, ако няма такъв. | `collection.FirstOrDefault()` | `int[] numbers = { 10, 20, 30 };`<br>`numbers.FirstOrDefault(n => n > 100);`<br><br>**Резултат:** `0` |
| 26 | **Single** | Очаква точно един елемент. 0 или повече от 1 → exception. | `collection.Single(x => condition)` | `int[] numbers = { 10, 20, 30 };`<br>`numbers.Single(n => n == 20);`<br><br>**Резултат:** `20` |
| 27 | **Last / LastOrDefault** | Връщат последния елемент. | `collection.Last()`<br>`collection.LastOrDefault()` | `int[] numbers = { 10, 20, 30 };`<br>`numbers.Last();`<br><br>**Резултат:** `30` |
| 28 | **Sum / Average / Min / Max** | Изчисляват математически стойности. | `Sum()`<br>`Average()`<br>`Min()`<br>`Max()` | `int[] numbers = { 10, 20, 30 };`<br><br>`Sum()` → `60`<br>`Average()` → `20`<br>`Min()` → `10`<br>`Max()` → `30` |
| 29 | **Contains** | Проверява дали колекцията съдържа дадена стойност. | `collection.Contains(value)` | `int[] numbers = { 10, 20, 30 };`<br>`numbers.Contains(20);`<br><br>**Резултат:** `True` |
| 30 | **IndexOf** | Връща индекса на даден елемент. | `list.IndexOf(value)` | `List<int> numbers = new() { 10, 20, 30 };`<br>`numbers.IndexOf(20);`<br><br>**Резултат:** `1` |
| 31 | **GroupBy** | Групира елементите по даден ключ. | `collection.GroupBy(x => key)` | `people.GroupBy(p => p.City);`<br><br>**Резултат:** групи от хора по `City` |
| 32 | **OrderBy + ThenBy** | Сортира по един или повече критерия. | `.OrderBy(x => key)`<br>`.ThenBy(x => key)` | `people.OrderBy(p => p.City).ThenBy(p => p.Name);`<br><br>**Резултат:** първо по град, после по име |
| 33 | **Skip + Take** | `Skip` пропуска N елемента. `Take` взема N елемента. | `.Skip(n)`<br>`.Take(n)` | `int[] numbers = { 10, 20, 30, 40, 50 };`<br>`numbers.Skip(2).Take(2);`<br><br>**Резултат:** `30, 40` |
| 34 | **Distinct** | Премахва дублиращите се стойности. | `collection.Distinct()` | `int[] numbers = { 10, 20, 20, 30, 30 };`<br>`numbers.Distinct();`<br><br>**Резултат:** `10, 20, 30` |
| 35 | **IEnumerable<T>** | Представлява последователност от елементи, която може да бъде обхождана. | `IEnumerable<T> result = collection;` | `IEnumerable<int> numbers = new[] { 10, 20, 30 };`<br><br>**Резултат:** sequence от `10, 20, 30` |
| 36 | **Deferred execution** | LINQ заявката не се изпълнява задължително веднага. | `var result = collection.Where(...);` | `var result = numbers.Where(n => n > 10);`<br><br>`numbers.Add(20);`<br>`foreach (var n in result)`<br><br>**Резултат:** заявката се изпълнява при обхождането |
| 37 | **ToList()** | Изпълнява заявката и създава `List<T>`. | `collection.Where(...).ToList()` | `var result = numbers.Where(n => n > 10).ToList();`<br><br>**Резултат:** реален `List<int>` |
| 38 | **null / ?. / ?? / ??=** | Позволяват безопасна работа с `null`. | `obj?.Property`<br>`value ?? defaultValue`<br>`value ??= defaultValue` | `string name = null;`<br>`Console.WriteLine(name ?? "Unknown");`<br><br>**Резултат:** `Unknown` |
| 39 | **Nullable int?** | Позволява value type да има `null`. | `int? variable = null;` | `int? age = null;`<br>`Console.WriteLine(age.HasValue);`<br><br>**Резултат:** `False` |
| 40 | **default** | Връща default стойността за даден тип. | `default(Type)`<br>`default` | `int x = default;`<br>`Console.WriteLine(x);`<br><br>**Резултат:** `0` |
| 41 | **ElementAt / ElementAtOrDefault** | Връщат елемент на даден индекс. | `collection.ElementAt(index)`<br>`collection.ElementAtOrDefault(index)` | `int[] numbers = { 10, 20, 30 };`<br>`numbers.ElementAt(1);`<br><br>**Резултат:** `20` |
| 42 | **Reverse** | Обръща реда на елементите. | `collection.Reverse()` | `int[] numbers = { 10, 20, 30 };`<br>`numbers.Reverse();`<br><br>**Резултат:** `30, 20, 10` |
| 43 | **Clear** | Премахва всички елементи от колекцията. | `list.Clear()` | `List<int> numbers = new() { 10, 20, 30 };`<br>`numbers.Clear();`<br><br>**Резултат:** `[]` |
| 44 | **Remove vs RemoveAt** | `Remove` премахва по стойност. `RemoveAt` премахва по индекс. | `list.Remove(value)`<br>`list.RemoveAt(index)` | `List<int> numbers = new() { 10, 20, 30 };`<br>`numbers.Remove(20);`<br><br>**Резултат:** `10, 30` |
| 45 | **Dictionary<TKey,TValue>** | Съхранява двойки `Key → Value`. | `Dictionary<TKey, TValue> dict = new();`<br>`dict[key] = value;` | `Dictionary<int, string> people = new();`<br>`people[1] = "Ivan";`<br>`Console.WriteLine(people[1]);`<br><br>**Резултат:** `Ivan` |
| 46 | **ContainsKey** | Проверява дали даден ключ съществува в Dictionary. | `dictionary.ContainsKey(key)` | `Dictionary<int, string> people = new();`<br>`people[1] = "Ivan";`<br>`people.ContainsKey(1);`<br><br>**Резултат:** `True` |
| 47 | **ContainsValue** | Проверява дали дадена стойност съществува. | `dictionary.ContainsValue(value)` | `people.ContainsValue("Ivan");`<br><br>**Резултат:** `True` |
| 48 | **TryGetValue** | Опитва да намери стойност по ключ без exception. | `dictionary.TryGetValue(key, out value)` | `if (people.TryGetValue(1, out string name))`<br>`{`<br>&nbsp;&nbsp;`Console.WriteLine(name);`<br>`}`<br><br>**Резултат:** `Ivan` |

---

## LINQ — най-важното

| Метод | Схема | Какво прави | Пример | Резултат |
|---|---|---|---|---|
| `Where` | `collection.Where(x => condition)` | Филтрира | `numbers.Where(n => n > 10)` | `15, 20` |
| `Select` | `collection.Select(x => expression)` | Избира/трансформира | `people.Select(p => p.Name)` | `Ivan, Maria` |
| `OrderBy` | `collection.OrderBy(x => key)` | Сортира възходящо | `numbers.OrderBy(n => n)` | `10, 20, 30` |
| `OrderByDescending` | `collection.OrderByDescending(x => key)` | Сортира низходящо | `numbers.OrderByDescending(n => n)` | `30, 20, 10` |
| `ThenBy` | `.ThenBy(x => key)` | Вторично сортиране | `.OrderBy(p => p.City).ThenBy(p => p.Name)` | City → Name |
| `First` | `collection.First()` | Първи елемент | `numbers.First()` | `10` |
| `FirstOrDefault` | `collection.FirstOrDefault()` | Първи или `default` | `numbers.FirstOrDefault(n => n > 100)` | `0` |
| `Last` | `collection.Last()` | Последен елемент | `numbers.Last()` | `30` |
| `LastOrDefault` | `collection.LastOrDefault()` | Последен или `default` | `numbers.LastOrDefault(n => n > 100)` | `0` |
| `Single` | `collection.Single(x => condition)` | Точно един елемент | `numbers.Single(n => n == 20)` | `20` |
| `SingleOrDefault` | `collection.SingleOrDefault(x => condition)` | 0 или 1 елемент | `numbers.SingleOrDefault(n => n == 100)` | `0` |
| `Any` | `collection.Any(x => condition)` | Има ли поне един? | `numbers.Any(n => n > 20)` | `True` |
| `All` | `collection.All(x => condition)` | Всички ли отговарят? | `numbers.All(n => n > 5)` | `True` |
| `Count` | `collection.Count()` | Колко са? | `numbers.Count()` | `3` |
| `Sum` | `collection.Sum()` | Сума | `numbers.Sum()` | `60` |
| `Average` | `collection.Average()` | Средно | `numbers.Average()` | `20` |
| `Min` | `collection.Min()` | Минимум | `numbers.Min()` | `10` |
| `Max` | `collection.Max()` | Максимум | `numbers.Max()` | `30` |
| `Contains` | `collection.Contains(value)` | Има ли стойността? | `numbers.Contains(20)` | `True` |
| `GroupBy` | `collection.GroupBy(x => key)` | Групира | `people.GroupBy(p => p.City)` | Групи по City |
| `Distinct` | `collection.Distinct()` | Премахва дубликати | `{10,20,20}.Distinct()` | `10,20` |
| `Skip` | `collection.Skip(n)` | Пропуска N | `numbers.Skip(2)` | `30,40,50` |
| `Take` | `collection.Take(n)` | Взема N | `numbers.Take(2)` | `10,20` |
| `ElementAt` | `collection.ElementAt(index)` | Взема по индекс | `numbers.ElementAt(1)` | `20` |
| `ToList` | `collection.ToList()` | Материализира като List | `numbers.Where(...).ToList()` | `List<T>` |

---

## Бърза шпора

| Ако искаш да... | Използвай | Схема |
|---|---|---|
| Филтрираш | `Where` | `.Where(x => condition)` |
| Избереш поле | `Select` | `.Select(x => x.Property)` |
| Сортираш | `OrderBy` | `.OrderBy(x => x.Property)` |
| Сортираш обратно | `OrderByDescending` | `.OrderByDescending(x => x.Property)` |
| Второ сортиране | `ThenBy` | `.ThenBy(x => x.Property)` |
| Вземеш първия | `First` | `.First()` |
| Вземеш първия или default | `FirstOrDefault` | `.FirstOrDefault()` |
| Вземеш последния | `Last` | `.Last()` |
| Вземеш точно един | `Single` | `.Single(x => condition)` |
| Провериш дали има поне един | `Any` | `.Any(x => condition)` |
| Провериш дали всички | `All` | `.All(x => condition)` |
| Преброиш | `Count` | `.Count()` |
| Сумираш | `Sum` | `.Sum()` |
| Намериш средно | `Average` | `.Average()` |
| Намериш минимум | `Min` | `.Min()` |
| Намериш максимум | `Max` | `.Max()` |
| Провериш стойност | `Contains` | `.Contains(value)` |
| Групираш | `GroupBy` | `.GroupBy(x => key)` |
| Махнеш дубликати | `Distinct` | `.Distinct()` |
| Пропуснеш N | `Skip` | `.Skip(n)` |
| Вземеш N | `Take` | `.Take(n)` |
| Вземеш по индекс | `ElementAt` | `.ElementAt(index)` |
| Направиш List | `ToList` | `.ToList()` |
| Работиш с null | `?.` | `obj?.Property` |
| Default при null | `??` | `value ?? defaultValue` |
| Зададеш default при null | `??=` | `value ??= defaultValue` |
| Работиш с Key → Value | `Dictionary` | `Dictionary<TKey,TValue>` |
| Провериш ключ | `ContainsKey` | `dict.ContainsKey(key)` |
| Вземеш безопасно стойност | `TryGetValue` | `dict.TryGetValue(key, out value)` |
