Высокоуровневые методы информатики и программирования.
Практическая работа 05: LINQ to DataSet
Цель работы ‒ изучение языка запросов LINQ
ПЛАН
Оглавление
1. Краткое введение ... ................................................................................................................................ 1
2. Практическое задание............................................................................................................................. 1
2.1. Постановка задачи............................................................................................................................. 1
2.2. Запросы LINQ to DataSet .................................................................................................................. 1
2.3. Выгрузка данных............................................................................................................................... 2
3. Указания.................. ................................................................................................................................ 2
1. Краткое введение
Довольно подробная информация с примерами есть здесь:
https://metanit.com/sharp/tutorial/15.1.php
По работе с текстовыми данными:
https://metanit.com/sharp/tutorial/7.1.php
По работе с объектами даты:
https://metanit.com/sharp/tutorial/19.1.php
2. Практическое задание
2.1. Постановка задачи
Создайте базу данных Access с одной таблицей о сотрудниках. Хранимые данные: имя,
должность, дата рождения, оклад. Заполните таблицу 8-10 записей.
В приложении на основе Windows Forms присоедините табличку базы данных. В приложении появятся объекты доступа к БД.
Для визуализации источника на форме разместите dataGrid, привяжите к таблице
(свойство DataSource). Запустите приложение и убедитесь, что набор данных отображается.
Разработайте интерфейс для выполнения различных операций запросов с визуализацией решений. Для выборок рекомендуется использовать второй dataGrid. Чтобы выводить
выборки, можно написать метод формы View(выборка). Для задания условий отбора, которые можно выбрать из известного списка, например, по должности, используйте
listBox’ы, отражающие возможные значения (свойство DataSource). Для ввода данных и
вывода, где необходимо, текстовые поля.
2.2. Запросы LINQ to DataSet
Найдите через Linq запросы:
• средний оклад по конторе;
• сотрудника по имени;
• сотрудников по должности;
• сотрудников пенсионного возраста;
• сотрудников, чей оклад выше среднего по конторе;
• сотрудников моложе 30-ти лет на указанной должности.
Используйте LINQ to DataSet, чтобы:
• сортировать список по фамилии;
• сортировать список по убыванию оклада;
• группировать список по должностям.
• найти средний оклад по должностям.
2.3. Выгрузка данных
Используйте LINQ to DataSet, чтобы сформировать справку об окладах в виде: фамилия – оклад с сортировкой по убыванию.
3. Указания
1. Получение доступа к таблице
Для доступа к таблице БД в классе формы опишите объект типа DataTable:
DataTable myTable;
На Form1_Load выполняется автоматически заполнение адаптера:
// TODO: данная строка кода позволяет загрузить данные в таблицу
"for_LINQ_2003DataSet.Работники".
this.работникиTableAdapter.Fill(this.for_LINQ_2003DataSet.Работники);
После чего присвойте переменной значение таблицы. Она одна, находится в наборе
данных for_LINQ_2003DataSet , а номер в коллекции = 0:
myTable = for_LINQ_2003DataSet.Tables[0];
2. Вывод выборки в dataGridView
Вывод выборки имеет особенности, связанные с типизацией. Данные выборки имеют
тип DataRow, обращение так:
IEnumerable <DataRow> myQuery = ...
а строки в dataGridView имеют тип DataRowView. Для визуализации решения в гриде
можно использовать прямое обращение к полям записи типа DataRow с формированием
строки на лету, например, если выборка имеет имя myQuery, то:
foreach (DataRow tmp in myQuery)
{
 dataGridView2.Rows.Add (tmp.Field<int>("Код"),
 tmp.Field<string>("Имя"),
 tmp.Field<int>("Оклад"),
 tmp.Field<string>("Должность"));
}
Строка выборки tmp имеет поля Field, извлекаемые по названию (такое же, как в таблице базы данных), например: tmp.Field<string>("Имя") извлекает поле «Имя».
