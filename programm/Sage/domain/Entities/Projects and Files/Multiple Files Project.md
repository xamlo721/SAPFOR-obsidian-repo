
В Sage предусмотрена возможность работы с несколькими файлами, но существует ряд ограничений: одновременно можно выбрать только один файл. Файл выбирается с помощью следующих методов:

```cpp
     SgProject::file(int i)
     SgFile::SgFile(char * dep_file_name)
```

Когда выбран файл, все операции в базе данных будут использовать текущую структуру данных файла (см. рисунок 1). Например, если создается инструкция, она добавляется в текущую структуру файла. При открытии проекта автоматически выбирается первый файл.

![[Pasted image 20241210003555.png]]

### Примеры использования 

Вот пример использования возможности работы с несколькими файлами:
```cpp
  project =  new SgProject("test.proj");
  nbfile = project->numberOfFiles();
  for (i=0; i< nbfile; i++)
    {
      file = &(project->file(i));
      printf("|||||||||||||||||||||||||||||||||||||||||||||||||||||||||\n");
      // any operations here will operate on file number i
      // file i has been selected by the method project->file(i)

      // do work here.......

      file->unparsestdout();
    }
```

Вот пример кода для извлечения кода функции из проекта с несколькими файлами:

```cpp
  nbfile = project->numberOfFiles();
  printf("Give the name of the function: ");
  scanf("%s",str);
  for (i=0; i< nbfile; i++) {
  
      file = &(project->file(i));
      if (!file) {
          Message("file not found",0);
          exit(1);
      }
      nbfunc = file->numberOfFunctions();
      for (j=0; jfunctions(j);
          if (!strcmp(func->symbol()->identifier(),str)) {
              printf("Function %s found in file %s\n",
                     func->symbol()->identifier(),
                     project->fileName(i));
              break;
	       }
        }
    }
```



