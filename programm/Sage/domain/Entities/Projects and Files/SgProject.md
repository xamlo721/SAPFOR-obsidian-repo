Проект - это группа обработанных исходных файлов (dep-файлов), составляющих программу, которой должен управлять Sage++. В настоящее время Sage++ может работать только с одним проектом одновременно. Если требуется несколько файлов в проекте, пожалуйста, обратитесь к разделу Атрибуты. (TODO)

На диске проект представлен в виде файла с именем, оканчивающимся на .proj, содержащего список имен файлов компонента .dep, по одному имени файла в строке. Файл - это один из проанализированных исходных файлов проекта. Каждый файл .dep содержит дерево синтаксического анализа. Корень дерева для файла называется глобальным узлом, а его непосредственные дочерние элементы - это определения и функции верхнего уровня в файлах. Файл также содержит таблицу символов и таблицу типов. Более подробную информацию о нем смотрите в обзоре .файлы dep.

Для получения доступа к данным проекта существует класс **SgProject**

```cpp
class  SgProject {

  public:

	  inline SgProject(SgProject &);
	  
	  /**
	   * proj_file_name - имя файла проекта; 
	   */
	  SgProject(const char *proj_file_name);
	
	  SgProject(const char *proj_file_name, char **files_list, int no);
	
	  inline ~SgProject();
	  
	  /**
	   * return - количество файлов в проекте; 
	   */
	  inline int numberOfFiles();
	
	  SgFile &file(int i);  
	
	  inline char *fileName(int i);
	
	  inline int Fortranlanguage();
	
	  inline int Clanguage();
	
	  void addFile(char * dep_file_name);
	
	  void deleteFile(SgFile * file);

};
```

####  Члены класса

Sage++ инициализируется путем создания экземпляра `SgProject` с помощью этого конструктора. Переменная `proj_file_name` представляет собой строку, содержащую имя файла `.proj`, соответствующего программе, которой нужно манипулировать.
```cpp
SgProject(char * proj_file_name)
```


Возвращает количество файлов в проекте.
```cpp
int numberOfFiles()
```


Возвращает ссылку на i-й файл в проекте.
```cpp
SgFile &file(int i)
```


Возвращает имя i-го файла в проекте.
```cpp
char *fileName(int i)
```


Возвращает ненулевое значение, если каждый файл в проекте является файлом Fortran.
```cpp
int Fortranlanguage()
```


Возвращает ненулевое значение, если хотя бы один файл в проекте не является файлом Fortran.
```cpp
int Clanguage()
```


В настоящее время не реализовано.
```cpp
void addFile(char * dep_file_name)
```


В настоящее время не реализовано.
```cpp
void deleteFile(SgFile * file)
```

### Примеры
```cpp
#include "sage++user.h"
main() {
  SgProject P("myproject.proj"); // opens and initializes project
  for(int i = 0; i < P.numberOfFiles(); i++){
    printf(" file is %s\n", P.fileName(i)");
    DoSomethingTo(P.file(i));
  };
}
```

```cpp
#include <stdio.h>
#include <GetOpt.h>
#include "sage++user.h"

int main (int argc, char **argv) {
  GetOpt getopt (argc, argv, "i:o:");
  SgProject *project;	
  int option_char;
  char *ifile, *ofile;	
  
  while ((option_char = getopt ()) != EOF)
    switch (option_char) {  
         case 'i': ifile = getopt.optarg; break;
         case 'o': ofile = getopt.optarg; break;
         case '?': fprintf (stderr, 
                   "usage: %s [i<input-proj> o<unparsed-file>]\n", argv[0]);
    }
  
  project = new SgProject (ifile);

  /* do something with the project */
}
```

[[2 Restructure - addStuffToProgram]]
[[1 Restructure - main]]
[[2 Instrument - InitSymbols]]
[[3 Instrument - InitFunctionTable]]
[[7 Instrument - FInitialize]]
[[9 Instrument - ProjectUnparse]]
[[12 Instrument - FAnalyze]]
[[22 Instrument - CAnalyze]]
[[23 Instrument - CInitSymbols]]
[[24 Instrument - CInitialize]]
[[28 Instrument - OpenProject]]
[[9 Expand Syntax - CAnalyze]]
[[10 Expand Syntax - ProjectUnparse]]
[[11 Expand Syntax - main]]
[[10 Expand Syntax - ProjectUnparse]]
[[11 Expand Syntax - main]]

Ссылки: [[SgFile]]

