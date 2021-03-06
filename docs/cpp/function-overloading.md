---
title: 函数重载
ms.date: 11/19/2018
helpviewer_keywords:
- function overloading [C++], about function overloading
- function overloading
- declaring functions [C++], overloading
ms.assetid: 3c9884cb-1d5e-42e8-9a49-6f46141f929e
ms.openlocfilehash: c05e4b840a02b3d9bbcd4ed259509be4c35c22c2
ms.sourcegitcommit: 9e891eb17b73d98f9086d9d4bfe9ca50415d9a37
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2018
ms.locfileid: "52176297"
---
# <a name="function-overloading"></a>函数重载

C++ 允许同一范围内具有相同名称的多个函数的规范。 这些被称为*重载*函数。 重载的函数，可提供不同的语义，对于函数，具体取决于类型和数量的参数。

例如，`print`函数，它采用`std::string`自变量可能会执行与采用一个类型的参数非常不同的任务**double**。 重载使您无需使用如下所示名称`print_string`或`print_double`。 在编译时，编译器将选择要使用的重载基于由调用方所传递的参数类型。  如果您调用`print(42.0)`则`void print(double d)`将调用函数。 如果您调用`print("hello world")`则`void print(std::string)`重载将调用。

可重载成员函数和非成员函数。 下表显示了 C++ 使用函数声明的哪些部分来区分同一范围内具有相同名称的函数组。

### <a name="overloading-considerations"></a>重载注意事项

|函数声明元素|是否用于重载？|
|----------------------------------|---------------------------|
|函数返回类型|否|
|参数的数量|是|
|自变量的类型|是|
|省略号存在或缺失|是|
|利用**typedef**名称|否|
|未指定的数组边界|否|
|**const**或**易失性**|是的当应用于整个函数|
|[ref-qualifier](#ref-qualifier)|是|

## <a name="example"></a>示例

以下示例阐述如何使用重载。

```cpp
// function_overloading.cpp
// compile with: /EHsc
#include <iostream>
#include <math.h>
#include <string>

// Prototype three print functions.
int print(std::string s);             // Print a string.
int print(double dvalue);            // Print a double.
int print(double dvalue, int prec);  // Print a double with a
                                     //  given precision.
using namespace std;
int main(int argc, char *argv[])
{
    const double d = 893094.2987;
    if (argc < 2)
    {
        // These calls to print invoke print( char *s ).
        print("This program requires one argument.");
        print("The argument specifies the number of");
        print("digits precision for the second number");
        print("printed.");
        exit(0);
    }

    // Invoke print( double dvalue ).
    print(d);

    // Invoke print( double dvalue, int prec ).
    print(d, atoi(argv[1]));
}

// Print a string.
int print(string s)
{
    cout << s << endl;
    return cout.good();
}

// Print a double in default precision.
int print(double dvalue)
{
    cout << dvalue << endl;
    return cout.good();
}

//  Print a double in specified precision.
//  Positive numbers for precision indicate how many digits
//  precision after the decimal point to show. Negative
//  numbers for precision indicate where to round the number
//  to the left of the decimal point.
int print(double dvalue, int prec)
{
    // Use table-lookup for rounding/truncation.
    static const double rgPow10[] = {
        10E-7, 10E-6, 10E-5, 10E-4, 10E-3, 10E-2, 10E-1,
        10E0, 10E1,  10E2,  10E3,  10E4, 10E5,  10E6 };
    const int iPowZero = 6;

    // If precision out of range, just print the number.
    if (prec < -6 || prec > 7)
    {
        return print(dvalue);
    }
    // Scale, truncate, then rescale.
    dvalue = floor(dvalue / rgPow10[iPowZero - prec]) *
        rgPow10[iPowZero - prec];
    cout << dvalue << endl;
    return cout.good();
}
```

前面的代码演示了文件范围内的 `print` 函数重载。

默认自变量不被视为函数类型的一部分。 因此，它不用于选择重载函数。 仅在默认自变量上存在差异的两个函数被视为多个定义而不是重载函数。

不能为重载运算符提供默认自变量。

## <a name="argument-matching"></a>自变量匹配

选择重载函数以实现当前范围内的函数声明与函数调用中提供的自变量的最佳匹配。 如果找到合适的函数，则调用该函数。 此上下文中的“Suitable”具有下列含义之一：

- 找到完全匹配项。

- 已执行不重要的转换。

- 已执行整型提升。

- 已存在到所需自变量类型的标准转换。

- 已存在到所需自变量类型的用户定义的转换（转换运算符或构造函数）。

- 已找到省略号所表示的自变量。

编译器为每个自变量创建一组候选函数。 候选函数是这样一种函数，其中的实际自变量可以转换为形式自变量的类型。

为每个自变量生成一组“最佳匹配函数”，并且所选函数是所有集的交集。 如果交集包含多个函数，则重载是不明确的并会生成错误。 对于至少一个自变量而言，最终选择的函数始终是比组中的所有其他函数更好的匹配项。 如果不是这样（如果没有清晰的胜者)，则函数调用会生成错误。

考虑下面的声明（针对下面的讨论中的标识，将函数标记为 `Variant 1`、`Variant 2` 和 `Variant 3`）：

```cpp
Fraction &Add( Fraction &f, long l );       // Variant 1
Fraction &Add( long l, Fraction &f );       // Variant 2
Fraction &Add( Fraction &f, Fraction &f );  // Variant 3

Fraction F1, F2;
```

请考虑下列语句：

```cpp
F1 = Add( F2, 23 );
```

前面的语句生成两个集：

|集 1：其第一个自变量的类型为 Fraction 的候选函数|集 2： 候选函数其第二个自变量可转换为类型**int**|
|--------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
|Variant 1|Variant 1 (**int**可转换为**长**使用标准转换)|
|Variant 3||

集 2 中的函数是具有从实参类型到形参类型的隐式转换的函数，在这些函数中，有一种函数的从实参类型到其形参类型的转换的“成本”是最低的。

这两个集的交集为 Variant 1。 不明确的函数调用的示例为：

```cpp
F1 = Add( 3, 6 );
```

前面的函数调用生成以下集：

|集 1： 候选函数，具有第一个自变量的类型**int**|集 2： 候选函数，具有第二个自变量的类型**int**|
|---------------------------------------------------------------------|----------------------------------------------------------------------|
|Variant 2 (**int**可转换为**长**使用标准转换)|Variant 1 (**int**可转换为**长**使用标准转换)|

请注意，这两个集之间的交集为空。 因此，编译器会生成错误消息。

对于自变量匹配的函数*n*默认自变量将被视为*n*+ 1 个单独函数，每个都具有不同数目的参数。

省略号 (...) 用作通配符；它与任何自变量匹配。 如果您未极其谨慎地设计重载函数集，这可能导致产生许多不明确的集。

> [!NOTE]
>  重载函数的多义性无法确定，直到遇到函数调用。 此时，将为函数调用中的每个自变量生成集，并且可以确定是否存在明确的重载。 这意味着，多义性可保持在你的代码中，直到它们由特定函数调用引发。

## <a name="argument-type-differences"></a>自变量类型差异

重载函数区分使用不同的初始值设定项的自变量类型。 因此，对于重载而言，给定类型的自变量和对该类型的引用将视为相同。 由于它们采用相同的初始值设定项，因此它们被视为是相同的。 例如，`max( double, double )` 被视为与 `max( double &, double & )` 相同。 声明两个此类函数会导致错误。

出于相同原因，函数通过修改类型实参**const**或**易失性**不被看作是不同的基类型的重载的目的。

但是，函数重载机制可以区分由限定的引用**const**并**易失性**和对基类型的引用。 此方法可以编写诸如以下内容的代码：

```cpp
// argument_type_differences.cpp
// compile with: /EHsc /W3
// C4521 expected
#include <iostream>

using namespace std;
class Over {
public:
   Over() { cout << "Over default constructor\n"; }
   Over( Over &o ) { cout << "Over&\n"; }
   Over( const Over &co ) { cout << "const Over&\n"; }
   Over( volatile Over &vo ) { cout << "volatile Over&\n"; }
};

int main() {
   Over o1;            // Calls default constructor.
   Over o2( o1 );      // Calls Over( Over& ).
   const Over o3;      // Calls default constructor.
   Over o4( o3 );      // Calls Over( const Over& ).
   volatile Over o5;   // Calls default constructor.
   Over o6( o5 );      // Calls Over( volatile Over& ).
}
```

### <a name="output"></a>输出

```Output
Over default constructor
Over&
Over default constructor
const Over&
Over default constructor
volatile Over&
```

指向**const**并**易失性**对象也被视为不同的基类型的指针的重载的目的。

## <a name="argument-matching-and-conversions"></a>自变量匹配和转换

当编译器尝试根据函数声明中的参数匹配实际参数时，如果未找到任何确切匹配项，它可以提供标准转换或用户定义的转换来获取正确类型。 转换的应用程序受这些规则的限制：

- 不考虑包含多个用户定义的转换的转换序列。

- 不考虑可通过删除中间转换来缩短的转换序列。

最终的转换序列（如果有）称为最佳匹配序列。 有几种方法将对象的类型转换**int**键入**无符号长**使用标准转换 (中所述[标准转换](../cpp/standard-conversions.md)):

- 从转换**int**到**长**，然后从**长**到**无符号长**。

- 从转换**int**到**无符号长**。

第一个序列（尽管它实现了所需目标）不是最佳匹配序列 - 存在一个较短的序列。

下表显示了一组称为常用转换的转换，这些转换对确定哪个序列是最佳匹配项有一定的限制。 该表后面的列表中讨论了常用转换影响序列选择的实例。

### <a name="trivial-conversions"></a>常用转换

|从类型转换|转换为类型|
|-----------------------|---------------------|
|*type-name*|*类型名称* **&**|
|*类型名称* **&**|*type-name*|
|*type-name* **[ ]**|*类型名称* __\*__|
|*type-name* **(** *argument-list* **)**|**(** __\*__ *类型名称* **) (** *自变量列表* **)**|
|*type-name*|**const** *类型名称*|
|*type-name*|**易失***类型名称*|
|*类型名称* __\*__|**const** *类型名称* __\*__|
|*类型名称* __\*__|**易失***类型名称* __\*__|

在其中尝试转换的序列如下：

1. 完全匹配。 用于调用函数的类型与函数原型中声明的类型之间的完全匹配始终是最佳匹配。 常用转换的序列将归类为完全匹配。 但是，不进行任何转换的序列被视为比进行转换的序列更佳：

   - 从指针，指向**const** (`type` <strong>\*</strong>到**const** `type` <strong>\*</strong>).

   - 从指针，指向**可变**(`type` <strong>\*</strong>到**易失性** `type` <strong>\*</strong>).

   - 从引用，到对引用**const** (`type` **&** 到**const** `type` **&**).

   - 从引用，到对引用**可变**(`type` **&** 到**易失性** `type` **&**).

1. 使用提升的匹配。 未归类为完全匹配项包含仅整型提升、 从任何序列**float**到**double**，和常用转换归类为使用提升的匹配。 尽管比不上完全匹配，但使用提升的匹配仍优于使用标准转换的匹配。

1. 使用标准转换的匹配。 未归类为完全匹配或仅包含标准转换和常用转换的使用提升的匹配的序列将归类为使用标准转换的匹配。 在此类别中，以下规则将适用：

   - 从指针到派生类中，为指向直接或间接基类的转换优于将转换为`void *`或`const void *`。

   - 从指向派生类的指针到指向基类的指针的转换会产生一个到直接基类的更好匹配。 假定类层次结构如下图所示。

![首选转换的图形](../cpp/media/vc391t1.gif "首选转换的关系图") <br/>
该图表显示首选的转换

从 `D*` 类型到 `C*` 类型的转换优于从 `D*` 类型到 `B*` 类型的转换。 同样，从 `D*` 类型到 `B*` 类型的转换优于从 `D*` 类型到 `A*` 类型的转换。

此同一规则适用于引用转换。 从 `D&` 类型到 `C&` 类型的转换优于从 `D&` 类型到 `B&` 类型的转换等。

此同一规则适用于指向成员的指针转换。 从 `T D::*` 类型到 `T C::*` 类型的转换优于从 `T D::*` 类型到 `T B::*` 类型的转换等（其中，`T` 是该成员的类型）。

前面的规则仅沿派生的给定路径应用。 考虑下图中显示的关系图。

![多个&#45;显示首选的转换的继承](../cpp/media/vc391t2.gif "多&#45;显示首选的转换的继承") <br/>
显示首选的转换的多个继承关系图

从 `C*` 类型到 `B*` 类型的转换优于从 `C*` 类型到 `A*` 类型的转换。 原因是它们位于同一个路径上，且 `B*` 更为接近。 但是，从 `C*` 类型到 `D*` 类型的转换不优于到 `A*` 类型的转换；没有首选项，因为这些转换遵循不同的路径。

1. 使用用户定义的转换的匹配。 此序列不能归类为完全匹配、使用提升的匹配或使用标准转换的匹配。 序列必须仅包含用户定义的转换、标准转换或要归类为使用用户定义的转换的匹配的常用转换。 使用用户定义的转换的匹配被认为优于使用省略号的匹配，但比不上使用标准转换的匹配。

1. 使用省略号的匹配。 与声明中的省略号匹配的任何序列将归类为使用省略号的匹配。 这被视为最弱匹配。

如果内置提升或转换不存在，则用户定义的转换将适用。 基于将匹配的参数的类型选择这些转换。 考虑下列代码：

```cpp
// argument_matching1.cpp
class UDC
{
public:
   operator int()
   {
      return 0;
   }
   operator long();
};

void Print( int i )
{
};

UDC udc;

int main()
{
   Print( udc );
}
```

类可用的用户定义转换`UDC`来自类型**int**并键入**长**。 因此，编译器会考虑针对将匹配的对象类型的转换：`UDC`。 转换为**int**存在，且已被选中。

在匹配自变量的过程中，标准转换可应用于自变量和用户定义的转换的结果。 因此，下面的代码将适用：

```cpp
void LogToFile( long l );
...
UDC udc;
LogToFile( udc );
```

在前面的示例中，用户定义的转换**运算符长**，调用，以转换`udc`键入**长**。 如果没有用户定义的转换为类型**长**已定义，则转换将继续，如下所示： 类型`UDC`将转换为类型**int**使用用户定义转换。 从类型的标准转换**int**键入**长**会应用在声明自变量进行匹配。

如果需要任何用户定义的转换来匹配自变量，则在计算最佳匹配时不会使用标准转换。 即使多个候选函数需要用户定义的转换也是如此；在这种情况下，这些函数被认为是相等的。 例如：

```cpp
// argument_matching2.cpp
// C2668 expected
class UDC1
{
public:
   UDC1( int );  // User-defined conversion from int.
};

class UDC2
{
public:
   UDC2( long ); // User-defined conversion from long.
};

void Func( UDC1 );
void Func( UDC2 );

int main()
{
   Func( 1 );
}
```

这两个版本`Func`需要用户定义的转换将类型转换**int**到类类型参数。 可能的转换包括：

- 从类型转换**int**键入`UDC1`（用户定义转换）。

- 从类型转换**int**键入**长**; 然后转换为键入`UDC2`（一个两步转换）。

即使其中的第二个转换需要标准转换以及用户定义的转换，这两个转换仍被视为相等。

> [!NOTE]
>  用户定义的转换被认为是通过构造函数的转换或通过初始化的转换（转换函数）。 在考虑最佳匹配时，两个方法被认为是相等的。

## <a name="argument-matching-and-the-this-pointer"></a>自变量匹配和 this 指针

类成员函数均以不同的方式，具体取决于它们被声明为被视为**静态**。 因为非静态函数具有提供的隐式参数**这**指针，非静态函数视为比静态函数多一个参数; 否则，声明它们完全相同。

这些非静态成员函数要求隐含**这**指针与通过该函数被调用时，对象类型匹配，或者对于重载运算符，它们要求第一个参数匹配的对象正在应用运算符。 (有关重载运算符的详细信息，请参阅[重载运算符](../cpp/operator-overloading.md)。)

没有临时对象将引入与不同的重载函数中的其他参数，并且不会尝试转换尝试匹配时**这**指针自变量。

当`->`成员选择运算符用于访问类的成员函数`class_name`，则**这**指针自变量的类型为`class_name * const`。 如果成员声明为**const**或**易失性**，类型为`const class_name * const`和`volatile class_name * const`分别。

`.` 成员选择运算符以相同的方式工作，只不过隐式 `&` (address-of) 运算符将成为对象名称的前缀。 下面的示例演示了此工作原理：

```cpp
// Expression encountered in code
obj.name

// How the compiler treats it
(&obj)->name
```

处理 `->*` 和 `.*`（指向成员的指针）运算符的左操作数的方式与处理与参数匹配相关的 `.` 和 `->`（成员选择）运算符的方式相同。

## <a name="ref-qualifiers"></a> 成员函数上引用限定符

Ref 限定符，让可以根据是否指向对象的成员函数重载**这**是右值或左值。  此功能可用于避免不必要的复制方案中的操作选择不是为了提供对数据的指针访问。 例如，假定类`C`初始化其构造函数中的某些数据，并在成员函数中返回的数据的副本`get_data()`。 如果类型的对象`C`是为即将销毁，则编译器将选择的右值`get_data() &&`重载，这可将数据移动，而不是将其复制。

```cpp
#include <iostream>
#include <vector>

using namespace std;

class C
{

public:
    C() {/*expensive initialization*/}
    vector<unsigned> get_data() &
    {
        cout << "lvalue\n";
        return _data;
    }
    vector<unsigned> get_data() &&
    {
        cout << "rvalue\n";
        return std::move(_data);
    }

private:
    vector<unsigned> _data;
};

int main()
{
    C c;
    auto v = c.get_data(); // get a copy. prints "lvalue".
    auto v2 = C().get_data(); // get the original. prints "rvalue"
    return 0;
}
```

## <a name="restrictions-on-overloading"></a>重载的限制

多个限制管理可接受的重载函数集：

- 重载函数集内的任意两个函数必须具有不同的自变量列表。

- 仅基于返回类型重载具有相同类型的自变量列表的函数是错误的。

     **Microsoft 专用**

可重载**运算符 new**仅为基础的返回类型，具体而言，根据指定的内存模型修饰符。

**结束 Microsoft 专用**

- 不能只根据一个静态类型和一个非静态类型来重载成员函数。

- **typedef**声明不定义新类型; 它们引入现有类型的同义词。 它们不影响重载机制。 考虑下列代码：

    ```cpp
    typedef char * PSTR;

    void Print( char *szToPrint );
    void Print( PSTR szToPrint );
    ```

   前面的两个函数具有相同的自变量列表。 `PSTR` 是类型的同义词`char *`。 在成员范围内，此代码生成错误。

- 枚举类型是不同的类型，并且可用于区分重载函数。

- 就区分重载函数而言，类型“array of”和“pointer to”是等效的。 此情况仅适用于单维度数组。 因此，以下重载函数会发生冲突并生成错误消息：

    ```cpp
    void Print( char *szToPrint );
    void Print( char szToPrint[] );
    ```

   对于多维数组，第二个和后续维度被视为类型的一部分。 因此，它们可用来区分重载函数：

    ```cpp
    void Print( char szToPrint[] );
    void Print( char szToPrint[][7] );
    void Print( char szToPrint[][9][42] );
    ```

## <a name="overloading-overriding-and-hiding"></a>重载、 重写和隐藏

同一范围内具有同一名称的任何两个函数声明都可以引用同一函数或重载的两个不同的函数。 如果声明的自变量列表包含等效类型的自变量（如上一节所述），函数声明将引用同一函数。 否则，它们将引用使用重载选择的两个不同的函数。

需要严格遵守类范围；因此，在基类中声明的函数与在派生类中声明的函数不在同一范围内。 如果使用与基类派生类函数中的虚函数相同的名称声明派生类中的函数*重写*基类函数。 有关详细信息，请参阅[虚函数](../cpp/virtual-functions.md)。

如果基类函数未声明为虚拟的，则派生的类函数可以说负责*隐藏*它。 重写和隐藏都是不同于重载。

需要严格遵守块范围；因此，在文件范围中声明的函数与在本地声明的函数不在同一范围内。 如果在本地声明的函数与在文件范围中声明的函数具有相同名称，则在本地声明的函数将隐藏文件范围内的函数而不是导致重载。 例如:

```cpp
// declaration_matching1.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
void func( int i )
{
    cout << "Called file-scoped func : " << i << endl;
}

void func( char *sz )
{
   cout << "Called locally declared func : " << sz << endl;
}

int main()
{
   // Declare func local to main.
   extern void func( char *sz );

   func( 3 );   // C2664 Error. func( int ) is hidden.
   func( "s" );
}
```

前面的代码显示函数 `func` 中的两个定义。 使用类型的自变量的定义`char *`局部`main`由于**extern**语句。 因此，使用类型的自变量的定义**int**处于隐藏状态，并在首次调用`func`出现错误。

对于重载的成员函数，不同版本的函数可能获得不同的访问权限。 它们仍被视为在封闭类的范围内，因此是重载函数。 请考虑下面的代码，其中的成员函数 `Deposit` 将重载；一个版本是公共的，另一个版本是私有的。

此示例的目的是提供一个 `Account` 类，其中需要正确的密码来执行存款。 使用重载可完成此操作。

请注意，对 `Deposit` 中的 `Account::Deposit` 的调用将调用私有成员函数。 此调用是正确的，因为 `Account::Deposit` 是成员函数，因而可以访问类的私有成员。

```cpp
// declaration_matching2.cpp
class Account
{
public:
   Account()
   {
   }
   double Deposit( double dAmount, char *szPassword );

private:
   double Deposit( double dAmount )
   {
      return 0.0;
   }
   int Validate( char *szPassword )
   {
      return 0;
   }

};

int main()
{
    // Allocate a new object of type Account.
    Account *pAcct = new Account;

    // Deposit $57.22. Error: calls a private function.
    // pAcct->Deposit( 57.22 );

    // Deposit $57.22 and supply a password. OK: calls a
    //  public function.
    pAcct->Deposit( 52.77, "pswd" );
}

double Account::Deposit( double dAmount, char *szPassword )
{
   if ( Validate( szPassword ) )
      return Deposit( dAmount );
   else
      return 0.0;
}
```

## <a name="see-also"></a>请参阅

[函数 (C++)](../cpp/functions-cpp.md)