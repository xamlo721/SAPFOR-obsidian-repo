_Sage++_ это объектно-ориентированный набор инструментов для создания программных преобразований и инструментов предварительной сборки. Он содержит парсеры для Fortran 77 со многими расширениями Fortran 90, C и C++, интегрированные с библиотекой классов C++. Библиотека предоставляет средства для доступа и реструктуризации дерева программы, таблиц символов и типов, а также аннотаций программиста на уровне исходного кода. Sage++ предоставляет базовую инфраструктуру, на которой могут быть построены все типы программных препроцессоров, включая распараллеливающие компиляторы, инструменты анализа производительности и оптимизаторы исходного кода.

#### 1. Введение 
Проектирование и создание системы перевода исходного кода в исходный код — очень трудоемкая задача. Однако такие системы часто являются предпосылкой для многих исследовательских проектов по компиляторам и расширениям языка. Sage++ был разработан как инструментарий для таких проектов. Он предоставляет интегрированный набор парсеров, которые преобразуют исходную программу во внутреннее представление, которое мы называем программным деревом; библиотеку объектно-ориентированных методов, которые манипулируют программным деревом и предоставляют разработчикам инструментов полную свободу в его реструктуризации; и депарсер, который генерирует новый исходный код из реструктурированной внутренней формы.

Такие системы трансляции используются, например, в исследованиях языковых расширений, которые допускают явное представление параллелизма, где они необходимы для построения компиляторов, которые генерируют целевой специфичный исходный код, содержащий вызовы к системам времени выполнения, которые поддерживают параллелизм. Примерами являются компиляторы Fortran-D и Fortran 90D \[1\] и компилятор pC++ \[5\]. Системы трансляции исходного кода также используются для построения компиляторов, которые решают проблему обнаружения параллелизма в последовательном исходном коде. Эти компиляторы применяют преобразования реструктуризации для генерации версии программы, которая использует директивы или явные параллельные конструкции, понимаемые «родным» компилятором на параллельной машине. Примерами этого являются компиляторы для Parafrase и Parafrase-II \[6\] и Superb \[2\]. Sage++ также позволяет строить оптимизации, специфичные для библиотеки, которые могут быть добавлены в качестве переносимого этапа предварительной обработки к компилятору C++.

Часто называемые препроцессорами, поскольку они не генерируют машинный код, все эти системы используют обширный синтаксический и семантический анализ и сложную глобальную оптимизацию для преобразования исходного кода. В каждом случае эти системы были основаны на слое технологии компилятора, на разработку которого каждой исследовательской группе потребовались годы. Sage++ делает этот слой доступным в обобщенной форме. Начиная с Sage++, а не с нуля, исследователи в этих областях могут потенциально сократить годы своего времени разработки.

Второй мотивацией для выпуска Sage++ является ответ на частые запросы программистов на доступ к инструментам, которые позволяют им выходить за рамки простых макросов и создавать расширения для C++ или Fortran.
#### 2. Sage++ как Мета - Инструмент
Sage++ разработан как инструмент, с помощью которого можно создавать другие инструменты. Например, разработчики научных библиотек могут использовать Sage++ для создания инструментов, способных оптимизировать исходный код, который связывается с библиотекой. В качестве иллюстрации рассмотрим проблему оптимизации использования пакета библиотеки C++ Matrix, похожего на Lapack++ \[4\]. Библиотека состоит из классов C++ для векторов и матриц со специальным механизмом для описания подмассивов и подвекторов, и где стандартные арифметические операторы были перегружены:

```cpp
class GenMat;

class Vector{ 

	public:

		Vector(int n){};
		
		Vector & operator =(Vector &); Vector & operator +(Vector &);
		
		friend Vector &operator *(float x, Vector &v);
		
		void vecVecAdd(Vector &left, Vector &right); // this = left*right void matVecMul(GenMat &M, Vector &x); // this = M*x
		
		void scalarVecMul(float x, Vector &v); // this = x*v

};

class GenMat{ // general matrix public:

	GenMat(int i, int j);
	
	GenMat & operator()( int , int );
	
	GenMat & operator()( index &, index &); 
	
	GenMat & operator =(GenMat &);
	
	Vector & operator *(Vector &);

};
```

Распространенной проблемой таких алгебраических приложений C++ является управление высокой стоимостью создания временных объектов и копий в выражениях типа:
```cpp
GenMat M(100,100);

Vector w(100), x(100), y(100), z(100);

z = x+ M*(x+3.2*y + w); 

x = z+w;

y = z+x;
```

Собственный компилятор выделит временные объекты для каждой из операций (в данном случае восемь). Кроме того, операции присваивания могут создавать ненужные копии данных (в данном случае три). Приведенный выше фрагмент кода можно написать для более эффективного использования временных объектов; следует использовать функции-члены, которые принимают два аргумента. Например, выражение x = z+w можно записать как x.vecVecAdd(z,w). Кроме того, поскольку сложение векторов не несет никаких зависимостей, нам не нужно беспокоиться о возможных псевдонимах, и выражения типа x = z+x можно переписать как x.vecVecAdd(z,x). Однако это не относится к умножению матриц и векторов. В этом случае, если x.matVecMul(M,z) записать как:
```cpp
for (i = 0; i < size; i++) {

	x[i] = 0.0;

	for (j = 0; j < size; j++)
	
		x[i] += M(i,j)*z(j);

}
```

тогда мы не можем позволить x и z быть псевдонимами, и необходимо сгенерировать временный.

Принимая во внимание эти наблюдения о псевдонимах, легко написать препроцессор Sage++, который преобразует первый набор выражений выше в код ниже.

```cpp
GenMat M(100,100);

Vector w(100),x(100),y(100),z(100);

Vector _T0(100); 
z.scalarVecMul(3.2,y); 
z.vecVecAdd(x,z); 
z.vecVecAdd(z,w);

_T0.matVecMul(M,z);

z.vecVecAdd(x,_T0); 
x.vecVecAdd(z,w); 
y.vecVecAdd(z,x);
```

Такой препроцессор будет сканировать исходный код в поисках выражений, включающих классы Vector или GenMat. Стратегия, которую может использовать препроцессор, заключается в использовании левой части каждого назначения в качестве свободного временного значения, пока оно не используется в правой части назначения. Обратите внимание, что одно временное значение \_T0 было сгенерировано из-за проблемы с псевдонимом с matVecMul. Более агрессивная оптимизация могла бы обнаружить, что вместо этого можно использовать y, поскольку оно переопределяется позже.

Совсем другое применение Sage++ заключается в создании инструмента для автоматического инструментирования пользовательского кода. Группа в Университете Орегона использовала Sage++ для автоматического добавления инструментирования для отслеживания вызовов функций-членов класса \[9\]. Они используют Sage++ для добавления объекта инструментирования к определению каждой функции-члена, которую нужно отслеживать. Когда программа запущена, вызов любого из инструментированных методов вызывает конструктор объекта инструментирования, который может регистрировать вызов метода. При выходе из метода деструктор объекта инструментирования также может регистрировать это событие.

Еще одно применение Sage++ — создание препроцессоров для программ на языке Fortran. Лучшим примером является система Fortran-S \[3\], разработанная в Университете Ренна. Эта система опирается на аннотации уровня пользователя, встроенные в комментарии, которые извлекаются Sage++, и вызывают преобразования, такие как векторизация циклов, блокировка и взаимообмен, которые все кодируются с помощью Sage++.

Sage++ также используется в проекте Argonne National Laboratory для выполнения автоматической дифференциации численных алгоритмов, написанных на языке C. Автоматическая дифференциация — это процесс дополнения функций в исходном коде для получения производных значений в дополнение к исходным выходным данным функции \[10\].

![](file:///C:\Users\Satomi\AppData\Local\Temp\ksohtml65480\wps1.jpg) 

Рисунок 1: Четыре потоковых дерева, связанных с SgFile

Другой пример Fortran — система в University of Colorado, которая оптимизирует определенные выражения для параллельного выполнения на KSR-1. Полученный инструмент используется там проектом NSF Grand Challenge.

#### 3 Using Sage++
В этом разделе представлен обзор библиотеки Sage++. Библиотека содержит четыре семейства классов: классы проектов и файлов, соответствующие проектам приложений с несколькими источниками и исходным файлам, которые они содержат; классы операторов, соответствующие базовым исходным операторам в Fortran (со многими расширениями Fortran 90), C и C++; классы выражений, представляющие выражения, содержащиеся в операторах; классы символов, представляющие базовые определяемые пользователем идентификаторы; и классы типов, представляющие типы, связанные с каждым идентификатором и выражением (см. рисунок 1).

#### 3.1 Parsing
Чтобы преобразовать прикладную программу с помощью Sage++, каждый исходный файл должен быть сначала проанализирован с помощью анализатора Fortran f2dep или анализатора C/C++ pC++2dep. Результатом является набор машинно-независимых двоичных файлов, называемых файлами .dep. Каждый файл .dep соответствует одному программному дереву. Файлы .dep являются полными переводами исходных файлов, которые они представляют, включая комментарии, поэтому их можно использовать для восстановления исходного источника. Содержимое файла .dep можно проверить с помощью программы dumpdep.

#### 3.2 Project and File Classes
Класс Sage++ [[SgProject]] представляет набор исходных файлов приложения, которые необходимо преобразовать. Конструктор [[SgProject]] принимает файл .proj (список файлов .dep, разделенных новой строкой) в качестве аргумента и инициализирует объект [[SgProject]], загружая каждый из файлов .dep:
```cpp
main(){

SgProject P("MyProject.proj"); // opens and initializes project 

	for (int i = 0; i < P.numberOfFiles(); i++){
	
		printf("Working on file %s...\n", P.fileName(i)");
		
		// begin transformation of P.file(i) here;
	
	}

}
```

Каждый файл .dep содержит дерево программы для кода в исходном файле, который он представляет. Корень дерева в каждом файле называется глобальным узлом, а его непосредственные потомки — определения и функции верхнего уровня в файле. Каждый файл .dep также содержит таблицу символов и таблицу типов; они будут описаны ниже. 

Класс, представляющий файлы, [[SgFile]], предоставляет доступ к каждому из этих определений верхнего уровня и к таблицам символов и типов (см. рисунок 1). Функции-члены SgFile могут сохранять реструктурированную программу в стандартный поток вывода, строковый буфер, файл ASCII или файл .dep. Файл .dep можно распарсить обратно в исходный код с помощью утилиты unparse.

#### 3.3 Statement

Классы операторов Sage++ используются для представления основных единиц программ Fortran и C. Sage++ имеет 53 различных класса операторов, разделенных на пять категорий: структурированные определения заголовков, такие как функции, модули и классы; традиционные структурированные операторы управления, такие как циклы do и условные операторы; исполняемые операторы, такие как выражения C и вызовы подпрограмм; простые операторы управления, такие как goto и return; и объявления и различные операторы Fortran, такие как USE, PARAMETER и операторы ввода-вывода. Большая часть иерархии классов операторов показана в таблице в конце этой статьи.

Класс операторов верхнего уровня содержит функции-члены, которые применимы ко всем операторам. Подклассы добавляют специальные конструкторы и функции доступа. Каждый оператор имеет несколько стандартных атрибутов, доступных методам класса верхнего уровня. Номер исходной строки, уникальный идентификатор и тег варианта, который идентифицирует подкласс оператора, являются атрибутами операторов. Также может быть до трех выражений, напрямую связанных с любым оператором. Оператор C for является хорошим примером того, почему необходимы три выражения: for(expr 1; ​​expr 2; expr 3)fg. Поскольку базовый строительный блок Sage++ — это оператор, метки и комментарии связаны с предыдущим оператором.

Каждый оператор также имеет контекст, доступный через класс операторов верхнего уровня: он может иметь лексического предшественника и преемника, и он может быть вложен в блок управления другого оператора или в определение блочной структуры, например, структуру C. Этот охватывающий оператор называется родительским элементом управления и определяет базовую структуру дерева программы.

Чтобы проиллюстрировать использование классов операторов, рассмотрим следующий простой пример. Предположим, мы хотим
обойти файл и применить развертывающее преобразование ко всем самым внутренним циклам, тела которых состоят только из операторов присваивания. Функция показана ниже:

```cpp
void UnrollLoops(SgFile *file, int unroll_factor) { 

	SgStatement *s = file->firstStatement(); 
	
	SgForStmt *loop;

	while(s) {
	
		if (loop = isSgForStmt(s)) { 
		
			SgForStmt *inner;
			
			inner = loop->getInnermostLoop();
			
			if (inner->isAssignLoop()) 
				inner->unrollLoop(unroll_factor);
			
		}
		
		s = s->lexNext(); // the lexical successor of statement s.
		
	}

}
```
Эта функция иллюстрирует типичную программу Sage++; основная часть функции проходит по операторам в лексическом порядке. Переменная s — указатель на универсальный объект оператора. Есть два способа определить, является ли оператор циклом: проверить, является ли вариант FOR NODE, или использовать специальную функцию приведения, в данном случае isSgForStmt(). Функция типа

``SgSUBCLASS * isSgSUBCLASS( SgBASECLASS *)``

предоставляется для каждого подкласса [[SgStatement]], [[SgExpression]] и [[SgType]]. Эти функции проверяют вариант аргумента. Если объект имеет производный тип SgSUBCLASS, функция возвращает указатель на объект, приведенный к SgSUBCLASS* (таким образом, разрешая доступ к специальным функциям-членам SgSUBCLASS). В противном случае она возвращает NULL.

#### 3.4 Expressions 
Выражения представлены деревьями объектов из класса выражений Sage++. Эти деревья имеют либо степень два (для бинарных операторов), либо степень один (для унарных операторов).

Базовый класс для выражений [[SgExpression]] содержит методы, общие для всех выражений. Каждое выражение может иметь до двух операндов: левая часть lhs() и правая часть rhs(). Кроме того, каждое выражение имеет тип и может иметь символ. Функции-члены [[SgExpression]] позволяют программисту проверять и изменять эти поля.

Кроме того, существуют специальные методы, которые манипулируют всем деревом выражений, корнем которого является заданный узел. Например, replaceSymbolByExpression() ищет в выражении ссылки на символы и заменяет их выражением. Чтобы помочь в построении модулей анализа зависимостей, существует метод, который упростит линейные алгебраические выражения до нормальной формы, и другой, который извлечет целочисленный коэффициент символа в линейном выражении.

Иерархия классов Sage++ для выражений показана в таблице в конце этой статьи. В отличие от классов, представляющих операторы, для каждого вида выражения нет подкласса. Узлы выражения, имеющие свой собственный подкласс, имеют специальный тип конструктора или специальные поля. Стандартным бинарным операторам не были предоставлены явные подклассы выражений. Вместо этого эти операторы были перегружены как «друзья» класса выражений, поэтому построение выражений, содержащих их, является очень простой задачей. Например, чтобы построить выражение вида:
				``(X + 3)  Y + 6:4``
нам понадобятся два объекта-символа и два объекта-выражения значения:
```cpp
SgVariableSymb xsymb("X"), ysymb("Y"); 

SgVarRefExp x(xsymb), y(ysymb); 

SgValueExp three(3), fltvalue(6.4); 

SgExpression &e = (x + three)*y + fltvalue;
```
Переменные X и Y создаются как символы, затем выражения ссылок на переменные для символов создаются через объекты SgVarRefExp. Обратите внимание, что мы не указали типы переменных X и Y, и их объявления не были сгенерированы. Мы вернемся к этому в следующем разделе. В этом коде e теперь является ссылкой на корень (+) программного дерева для нужного выражения (см. рисунок 2). Также обратите внимание, что конструкторы для класса выражения значения позволяют создавать любое значение базового типа:

```cpp
SgValueExp(int value); 
SgValueExp(char char_val); 
SgValueExp(float float_val); 
SgValueExp(double double_val); 
SgValueExp(char *string_val);

SgValueExp(double real, double imaginary); SgValueExp(SgValueExp &real, SgValueExp &imaginary);
```
Чтобы построить оператор присваивания C в форме
``X = (X + 3)  Y + 6:4;``
Используя определения переменных X, Y, three и tvalue, данные выше, мы сначала создаем выражение SgAssignOp, а затем используем его для создания объекта SgCExpStmt:
```cpp
SgCExpStmt c_stmt(SgAssignOp(x.copy(), (x + three)*y + fltvalue));
```
В Фортране нет выражений присваивания, и мы строим оператор напрямую:
```cpp
SgAssignStmt fortran_stmt(x.copy(), (x + three)*y + fltvalue);
```
Подклассы выражений предоставляют конструкторы, которые упрощают построение выражений и извлечение значений. Например, конструкторы для класса SgArrayRefExp, используемые для ссылок на массивы, упрощают построение ссылок на массивы.
![[Pasted image 20241208144207.png]]
				Рисунок 2: Сегмент дерева программ
```cpp
SgArrayRefExp(SgSymbol &s, SgExpression &sub1, SgExpression &sub2, SgExpression &sub3);
```
создает ссылку на массив 3-D для массива с символом s и тремя индексными выражениями. В качестве другого примера, векторные выражения в Fortran (и нашем расширении для C) имеют форму exp1 : exp2 : exp3 и представлены классом SgSubscriptExp, который имеет конструктор формы
```cpp
SgSubscriptExp(SgExpression &lbound, SgExpression &ubound, SgExpression &step)
```
а также функции доступа для извлечения трех аргументов. Таким образом, для построения ссылки на массив Fortran 90 X(1:100:3) или «расширенной» ссылки на массив C X\[1:100:3\] мы можем написать
```cpp
SgVariableSymb xsymb("X");

SgValueExp three(3), one(1), hundred(100); 
SgSubscriptExp range(one, hundred, three); 
SgArrayRefExp new_expression(xsymb, range);
```

#### 3.5 Symbols and Types
#### 3.5.1 Symbols
Базовый класс Sage++ для символов — [[SgSymbol]]. Символы в каждом файле организованы в виде списка, доступного из [[SgFile]]. Каждый символ имеет уникальный identifyer(), type(), который подробно описан ниже, и оператор, называемый scope(), который является оператором, в котором объявление находится в области видимости (т. е. родительский элемент управления оператора объявления). Оператор, в котором объявляется переменная, задается declaredInStmt().

[[SgSymbol]] имеет три метода для создания копий символа. Самый простой метод копирует только запись таблицы символов. Другая функция копирует символ и генерирует новую информацию о типе, а третий метод также копирует тело объявления. Для символов Fortran 90 атрибуты можно проверять или изменять.

Существует относительно немного подклассов символов:

	SgVariableSymb представляет основные имена переменных программы. Он имеет методы, которые возвращают количество использований переменной, а также операторы и выражения, в которых она используется. Аналогичные функции существуют для определений переменной.
	SgConstantSymb представляет имена констант программы. Экземпляры могут быть созданы путем указания идентификатора, оператора области действия и выражения, определяющего значение.
	SgFunctionSymb представляет имена функций и подпрограмм. Методы позволяют получить доступ к символам в списке формальных параметров, результирующему символу и рекурсивному флагу для Fortran.
	SgMemberFuncSymb представляет символы для функций-членов классов и структур. Конструктор позволяет указать идентификатор, тип, охватывающий класс и статус защиты функции. Методы возвращают статус защиты функции и запись таблицы символов определяющего класса.

	SgFieldSymb Этот класс используется для полей в операторе перечисления C или полей в структуре или классе. Он имеет методы, похожие на методы в SgMemberFuncSymb.
	SgClassSymb представляет имена классов, объединений, структур и коллекций pC++ (расширение языка с параллельными данными). Его методы предоставляют доступ к полям и функциям классов, которые он представляет.
	SgTypeSymb используется для символов из определения типа C.
	SgLabelSymb — для меток C.
	SgLabelVarSymb — для переменных меток Fortran.
	SgExternalSymb — для внешних функций Fortran.
	SgConstructSymb — для имен конструкций Fortran.
	SgInterfaceSymb — для интерфейсов модулей Fortran 90.

Обход таблицы символов (Traversing) — очень распространенная задача Sage++. Например, рассмотрим задачу поиска записи в таблице символов для заданной функции-члена в заданном классе. Есть несколько способов сделать это. Код ниже ищет в таблице имя класса. Затем он ищет в списке полей имя функции-члена и в конце возвращает указатель на объект-символ (если он найден).
```cpp
SgSymbol *findMemberFunction(char *className, char *functionName){ 

	SgSymbol *s, *fld;
	
	SgClassSymb *cl;
	
	SgMemberFuncSymb *f; int i;
	
	for (s=file.firstSymbol(); s ; s = s->next()) 
	
		if (!strcmp(s->identifier(), className))
		
			break;
	
		if (s == NULL)
	
			return  NULL;
	
		if (cl = isSgClassSymb(s)){
	
		for(i = 1, fld = cl->field(i); fld; fld = cl->field(i++)) { 
			if ((f = isSgMemberFuncSymb(fld)) && !strcmp(f->identifier(), functionName)) 
			return f;
		
		}
	
	}
	
	return  NULL;

}
```
#### 3.5.2 Types
Классы типов Sage++ содержат базовую информацию о символах. Как и в случае с символами, Sage++ помещает типы из исходного файла в список объектов, к заголовку которых можно получить доступ через метод SgFile.

Базовым классом для типов является [[SgType]]. Многие типы определяются в терминах других типов. Например, тип массива имеет базовый тип, который может быть типом указателя, который имеет базовый тип, который может быть целым числом или классом и т. д. Методы [[SgType]] могут копировать типы и проверять, эквивалентны ли два типа.
Существует восемь основных подклассов[[SgType]]:

SgTypeInt, SgTypeFloat, SgTypeChar, ... являются основными типами.
[[SgArrayType]] используется для представления типов массивов. Анализатор присваивает каждой переменной массива собственный объект дескриптора типа массива. Функции-члены могут добавлять новые измерения, возвращать форму и базовый тип массива, а также изменять базовый тип.
[[SgClassType]] представляет типы структур C, записей Fortran, классов C++, объединений C, перечислений C и коллекций pC++.
[[SgPointerType]] представляет типы указателей.
[[SgReferenceType]] представляет типы ссылок C++, т. е. в форме int &x.
[[SgFunctionType]] представляет типы символов для функций. Метод возвращает тип возвращаемого значения функции; другой метод позволяет модифицировать этот тип.
[[SgDerivedType]] представляет тип символов C, полученных из typedef, а также тип переменных, которые имеют тип класса.
[[SgDescriptType]] — это объект дескриптора, который служит для модификации другого объекта типа. Например, в операторе C long volatile int x; long и volatile являются модификаторами, а int — базовым типом. Тип x представлен объектом SgDescriptType, который содержит информацию о модификаторах и базовом типе.
Чтобы проиллюстрировать использование таблицы типов, рассмотрим простую задачу определения, принадлежит ли переменная определенному пользователем классу. Более конкретно, при анализе кода
```cpp
class myClass; myClass x, y;

y = x + 2;
```
если e — это выражение, представляющее ссылку на переменную x, нам нужна функция isVarRefOf- Class(e, \myClass"), которая будет возвращать 1, если тип класса совпадает, и 0 в противном случае. Чтобы написать эту функцию, мы сначала проверим, действительно ли e является ссылкой на переменную. Затем мы проверим, является ли тип символа производным типом. Из производного типа мы можем найти имя класса.
```cpp
int isVarRefOfClass(SgExpression *e, char *className){ 

	SgSymbol *s;
	
	SgDerivedType *d;
	
	SgClassSymb *cl;
	
	SgVarRefExp *exp;
	
	  
	
	if((exp = isSgVarRefExp(e)) == NULL) return 0; 
	
	s = exp->symbol();
	
	if((d = isSgDerivedType(s->type())) == NULL) return 0; 
	
	if(cl = isSgClassSymb(d->typeName()))
	
		if(!strcmp(cl->identifier(), className)) return 1;
	
	return 0;

}
```
#### 4 Data Dependence and Data Flow Analysis
Sage++ предоставляет общую структуру для анализа зависимости данных и потока, похожую на описанную в \[7\]. Эта часть Sage++ была сохранена максимально открытой для облегчения экспериментов. Обратите внимание, что процедуры анализа зависимости данных и потока в Sage++ все еще находятся в стадии разработки и время от времени подвергаются изменениям. Текущая реализация ограничена Fortran 77.
#### 4.1 Data Dependence Analysis
Тест Omega \[8\] — это тест зависимости данных, используемый в Sage++. Процедуры зависимости данных в Sage++ предоставляют интерфейс для программного обеспечения Omega. Предоставляются функции для извлечения данных из циклов о переменных индукции, доступе к массиву в линейной форме и зависимостях данных. Информация о зависимости данных предоставляется в форме векторов расстояния и направления (та же информация о зависимости данных, которая вычисляется Omega). Класс depGraph хранит информацию о зависимости данных; подмножество этого класса показано ниже:

```cpp
class depGraph {

	depNode *current; // list of dependences depNode *first;
	
	public:
	
	SgStatement *loop; // the loop statement
	
	Set *arrayRef; // list of array access in the loop in linear form 
	
	Set *induc; // set of induction variables
	
	depGraph(SgFile *fi, SgStatement *f,SgStatement *l);
	
	~depGraph();
	
	...

};
```
Тот факт, что ссылки на массивы хранятся в линейной форме, помогает реализовать интерфейс для тестов зависимости. График зависимости и другая информация, связанная с циклом, может быть рассчитана для любой функции путем вызова
```cpp 
initializeDepAnalysisForFunction(file,function)

// extracts the dependence graph for the named loop.
depg = new depGraph(file,function,loop) 
```
#### 4.2 Flow Analysis
Sage++ предоставляет фреймворк для анализа потока данных, чтобы помочь пользователям писать свои собственные процедуры анализа потока данных. Например, чтобы реализовать итеративный прямой анализ потока данных, пользователь пишет набор функций для построения наборов gen и kill для каждого оператора и функцию equal (которая указывает, когда два элемента набора равны), и передает эти функции следующей функции Sage++:

```cpp
void iterativeForwardFlowAnalysis(
	SgFile *file, 
	SgStatement *func, 
	Set *(*giveGenSet) (SgStatement *func,SgStatement *stmt), 
	Set *(*giveKillSet)(SgStatement*func,SgStatement *stmt), 
	int (*equal)(void *e1, void *e2),...);
```

Класс Set предоставляется для помощи в реализации наборов данных.
Текущая версия также предлагает более общую структуру анализа потока с такими функциями, как controlFlow(SgStatement \*stmt,...), которая возвращает последователей и предшественников оператора в графе потока управления, и defUseVar(SgStatement \*stmt,...), которая возвращает список данных, считанных и записанных оператором. Эти функции можно использовать для построения более сложных инструментов анализа потока.
#### 4.3 Loop Transformations
Sage++ предоставляет набор базовых инструментов преобразования циклов. Ниже приведены некоторые из доступных преобразований циклов:
```cpp
int loopFusion(SgStatement *loop1,SgStatement *loop2) int loopInterchange(SgStatement *b, int *permut, int n)

int tileLoops(SgStatement *func,SgStatement *b, int *size, int nb) int distributeLoopSCC(SgStatement *b, int *sccTable, int  leadingdim, int  numSCC)
...
```
Эти процедуры преобразования не проверяют допустимость выполняемых ими преобразований. Условия, требуемые для применения преобразования, могут сильно отличаться от одного приложения Sage++ к другому. Во многих случаях известно, что преобразование допустимо, но все равно его допустимость не может быть явно проверена. Например, это тот случай, когда предыдущее преобразование изменило структуру цикла без обновления графа зависимости данных. Кроме того, программные преобразования также могут быть заданы директивами в коде.

#### 5 Finding Out More About Sage++
Для получения полной информации об использовании Sage++ обратитесь к Руководству пользователя Sage++ (около 250 страниц). Это наиболее полный справочник по Sage++ из имеющихся. Он включает введение и обзор Sage++, полное описание каждого класса в библиотеке, несколько примеров программ и полный индекс.
Команда разработчиков Sage++ поддерживает автоматизированный почтовый сервер, FTP-архив и сервер. Чтобы получить больше информации о списках рассылки Sage++, отправьте непустое сообщение по адресу:
	sage-request@cica.indiana.edu
Все документы, руководства, файлы программ и гипертекстовые документы Sage++ также доступны через анонимный FTP-архив ftp
cica.cica.indiana.edu:pub/sage
Гипертекстовая версия руководства пользователя Sage++ и других документов доступна по адресу WWW
	http://www.cica.indiana.edu/sage/home-page.html 
Отчеты об ошибках можно отправлять по адресу
	sage-bugs@cica.indiana.edu
#### 6 Limitations of Sage++
Sage++ показал себя мощным инструментом в наших экспериментах по прототипированию компилятора, но у него все еще есть ряд ограничений. Самым важным из них является то, что пользователям нелегко добавлять расширения языка в Fortran или C. Чтобы добавить новый оператор в язык, необходимо расширить парсер (основанный на версии YACC GNU Bison), добавить новый тип узла во внутреннюю форму и соответствующий подкласс в иерархию Sage++. Модуль unparser, который управляется таблицами, также должен быть расширен для распознавания этого нового узла. Хотя мы делали это несколько раз (мы добавляли некоторые расширения PCF, Fortran-S, Fortran-M и HPF в Fortran и расширяли C++ для определения нашего языка pC++ \[5\], а также предлагаемого синтаксиса CC++), это непростая задача, поскольку она требует полного понимания внутренних структур парсера. Будущая версия Sage++ будет работать с другим генератором синтаксических анализаторов, что, как мы надеемся, упростит эту задачу.
#### 7 Conclusions
Иерархия объектов Sage++ предоставляет гибкий и расширяемый инструмент для манипулирования внутренним представлением программ, написанных на C/C++ и Fortran (и его расширениях). В сочетании с парсерами и депарсером набор инструментов Sage++ позволяет исследователям эффективно конструировать широкий спектр систем преобразования исходного кода в исходный код, значительно сокращая время разработки, которое обычно связано с созданием таких систем с нуля.

Sage++ все еще находится в стадии разработки. Многие из уже реализованных улучшений и расширений были предложены пользователями Sage++. Мы хотели бы поблагодарить их всех, и в частности Бернда Мора, Эндрю Мауэра, Даррила Брауна, Майкла Голдена и Крейга Чейза.

#### References

	\[1\] G. Fox, S. Hiranandani, K. Kennedy, C. Koelbel, U. Kremer, C. Tseng, and M. Wu. "Fortran D Language Specication." Tech. Report COMP TR90079 from the Dept. Computer Science, Rice University, March 1991.

	\[2\] P. Brezany, M. Gerndt, V. Sipkova, and H.P. Zima. "SUPERB support for irregular scientic computations." In Proceedings of the Scalable High Performance Computing Conference (SHPCC-92). IEEE Computer Society Press, April 1992, pp. 314-321.

	\[3\] F. Bodin, L. Kervella, and T. Priol. "Fortran-S: A Fortran Interface for Shared Virtual Memory Architectures." In Proceedings, Supercomputing 93, Portland Oregon.

	\[4\] J. Dongarra, R. Pozzo, D. Walker, "An Object Oriented Design for High Performance Linear Algebra on Distributed Memory Architectures," In Proceedings of the First Annual Object-Oriented Numerics Conference (OON-SKI), Sunriver, Oregon, Apr. 1993, pp. 257-264.

	\[5\] F. Bodin, D. Gannon, P. Beckman, S. Narayana, S. Yang , \Distributed pC++: Basic Ideas for an Object Parallel Language," In Proceedings of the First Annual Object-Oriented Numerics Conference (OON-SKI), Sunriver, Oregon, Apr. 1993, pp. 1-24.

	\[6\] Polychronopoulos, C., Girkar, M., Haghighat, M., et al, "The Structure of Parafrase-2: An Advanced Parallelizing Compiler for C and Fortran", In Languages and Compilers for Paral lel Computing, Gelernter, D., Nicolau, A., Padua, D., eds., MIT Press 1990, pp. 423-453.

	\[7\] A. V. Aho and R. Sethi and J. D. Ullman, Compiler Principles, Techniques, and Tools, Addison Wesley, 1986.

	\[8\] W. Pugh, D. Wonnacott "Eliminating False Data Dependences Using the Omega Test" Tech. Report CS-TR-2993, from the Dept. of Computer Science, Univ. of Maryland; an earlier version appeared at the ACM SIGPLAN PLDI'92 conference.

	\[9\] A. Malony, B. Mohr, P. Beckman, D. Gannon, S. Yang, F. Bodin, \Performance Analysis of pC++: A Portable Data-Parallel Programming System for Scalable Parallel Computers", In Proc. 8th Int. Paral lel Processing Symb. (IPPS), Cancun, Mexico, Apr. 1994.

	\[10\] A.Griewank, \On Automatic Diserentiation", In Mathematical Programming: Recent Developments and Applications, M. Iri and K. Tanabe, eds., Kluwer Academic Publishers, 1989, pp. 83-108.

![[Pasted image 20241208154731.png]]

![[Pasted image 20241208154743.png]]

Источник: 
https://www.researchgate.net/publication/2725408_Sage_An_Object-Oriented_Toolkit_and_Class_Library_for_Building_Fortran_and_C_Restructuring_Tools

![[Sage_An_Object-Oriented_Toolkit_and_Class_Library_.pdf]]

![[Sage_An_Object-Oriented_Toolkit_and_Class_Library_.docx]]

