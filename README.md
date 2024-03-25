公司的读表方式是把excel转成xml，再由C++读xml，觉得很烦，找了很久，也就这个BasicExcel简单好用

读数据为主,效率低

BasicExcel本身不支持.xlsx文件，需要另存为.xls

同时也不支持超过65535行和255列

用中文的页签名某些情况下会转换成空字符,导致打开失败

# 修改内容
bool BasicExcel::Load(const char* filename, bool IsOnlyRead = false);
    
Load函数增加默认只读参数，因为如果在已经某个软件中打开表格，读写打开会导致读不出数据，空指针异常
  
BasicExcelCell从的字符串成员，从char和wchar改成了string和wsting

## 数据读取修改
修改了数据读取的方式，比如一个单元格里写的是 1878684141.42352352，这种超长数字,原版的会将其视为一个字符串而不是double，double字段数据是0
    
## 数据读取修改后
头文件开始新增了多字符和宽字符互转的函数
        
如果单元格是一个字符串：BasicExcelCell的string VarStr和wstring ValWStr_中都会存一份，如果可以转成一个数值,int32、int64、double都会相应转换并写入
        
如果单元格是一个数值：int32、int64、double都会写一份,同时也会转换成string和wstring再存一份

写入中文字符串需要：Sheet0->Cell(Row, 1)->SetWString(BssicExcelUti::s2ws(utf8_to_ansi("中文").c_str()).c_str());
        
所以不论如何,对一个BasicExcelCel取值，总是能取到
        
 BasicExcelWorksheet增加了以下代码，用于从Excel按行按字段获取数据
```c++
struct BasicExcelRowData
{
	unordered_map<string, const BasicExcelCell*> Data;
	bool HasField(string Field) const;
	const BasicExcelCell* GetCellByField(string Field) const;
};
class BasicExcelWorksheet
{
private:
    int m_Row_Start = 0;
    int m_Row_End = 0;
    int m_Col_Start = 0;
    int m_Col_End = 0;
    unordered_map<string, int> FieldToCol;	// <字段名, 在第几列>
    bool DealCustomData(int DataStartRow = 2, int DataStartCol = 0);	    // 默认第0行是字段名,第1行是说明解释,第二行开始是真正的数据
    BasicExcelRowData GetRowData_Point(int Row);			    // 返回<key字段名, 该行该字段名对应的数据>		返回原始数据指针
public:
    void VisitAllRow(function<bool(int, const BasicExcelRowData&)> Func);    // 遍历所有行,返回true继续遍历下一行,返回false停止  参数1：行数   参数2：<字段名， 数据>
}
```
# 例子
Id     | Type | Max| Con| OpenDay
-------- | -----| -----| -----| -----
id  | 类型 | 每日寻宝次数上限| 消耗道具 | 开服天数
1  | 333 | 30 | 523,1 | 1,9999
2  | 1 | 30 | 523,3 | 1,9999
3  | 1 | 30 | 523,3 | 1,9999
```c++
#include <iostream>
#include "BasicExcel.hpp"
using namespace YExcel;


bool ReadHunting(int row, const BasicExcelRowData& data)
{
    if (row >= 5)
        return false;
    for (auto& it : data)
        printf("[<FileName:%s> <Val:%s>]  ", it.first.c_str(), it.second->GetString());
    printf("\n\n");
    return true;
}

int main() 
{
    BasicExcel e;
    e.Load("a.xls", true);
    BasicExcelWorksheet* sheet = e.GetWorksheet("Hunting");

    sheet->VisitAllRow(ReadHunting);
    
    system("pause");
    return 0;
}
```
