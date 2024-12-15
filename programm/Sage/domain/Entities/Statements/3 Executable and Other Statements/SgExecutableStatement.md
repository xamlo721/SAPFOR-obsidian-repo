Представляет собой исполняемые инструкции для всех языков.

```cpp
class  **SgExecutableStatement**: public  SgStatement {
  // this is really a non-control, non-declaration stmt.
  // no special functions here.
public: 
  inline SgExecutableStatement(int variant);
};
```

#### Члены класса

`**SgExecutableStatement**`**(int variant)**

document me