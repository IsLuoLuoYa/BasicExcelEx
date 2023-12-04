# BasicExcel使用

[官网](https://www.codeproject.com/Articles/13852/BasicExcel-A-Class-to-Read-and-Write-to-Microsoft)



## 基本使用

```c++
#include <iostream>
#include "BasicExcel.hpp"
using namespace YExcel;

int main() {
    BasicExcel e;
    e.Load("test1.xls");
    e.New(1);
    BasicExcelWorksheet* sheet = e.GetWorksheet("Sheet1");
    BasicExcelCell* cell = sheet->Cell(0,0);
    cell->Set(3.6666);
    e.SaveAs("test1.xls");
    return 0;
}
```



> 注意

1. 使用```using namespace YExcel;```命名；
2. 一定得使用```BasicExcel::New()```函数创建工作博，否则文件出错，打不开；



我应该列出您应该知道使用的三个类中的函数。接下来将有一个示例代码。`BasicExcel`



## 函数大全

### 类 基本Excel



| `void New(int sheets=3)`                                     | 使用给定数量的电子表格创建新的 Excel 工作簿（最少 1 个）。   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `bool Load(const char* filename)`                            | 从文件加载 Excel 工作簿。                                    |
| `bool Save()`                                                | 将当前Excel工作簿保存到打开的文件。                          |
| `bool SaveAs(const char* filename)`                          | 将当前 Excel 工作簿保存到文件。                              |
| `size_t GetTotalWorkSheets()`                                | 当前 Excel 工作簿中的 Excel 工作表总数。                     |
| `BasicExcelWorksheet* GetWorksheet(size_t sheetIndex)`       | 获取指向给定索引处的 Excel 工作表的指针。索引从 开始。如果索引无效，则返回。`0``0` |
| `BasicExcelWorksheet* GetWorksheet(const char* name)`        | 获取指向已指定 ANSI 名称的 Excel 工作表的指针。如果没有具有给定名称的 Excel 工作表，则返回。`0` |
| `BasicExcelWorksheet* GetWorksheet(const wchar_t* name)`     | 获取指向已指定 Unicode 名称的 Excel 工作表的指针。如果没有具有给定名称的 Excel 工作表，则返回。`0` |
| `BasicExcelWorksheet* AddWorksheet(int sheetIndex=-1)`       | 将新的 Excel 工作表添加到给定索引。工作表的名称是 SheetX，其中 X 是从 1 开始的数字。索引从 开始。工作表将添加到最后一个位置，如果 。如果成功，则返回指向工作表的指针，否则返回。`0``sheetIndex == -1``0` |
| `BasicExcelWorksheet* AddWorksheet(const char* name, int sheetIndex=-1)` | 将具有给定 ANSI 名称的新 Excel 工作表添加到给定索引。索引从 开始。工作表将添加到最后一个位置，如果 。如果成功，则返回指向工作表的指针，否则返回 0。`0``sheetIndex == -1` |
| `BasicExcelWorksheet* AddWorksheet(const wchar_t* name, int sheetIndex=-1)` | 将具有给定 Unicode 名称的新 Excel 工作表添加到给定索引。索引从 开始。工作表将添加到最后一个位置，如果 。如果成功，则返回指向工作表的指针，否则返回 0。`0``sheetIndex == -1` |
| `bool DeleteWorksheet(size_t sheetIndex)`                    | 删除给定索引处的 Excel 工作表。索引从 开始。如果成功，则返回，否则返回。`0``true ``false` |
| `bool DeleteWorksheet(const char* name)`                     | 删除已指定 ANSI 名称的 Excel 工作表。如果成功，则返回，否则返回。`true ``false` |
| `bool DeleteWorksheet(const wchar_t* name)`                  | 删除已指定 Unicode 名称的 Excel 工作表。如果成功，则返回，否则返回。`true ``false` |
| `char* GetAnsiSheetName(size_t sheetIndex)`                  | 获取给定索引处的工作表名称。索引从 开始。如果名称采用 Unicode 格式，则返回。`0``0` |
| `wchar_t* GetUnicodeSheetName(size_t sheetIndex)`            | 获取给定索引处的工作表名称。索引从 开始。如果名称采用 ANSI 格式，则返回。`0``0` |
| `bool GetSheetName(size_t sheetIndex, char* name)`           | 获取给定索引处的工作表名称。索引从 开始。如果名称采用 Unicode 格式，则返回。`0``false` |
| `bool GetSheetName(size_t sheetIndex, wchar_t* name)`        | 获取给定索引处的工作表名称。索引从 0 开始。如果名称采用 ANSI 格式，则返回。`false` |
| `bool RenameWorksheet(size_t sheetIndex, const char* to)`    | 将给定索引处的 Excel 工作表重命名为给定的 ANSI 名称。索引从 开始。如果成功，则返回，否则返回。`0``true ``false` |
| `bool RenameWorksheet(size_t sheetIndex, const wchar_t* to)` | 将给定索引处的 Excel 工作表重命名为给定的 Unicode 名称。索引从 开始。如果成功，则返回，否则返回。`0``true ``false` |
| `bool RenameWorksheet(const char* from, const char* to)`     | 将已指定 ANSI 名称的 Excel 工作表重命名为另一个 ANSI 名称。如果成功，则返回，否则返回。`true ``false` |
| `bool RenameWorksheet(const wchar_t* from, const wchar_t* to)` | 将已指定 Unicode 名称的 Excel 工作表重命名为另一个 Unicode 名称。如果成功，则返回，否则返回。`true ``false` |



### 类基本Excel工作表



| `char* GetAnsiSheetName()`                                   | 获取当前工作表名称。如果名称采用 Unicode 格式，则返回。`0`   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `wchar_t* GetUnicodeSheetName()`                             | 获取当前工作表名称。如果名称采用 ANSI 格式，则返回。`0`      |
| `bool GetSheetName(char* name)`                              | 获取当前工作表名称。如果名称采用 Unicode 格式，则返回。`false` |
| `bool GetSheetName(wchar_t* name)`                           | 获取当前工作表名称。如果名称采用 ANSI 格式，则返回。`false`  |
| `bool Rename(const char* to)`                                | 将当前 Excel 工作表重命名为另一个 ANSI 名称。如果成功，则返回，否则返回。`true ``false` |
| `bool Rename(const wchar_t* to)`                             | 将当前 Excel 工作表重命名为另一个 Unicode 名称。如果成功，则返回，否则返回。`true ``false` |
| `void Print(ostream& os, char delimiter=',', char textQualifier='\0')` | 将整个工作表打印到输出流，使用定义的分隔符分隔每一列，并使用定义的 .如果不希望有任何文本限定符，请省略参数。`textQualifier``textQualifier` |
| `size_t GetTotalRows()`                                      | 当前 Excel 工作表中的总行数。                                |
| `size_t GetTotalCols()`                                      | 当前 Excel 工作表中的列总数。                                |
| `BasicExcelCell* Cell(size_t row, size_t col)`               | 返回指向 Excel 单元格的指针。行和列从 开始。如果行超过 65535 或列超过 255，则返回。`0``0` |
| `bool EraseCell(size_t row, size_t col)`                     | 擦除单元格的内容。行和列从 开始。如果成功，如果行或列超出范围，则返回。`0``true ``false` |



### 类 BasicExcelCell





| `int Type() const`                                           | 获取存储在当前 Excel 单元格中的值的类型。返回以下枚举之一：、。`UNDEFINED``INT``DOUBLE``STRING``WSTRING` |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `bool Get(int& val) const`                                   | 获取一个值。如果单元格不包含 .`integer ``false ``integer`    |
| `bool Get(double& val) const`                                | 获取一个值。如果单元格不包含 .`double ``false ``double`      |
| `bool Get(char* str) const`                                  | 获取 ANSI 字符串。如果单元格不包含 ANSI 则返回。`false ``string` |
| `bool Get(wchar_t* str) const`                               | 获取一个 Unicode 字符串。如果单元格不包含 Unicode 则返回。`false ``string` |
| `size_t GetStringLength()`                                   | 返回 ANSI 或 Unicode 字符串的长度（不包括字符）。`null`      |
| `int GetInteger() const`                                     | 获取一个值。如果单元格不包含 .`integer ``0``integer`         |
| `double GetDouble() const`                                   | 获取一个值。如果单元格不包含 .`double ``0``.<code>0``double` |
| `const char* GetString() const`                              | 获取 ANSI .如果单元格不包含 ANSI 则返回。`string``0``string` |
| `const wchar_t* GetWString() const`                          | 获取一个统一码。如果单元格不包含 Unicode 则返回。`string``0``string` |
| `ostream& operator<<(ostream& os, const BasicExcelCell& cell)` | 打印要输出的单元格。如果未定义单元格，则打印空字符。`stream` |
| `void Set(int val)`                                          | 将当前 Excel 单元格的内容设置为 .`integer`                   |
| `void Set(double val)`                                       | 将当前 Excel 单元格的内容设置为 .`double`                    |
| `void Set(const char* str)`                                  | 将当前 Excel 单元格的内容设置为 ANSI 。`string`              |
| `void Set(const wchar_t* str)`                               | 将当前 Excel 单元格的内容设置为 Unicode g。`strin`           |
| `void SetInteger(int val)`                                   | 将当前 Excel 单元格的内容设置为 .`integer`                   |
| `void SetDouble(double val)`                                 | 将当前 Excel 单元格的内容设置为 .`double`                    |
| `void SetString(const char* str)`                            | 将当前 Excel 单元格的内容设置为 ANSI 。`string`              |
| `void SetWString(const wchar_t* str)`                        | 将当前 Excel 单元格的内容设置为 Unicode 。`string`           |
| `void EraseContents()`                                       | 擦除当前Excel单元格的内容。将类型设置为 。`UNDEFINED`        |



## 示例代码

```c++
#include "BasicExcel.hpp"
using namespace YExcel;

int main(int argc, char* argv[])
{
  BasicExcel e;

  // Load a workbook with one sheet, display its contents and
  // save into another file.
  e.Load("example1.xls");
  BasicExcelWorksheet* sheet1 = e.GetWorksheet("Sheet1");
  if (sheet1)
  {
    size_t maxRows = sheet1->GetTotalRows();
    size_t maxCols = sheet1->GetTotalCols();
    cout << "Dimension of " << sheet1->GetAnsiSheetName() <<
        " (" << maxRows << ", " << maxCols << ")" << endl;

    printf(" ");
    for (size_t c=0; c<maxCols; ++c) printf("%10d", c+1);
    cout << endl;

    for (size_t r=0; r<maxRows; ++r)
    {
      printf("%10d", r+1);
      for (size_t c=0; c<maxCols; ++c)
      {
        BasicExcelCell* cell = sheet1->Cell(r,c);
        switch (cell->Type())
        {
          case BasicExcelCell::UNDEFINED:
            printf(" ");
            break;

          case BasicExcelCell::INT:
            printf("%10d", cell->GetInteger());
            break;

          case BasicExcelCell::DOUBLE:
            printf("%10.6lf", cell->GetDouble());
            break;

          case BasicExcelCell::STRING:
            printf("%10s", cell->GetString());
            break;

          case BasicExcelCell::WSTRING:
            wprintf(L"%10s", cell->GetWString());
            break;
        }
      }
      cout << endl;
    }
  }
  cout << endl;
  e.SaveAs("example2.xls");

  // Create a new workbook with 2 worksheets and write some contents.
  e.New(2);
  e.RenameWorksheet("Sheet1", "Test1");
  BasicExcelWorksheet* sheet = e.GetWorksheet("Test1");
  BasicExcelCell* cell;
  if (sheet)
  {
    for (size_t c=0; c<4; ++c)
    {
      cell = sheet->Cell(0,c);
      cell->Set((int)c);
    }

    cell = sheet->Cell(1,3);
    cell->SetDouble(3.141592654);

    sheet->Cell(1,4)->SetString("Test str1");
    sheet->Cell(2,0)->SetString("Test str2");
    sheet->Cell(2,5)->SetString("Test str1");

    sheet->Cell(4,0)->SetDouble(1.1);
    sheet->Cell(4,1)->SetDouble(2.2);
    sheet->Cell(4,2)->SetDouble(3.3);
    sheet->Cell(4,3)->SetDouble(4.4);
    sheet->Cell(4,4)->SetDouble(5.5);

    sheet->Cell(4,4)->EraseContents();
  }

  sheet = e.AddWorksheet("Test2", 1);
  sheet = e.GetWorksheet(1);
  if (sheet)
  {
    sheet->Cell(1,1)->SetDouble(1.1);
    sheet->Cell(2,2)->SetDouble(2.2);
    sheet->Cell(3,3)->SetDouble(3.3);
    sheet->Cell(4,4)->SetDouble(4.4);
    sheet->Cell(70,2)->SetDouble(5.5);
  }
  e.SaveAs("example3.xls");

  // Load the newly created sheet and display its contents
  e.Load("example3.xls");

  size_t maxSheets = e.GetTotalWorkSheets();
  cout << "Total number of worksheets: " << e.GetTotalWorkSheets() << endl;
  for (size_t i=0; i<maxSheets; ++i)
  {
    BasicExcelWorksheet* sheet = e.GetWorksheet(i);
    if (sheet)
    {
      size_t maxRows = sheet->GetTotalRows();
      size_t maxCols = sheet->GetTotalCols();
      cout << "Dimension of " << sheet->GetAnsiSheetName() <<
         " (" << maxRows << ", " << maxCols << ")" << endl;

      if (maxRows>0)
      {
        printf(" ");
        for (size_t c=0; c<maxCols; ++c) printf("%10d", c+1);
        cout << endl;
      }

      for (size_t r=0; r<maxRows; ++r)
      {
        printf("%10d", r+1);
        for (size_t c=0; c<maxCols; ++c)
        {
          cout << setw(10) << *(sheet->Cell(r,c));
        // Another way of printing a cell content.
        }
        cout << endl;
      }
      if (i==0)
      {
        ofstream f("example4.csv");
        sheet->Print(f, ',', '\"'); // Save the first sheet as a CSV file.
        f.close();
      }
    }
    cout << endl;
  }
  return 0;
}
```

