Копирование между файлами должно выполняться функцией-членом,
```cpp
     inline SgSymbol &SgSymbol;::copyAcrossFiles(SgStatement &where;)
```

где параметр where указывает, куда будут вставлены инструкции. Этот метод может копировать только полную функцию, подпрограмму, класс или структуру. Он дублирует все выражения, символы и типы, на которые есть ссылки в теле функции, так что после копирования больше нет ссылок на исходный файл. 

Чтобы проиллюстрировать проблему копирования между файлами, давайте рассмотрим этот некорректный пример. 
```cpp
  project =  new SgProject("test.proj");
  nbfile = project->numberOfFiles();  
  file = &(project->file(0));
  func = file->functions(0);  // take the first function of file 0 to
                              // be copied and inserted in the other file
  func->extractStmt();    // extract to allow copy
  for (i=1; i< nbfile; i++)
    {
      file = &(project->file(i));
      if (!file)  
        {
          Message("file not found",0);
          exit(1);
        }
      first =   file->firstStatement();
      copyoffunc = &(func->copy()); // THIS IS REALLY WRONG
      first->insertStmtAfter(*copyoffunc);
      printf("|||||||||||||||||||||||||||||||||||||||||||||||||||||||||\n");
      file->unparsestdout();
      // unparse correctly but database is corrupted.
      sprintf(str,"debug%d.dep",i);
      file->saveDepFile(str); // incorrect database output.
    }
```
Результат показан на рисунке 2:
![[Pasted image 20241210003909.png]]
Примечание: Несмотря на то, что работа с несколькими файлами очень ограничена и хрупка, ее все же можно легко использовать для создания сложных структур данных. В одном файле синтаксический анализатор может создать объект для копирования. Затем его можно скопировать в другой файл, который будет использоваться в качестве шаблона.

```cpp
  .....
  project =  new SgProject("test.proj");
  nbfile = project->numberOfFiles();
  // set to the first file
  file = &(project->file(0));
  // get the first function
  func = file->functions(0);
  // get the symbol
  fc = func->symbol();
  // the following loop add the first function
  // of file number 0 to all the other files
  for (i=1; i< nbfile; i++)
    {
      file = &(project->file(i));
      first =   file->firstStatement();
      // call the copy across file function
      fccop =  &(fc->copyAcrossFiles(*first));
      // how to get the corresponding statement
      copyoffunc = fccop->body();
      file->unparsestdout();
    }
   .....
}
```
