---
title: '方法: ネイティブ関数の参照クラスを変更する'
ms.custom: get-started-article
ms.date: 11/04/2016
helpviewer_keywords:
- platform invoke, reference class
- reference types, modifying in a C++ native function
ms.assetid: c701145b-62a0-4c4b-b32a-db8d69a59720
ms.openlocfilehash: a9ff21390f8a5d7b20c8c36e596f80140ccb9a39
ms.sourcegitcommit: c1fd917a8c06c6504f66f66315ff352d0c046700
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2020
ms.locfileid: "90683950"
---
# <a name="how-to-modify-reference-class-in-a-native-function"></a>方法: ネイティブ関数の参照クラスを変更する

CLR 配列を含む参照クラスをネイティブ関数に渡し、PInvoke サービスを使用してクラスを変更できます。

## <a name="examples"></a>例

次のネイティブライブラリをコンパイルします。

```cpp
// modify_ref_class_in_native_function.cpp
// compile with: /LD
#include <stdio.h>
#include <windows.h>

struct S {
   wchar_t* str;
   int intarr[2];
};

extern "C"  {
   __declspec(dllexport) int bar(S* param) {
      printf_s("str: %S\n", param->str);
      fflush(stdin);
      fflush(stdout);
      printf_s("In native: intarr: %d, %d\n",
                param->intarr[0], param->intarr[1]);
      fflush(stdin);
      fflush(stdout);
      param->intarr[0]=300;param->intarr[1]=400;
      return 0;
    }
};
```

次のアセンブリをコンパイルします。

```cpp
// modify_ref_class_in_native_function_2.cpp
// compile with: /clr
using namespace System;
using namespace System::Runtime::InteropServices;

[StructLayout(LayoutKind::Sequential, CharSet = CharSet::Unicode)]
ref class S  {
public:
   [MarshalAsAttribute(UnmanagedType::LPWStr)]
   String ^ str;
   [MarshalAsAttribute(UnmanagedType::ByValArray,
        ArraySubType=UnmanagedType::I4, SizeConst=2)]
   array<Int32> ^ intarr;
};

[DllImport("modify_ref_class_in_native_function.dll",
           CharSet=CharSet::Unicode)]
int bar([In][Out] S ^ param);

int main() {
   S ^ param = gcnew S;
   param->str = "Hello";
   param->intarr = gcnew array<Int32>(2);
   param->intarr[0] = 100;
   param->intarr[1] = 200;
   bar(param);   // Call to native function
   Console::WriteLine("In managed: intarr: {0}, {1}",
                       param->intarr[0], param->intarr[1]);
}
```

```Output
str: Hello
In native: intarr: 100, 200
In managed: intarr: 300, 400
```

## <a name="see-also"></a>関連項目

[C++ Interop (暗黙の PInvoke) の使用](../dotnet/using-cpp-interop-implicit-pinvoke.md)
