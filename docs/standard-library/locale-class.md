---
title: locale クラス
ms.date: 07/20/2020
f1_keywords:
- xlocale/std::locale
- xlocale/std::locale::category
- xlocale/std::locale::combine
- xlocale/std::locale::name
- xlocale/std::locale::classic
- xlocale/std::locale::global
- xlocale/std::locale::operator( )
- xlocale/std::locale::facet
- xlocale/std::locale::id
helpviewer_keywords:
- std::locale [C++]
- std::locale [C++], category
- std::locale [C++], combine
- std::locale [C++], name
- std::locale [C++], classic
- std::locale [C++], global
- std::locale [C++], facet
- std::locale [C++], id
ms.assetid: 7dd6d271-472d-4750-8fb5-ea8f55fbef62
ms.openlocfilehash: 55aeaf27b1c31ef0dba68d0ead3633590777cbdf
ms.sourcegitcommit: 6280a4c629de0f638ebc2edd446de2a9b11f0406
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2020
ms.locfileid: "90040602"
---
# <a name="locale-class"></a>locale クラス

特定のローカライズされた環境を集合的に定義する一連のファセットとして、カルチャ固有の情報をカプセル化するロケール オブジェクトを表すクラス。

## <a name="syntax"></a>構文

```cpp
class locale;
```

## <a name="remarks"></a>解説

ファセットは、次の形式のパブリック オブジェクトがある、[facet](#facet_class) クラスから派生したクラスのオブジェクトへのポインターです。

```cpp
static locale::id id;
```

制約のない一連のファセットを定義できます。 任意の数のファセットを指定するロケール オブジェクトを構築することもできます。

これらのファセットの定義済みのグループは、従来の標準 C ライブラリでは `setlocale` 関数で管理されていた[ロケールのカテゴリ](#category)を表します。

Category `collate` (LC_COLLATE) には、次のファセットが含まれます。

```cpp
collate<char>
collate<wchar_t>
```

Category `ctype` (LC_CTYPE) には、次のファセットが含まれます。

```cpp
ctype<char>
ctype<wchar_t>
codecvt<char, char, mbstate_t>
codecvt<wchar_t, char, mbstate_t>
codecvt<char16_t, char, mbstate_t>
codecvt<char32_t, char, mbstate_t>
```

Category `monetary` (LC_MONETARY) には、次のファセットが含まれます。

```cpp
moneypunct<char, false>
moneypunct<wchar_t, false>
moneypunct<char, true>
moneypunct<wchar_t, true>
money_get<char, istreambuf_iterator<char>>
money_get<wchar_t, istreambuf_iterator<wchar_t>>
money_put<char, ostreambuf_iterator<char>>
money_put<wchar_t, ostreambuf_iterator<wchar_t>>
```

Category `numeric` (LC_NUMERIC) には、次のファセットが含まれます。

```cpp
num_get<char, istreambuf_iterator<char>>
num_get<wchar_t, istreambuf_iterator<wchar_t>>
num_put<char, ostreambuf_iterator<char>>
num_put<wchar_t, ostreambuf_iterator<wchar_t>>
numpunct<char>
numpunct<wchar_t>
```

Category `time` (LC_TIME) には、次のファセットが含まれます。

```cpp
time_get<char, istreambuf_iterator<char>>
time_get<wchar_t, istreambuf_iterator<wchar_t>>
time_put<char, ostreambuf_iterator<char>>
time_put<wchar_t, ostreambuf_iterator<wchar_t>>
```

Category `messages` (LC_MESSAGES) には、次のファセットが含まれます。

```cpp
messages<char>
messages<wchar_t>
```

(最後のカテゴリは POSIX では必須ですが、C 標準には必要ありません)。

これらの定義済みのファセットの一部は、 `iostream` テキストシーケンスとの間での数値の変換を制御するために、クラスによって使用されます。

クラス ロケールのオブジェクトは、ロケール名を [string](../standard-library/string-typedefs.md#string) クラスのオブジェクトとして格納します。 無効なロケール名を使用してロケールのファセットまたはロケール オブジェクトを構築すると、[runtime_error](../standard-library/runtime-error-class.md) クラスのオブジェクトがスローされます。 `"*"`ロケールオブジェクトが、C スタイルのロケールがオブジェクトによって表されるロケールと完全に対応していることを特定できない場合、格納されるロケール名はです。 それ以外の場合は、名前を呼び出すことによって、標準 C ライブラリ内でロケールオブジェクトに対応するロケールを設定でき `locale_object` `setlocale(LC_ALL , locale_object.` [name](#name) `().c_str())` ます。

この実装では、次の静的メンバー関数を呼び出すことによって、

```cpp
static locale empty();
```

ファセットがないロケール オブジェクトを構築することもできます。 透過的なロケールでもあります。 テンプレート関数が use_facet [has_facet](../standard-library/locale-functions.md#has_facet)で[use_facet](../standard-library/locale-functions.md#use_facet) 、要求されたファセットが透過的なロケールで見つからない場合は、最初にグローバルロケールを参照し、次に、それが透過的な場合はクラシックロケールを参照します。 そのため、次のように記述できます。

```cpp
cout.imbue(locale::empty());
```

後続のへの挿入 [`cout`](../standard-library/iostream.md#cout) は、グローバルロケールの現在の状態によって仲介されます。 次のように記述することもできます。

```cpp
locale loc(locale::empty(),
    locale::classic(),
    locale::numeric);

cout.imbue(loc);
```

`cout` への以降の挿入についての数値書式設定規則は、グローバル ロケールで日付や金額の挿入についての変更規則が提供されている場合でも、C のロケールの場合と同様です。

### <a name="constructors"></a>コンストラクター

|コンストラクター|説明|
|-|-|
|[locale](#locale)|ロケール、ロケールのコピー、またはファセットやカテゴリが別のロケールのファセットやカテゴリで置換されたロケールのコピーを作成します。|

### <a name="typedefs"></a>Typedefs

|型名|説明|
|-|-|
|[category](#category)|標準ファセット ファミリを示すビットマスク値を指定する整数型。|

### <a name="member-functions"></a>メンバー関数

|メンバー関数|説明|
|-|-|
|[結合](#combine)|ターゲット ロケールに指定されたロケールのファセットを挿入します。|
|[name](#name)|格納されているロケール名を返します。|

### <a name="static-functions"></a>静的関数

|Name|説明|
|-|-|
|[classic](#classic)|この静的メンバー関数は、クラシック C ロケールを表すロケール オブジェクトを返します。|
|[global](#global)|プログラムの既定のロケールをリセットします。|

### <a name="operators"></a>オペレーター

|演算子|説明|
|-|-|
|[operator =](#op_eq)|ロケールを割り当てます。|
|[operator! =](#op_neq)|2 つのロケールが等しくないかどうかをテストします。|
|[operator ()](#op_call)|2 つの `basic_string` オブジェクトを比較します。|
|[operator = =](#op_eq_eq)|2 つのロケールが等しいかどうかをテストします。|

### <a name="classes"></a>クラス

|クラス|説明|
|-|-|
|[facet](#facet_class)|すべてのロケールのファセットの基底クラスとして機能するクラス。|
|[`id`](#id_class)|このメンバー クラスは、ロケール内でファセットを検索するためのインデックスとして使用される一意のファセット ID を提供します。|

## <a name="requirements"></a>要件

**ヘッダー:**\<locale>

**名前空間:** std

## <a name="localecategory"></a><a name="category"></a> locale:: category

標準ファセット ファミリを示すビットマスク値を指定する整数型。

```cpp
typedef int category;
static const int collate = LC_COLLATE;
static const int ctype = LC_CTYPE;
static const int monetary = LC_MONETARY;
static const int numeric = LC_NUMERIC;
static const int time = LC_TIME;
static const int messages = LC_MESSAGES;
static const int all = LC_ALL;
static const int none = 0;
```

### <a name="remarks"></a>注釈

この型は、 **`int`** クラスロケールに対してローカルなビットマスク型の個別の要素のグループを表すことができる型のシノニムです。または、対応する C ロケールカテゴリのいずれかを表すために使用できます。 要素は次のとおりです。

- `collate`。 C カテゴリに対応する LC_COLLATE

- `ctype`。 C カテゴリに対応する LC_CTYPE

- `monetary`。 C カテゴリに対応する LC_MONETARY

- `numeric`。 C カテゴリに対応する LC_NUMERIC

- `time`。 C カテゴリに対応する LC_TIME

- `messages`POSIX カテゴリに対応する LC_MESSAGES

次の2つの便利な値があります。

- `none`。 C カテゴリのいずれにも対応しません。

- `all`。すべてのカテゴリの C 共用体に対応 LC_ALL

`OR`&#124; のように、これらの定数と共にを使用すると、任意のカテゴリグループを表すことができ `monetary` `time` ます。

## <a name="localeclassic"></a><a name="classic"></a> locale:: classic

この静的メンバー関数は、クラシック C ロケールを表すロケール オブジェクトを返します。

```cpp
static const locale& classic();
```

### <a name="return-value"></a>戻り値

C ロケールへの参照。

### <a name="remarks"></a>注釈

Classic C ロケールは、標準 C ライブラリ内の米国英語の ASCII ロケールです。 これは、国際化されていないプログラムで暗黙的に使用されるロケールです。

### <a name="example"></a>例

```cpp
// locale_classic.cpp
// compile with: /EHsc
#include <iostream>
#include <string>
#include <locale>

using namespace std;

int main( )
{
   locale loc1( "german" );
   locale loc2 = locale::global( loc1 );
   cout << "The name of the previous locale is: " << loc2.name( )
        << "." << endl;
   cout << "The name of the current locale is: " << loc1.name( )
        << "." << endl;

   if (loc2 == locale::classic( ) )
      cout << "The previous locale was classic." << endl;
   else
      cout << "The previous locale was not classic." << endl;

   if (loc1 == locale::classic( ) )
      cout << "The current locale is classic." << endl;
   else
      cout << "The current locale is not classic." << endl;
}
```

```Output
The name of the previous locale is: C.
The name of the current locale is: German_Germany.1252.
The previous locale was classic.
The current locale is not classic.
```

## <a name="localecombine"></a><a name="combine"></a> locale:: 結合

ターゲット ロケールに指定されたロケールのファセットを挿入します。

```cpp
template <class Facet>
locale combine(const locale& source_locale) const;
```

### <a name="parameters"></a>パラメーター

*source_locale*\
ターゲット ロケールに挿入されるファセットを含むロケール。

### <a name="return-value"></a>戻り値

** \* この**メンバー関数は、 `Facet` *source_locale*に示されているファセットをで置換または追加するロケールオブジェクトを返します。

### <a name="example"></a>例

```cpp
// locale_combine.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <tchar.h>
using namespace std;

int main() {
   locale loc ( "German_germany" );
   _TCHAR * s1 = _T("Das ist wei\x00dfzz."); // \x00df is the German sharp-s; it comes before z in the German alphabet
   _TCHAR * s2 = _T("Das ist weizzz.");
   int result1 = use_facet<collate<_TCHAR> > ( loc ).
      compare (s1, &s1[_tcslen( s1 )-1 ],  s2, &s2[_tcslen( s2 )-1 ] );
   cout << isalpha (_T ( '\x00df' ), loc ) << result1 << endl;

   locale loc2 ( "C" );
   int result2 = use_facet<collate<_TCHAR> > ( loc2 ).
      compare (s1, &s1[_tcslen( s1 )-1 ],  s2, &s2[_tcslen( s2 )-1 ] );
   cout << isalpha (_T ( '\x00df' ), loc2 )  << result2 << endl;

   locale loc3 = loc2.combine<collate<_TCHAR> > (loc);
   int result3 = use_facet<collate<_TCHAR> > ( loc3 ).
      compare (s1, &s1[_tcslen( s1 )-1 ],  s2, &s2[_tcslen( s2 )-1 ] );
   cout << isalpha (_T ( '\x00df' ), loc3 ) << result3 << endl;
}
```

## <a name="facet-class"></a><a name="facet_class"></a> ファセットクラス

すべてのロケールのファセットの基底クラスとして機能するクラス。

```cpp
class facet {
protected:
    explicit facet(size_t references = 0);
    virtual ~facet();
private:
    facet(const facet&) // not defined
    void operator=(const facet&) // not defined
};
```

### <a name="remarks"></a>注釈

クラスのオブジェクトをコピーしたり、割り当てたりすることはできません `facet` 。 クラス `locale::facet` から派生したオブジェクトは構築および破棄できますが、厳密な意味での基底クラスのオブジェクトは構築および破棄できません。 通常は、を構築する `_Myfac` ときにから派生したオブジェクトを構築します。 `facet` `locale``locale loc(locale::classic(), new _Myfac);`

このような場合、基底クラスのコンストラクターには、 `facet` ゼロ *参照* 引数が必要です。 オブジェクトが不要になった場合は削除されます。そのため、オブジェクトの有効期間に対して責任があるまれなケースでのみ、0以外の *参照* 引数を指定します。

## <a name="localeglobal"></a><a name="global"></a> locale:: global

プログラムの既定のロケールをリセットします。 この呼び出しは、C と C++ の両方のグローバルロケールに影響します。

```cpp
static locale global(const locale& new_default_locale);
```

### <a name="parameters"></a>パラメーター

*new_default_locale*\
プログラムによって既定のロケールとして使用されるロケール。

### <a name="return-value"></a>戻り値

既定のロケールがリセットされる前の以前のロケール。

### <a name="remarks"></a>注釈

プログラムの起動時には、グローバル ロケールはクラシック ロケールと同じです。 `global()` 関数は `setlocale( LC_ALL, loc.name. c_str())` を呼び出して、標準 C ライブラリ内で一致するロケールを設定します。

### <a name="example"></a>例

```cpp
// locale_global.cpp
// compile by using: /EHsc
#include <locale>
#include <iostream>
#include <tchar.h>
using namespace std;

int main( )
{
   locale loc ( "German_germany" );
   locale loc1;
   cout << "The initial locale is: " << loc1.name( ) << endl;
   locale loc2 = locale::global ( loc );
   locale loc3;
   cout << "The current locale is: " << loc3.name( ) << endl;
   cout << "The previous locale was: " << loc2.name( ) << endl;
}
```

```Output
The initial locale is: C
The current locale is: German_Germany.1252
The previous locale was: C
```

## <a name="id-class"></a><a name="id_class"></a> id クラス

このメンバー クラスは、ロケール内でファセットを検索するためのインデックスとして使用される一意のファセット ID を提供します。

```cpp
class id
{
   protected:    id();
   private:      id(const id&)
   void operator=(const id&)  // not defined
};
```

### <a name="remarks"></a>注釈

このメンバー クラスは、一意の各ロケール ファセットに必要な静的メンバー オブジェクトを表します。 クラスのオブジェクトをコピーしたり、割り当てたりすることはできません `id` 。

## <a name="localelocale"></a><a name="locale"></a> locale:: locale

ロケール、ロケールのコピー、またはファセットやカテゴリが別のロケールのファセットやカテゴリで置換されたロケールのコピーを作成します。 には、デストラクターも含まれています。

```cpp
locale();

explicit locale(const char* locale_name, category new_category = all);
explicit locale(const string& locale_name);
locale(const locale& from_locale);
locale(const locale& from_locale, const locale& Other, category new_category);
locale(const locale& from_locale, const char* locale_name, category new_category);

template <class Facet>
locale(const locale& from_locale, const Facet* new_facet);

~locale();
```

### <a name="parameters"></a>パラメーター

*locale_name*\
ロケールの名前。

*from_locale*\
新しいロケールを構築する際にコピーされるロケール。

*他の*\
カテゴリの選択元となるロケール。

*new_category*\
構築されるロケール内での置換後のカテゴリ。

*new_facet*\
構築されるロケール内での置換後のファセット。

### <a name="remarks"></a>注釈

最初のコンストラクターは、グローバル ロケールと一致するようにオブジェクトを初期化します。 2番目と3番目のコンストラクターは、すべてのロケールカテゴリを初期化して、ロケール名 *locale_name*との動作が一致するようにします。 残りのコンストラクターは *from_locale*をコピーします。ただし、次の点に注意してください。

`locale(const locale& from_locale, const locale& Other, category new_category);`

C & *new_category*が0以外のカテゴリ c に対応する*他の*ファセットを置き換えます。

`locale(const locale& from_locale, const char* locale_name, category new_category);`

`locale(const locale& from_locale, const string& locale_name, category new_category);`

`locale(locale_name, all)`カテゴリ*replace_category*に対応するファセットから、が0以外のものに置き換え `replace_category & new_category` ます。

`template<class Facet> locale(const locale& from_locale, Facet* new_facet);`

*new_facet*が null ポインターではない場合は、ファセット*new_facet* *from_locale*を (またはに追加して) 置換します。

ロケール名 *locale_name* が null ポインターである場合、または無効な場合、関数は [runtime_error](../standard-library/runtime-error-class.md)をスローします。

### <a name="example"></a>例

```cpp
// locale_locale.cpp
// compile with: /EHsc
#include <locale>
#include <iostream>
#include <tchar.h>
using namespace std;

int main( ) {

   // Second constructor
   locale loc ( "German_germany" );
   _TCHAR * s1 = _T("Das ist wei\x00dfzz."); // \x00df is the German sharp-s, it comes before z in the German alphabet
   _TCHAR * s2 = _T("Das ist weizzz.");
   int result1 = use_facet<collate<_TCHAR> > ( loc ).
      compare (s1, &s1[_tcslen( s1 )-1 ],  s2, &s2[_tcslen( s2 )-1 ] );
   cout << isalpha (_T ( '\x00df' ), loc ) << result1 << endl;

   // The first (default) constructor
   locale loc2;
   int result2 = use_facet<collate<_TCHAR> > ( loc2 ).
      compare (s1, &s1[_tcslen( s1 )-1 ],  s2, &s2[_tcslen( s2 )-1 ] );
   cout << isalpha (_T ( '\x00df' ), loc2 )  << result2 << endl;

   // Third constructor
   locale loc3 (loc2,loc, _M_COLLATE );
   int result3 = use_facet<collate<_TCHAR> > ( loc3 ).
      compare (s1, &s1[_tcslen( s1 )-1 ],  s2, &s2[_tcslen( s2 )-1 ] );
   cout << isalpha (_T ( '\x00df' ), loc3 ) << result3 << endl;

   // Fourth constructor
   locale loc4 (loc2, "German_Germany", _M_COLLATE );
   int result4 = use_facet<collate<_TCHAR> > ( loc4 ).
      compare (s1, &s1[_tcslen( s1 )-1 ],  s2, &s2[_tcslen( s2 )-1 ] );
   cout << isalpha (_T ( '\x00df' ), loc4 ) << result4 << endl;
}
```

## <a name="localename"></a><a name="name"></a> locale:: name

格納されているロケール名を返します。

```cpp
string name() const;
```

### <a name="return-value"></a>戻り値

ロケールの名前を指定する文字列。

### <a name="example"></a>例

```cpp
// locale_name.cpp
// compile with: /EHsc
#include <iostream>
#include <string>
#include <locale>

using namespace std;

int main( )
{
   locale loc1( "german" );
   locale loc2 = locale::global( loc1 );
   cout << "The name of the previous locale is: "
        << loc2.name( ) << "." << endl;
   cout << "The name of the current locale is: "
        << loc1.name( ) << "." << endl;
}
```

```Output
The name of the previous locale is: C.
The name of the current locale is: German_Germany.1252.
```

## <a name="localeoperator"></a><a name="op_eq"></a> locale:: operator =

ロケールを割り当てます。

```cpp
const locale& operator=(const locale& other) noexcept;
```

## <a name="localeoperator"></a><a name="op_neq"></a> locale:: operator! =

2 つのロケールが等しくないかどうかをテストします。

```cpp
bool operator!=(const locale& right) const;
```

### <a name="parameters"></a>パラメーター

*そうです*\
不等性をテストする一方のロケール。

### <a name="return-value"></a>戻り値

**`true`** ロケールが同じロケールのコピーでない場合は、ブール値。 ロケールが **`false`** 同じロケールのコピーである場合は、

### <a name="remarks"></a>注釈

2つのロケールは、それらが同じロケールである場合、一方が他方のコピーである場合、または同じ名前を持つ場合に等しくなります。

### <a name="example"></a>例

```cpp
// locale_op_ne.cpp
// compile with: /EHsc
#include <iostream>
#include <string>
#include <locale>

using namespace std;

int main( )
{
   locale loc1( "German_Germany" );
   locale loc2( "German_Germany" );
   locale loc3( "English" );

   if ( loc1 != loc2 )
      cout << "locales loc1 (" << loc1.name( )
      << ") and\n loc2 (" << loc2.name( ) << ") are not equal." << endl;
   else
      cout << "locales loc1 (" << loc1.name( )
      << ") and\n loc2 (" << loc2.name( ) << ") are equal." << endl;

   if ( loc1 != loc3 )
      cout << "locales loc1 (" << loc1.name( )
      << ") and\n loc3 (" << loc3.name( ) << ") are not equal." << endl;
   else
      cout << "locales loc1 (" << loc1.name( )
      << ") and\n loc3 (" << loc3.name( ) << ") are equal." << endl;
}
```

```Output
locales loc1 (German_Germany.1252) and
loc2 (German_Germany.1252) are equal.
locales loc1 (German_Germany.1252) and
loc3 (English_United States.1252) are not equal.
```

## <a name="localeoperator"></a><a name="op_call"></a> locale:: operator ()

`basic_string`このロケールのファセットで定義されている辞書式比較規則に従って、2つのオブジェクトを比較し `std::collate<charT>` ます。

```cpp
template <class CharType, class Traits, class Allocator>
bool operator()(
    const basic_string<CharType, Traits, Allocator>& left,
    const basic_string<CharType, Traits, Allocator>& right) const;
```

### <a name="parameters"></a>パラメーター

*左側*\
比較する最初の文字列。

*そうです*\
比較する 2 番目の文字列。

### <a name="return-value"></a>戻り値

- **`true`***left*が辞書式未満の場合*は、それ以外の場合*は **`false`** 。

### <a name="remarks"></a>注釈

このメンバー関数は、実質的に次の内容を実行します。

```cpp
const collate<CharType>& fac = use_fac<collate<CharType>>(*this);

return (fac.compare(left.begin(), left.end(), right.begin(), right.end()) < 0);
```

これは、locale オブジェクトを関数オブジェクトとして使用できることを意味します。

### <a name="example"></a>例

```cpp
// locale_op_compare.cpp
// compile with: /EHsc
#include <iostream>
#include <string>
#include <locale>

int main( )
{
   using namespace std;
   const wchar_t *sa = L"ztesting";
   const wchar_t *sb = L"\0x00DFtesting";
   basic_string<wchar_t> a( sa );
   basic_string<wchar_t> b( sb );

   locale loc( "German_Germany" );
   cout << loc( a,b ) << endl;

   const collate<wchar_t>& fac = use_facet<collate<wchar_t> >( loc );
   cout << ( fac.compare( sa, sa + a.length( ),
       sb, sb + b.length( ) ) < 0) << endl;
}
```

```Output
0
0
```

## <a name="localeoperator"></a><a name="op_eq_eq"></a> locale:: operator = =

2 つのロケールが等しいかどうかをテストします。

```cpp
bool operator==(const locale& right) const;
```

### <a name="parameters"></a>パラメーター

*そうです*\
等しいかどうかをテストする一方のロケール。

### <a name="return-value"></a>戻り値

**`true`** ロケールが同じロケールのコピーである場合は、ブール値。 **`false`** ロケールが同じロケールのコピーではない場合です。

### <a name="remarks"></a>注釈

2つのロケールは、それらが同じロケールである場合、一方が他方のコピーである場合、または同じ名前を持つ場合に等しくなります。

### <a name="example"></a>例

```cpp
// locale_op_eq.cpp
// compile with: /EHsc
#include <iostream>
#include <string>
#include <locale>

using namespace std;

int main( )
{
   locale loc1( "German_Germany" );
   locale loc2( "German_Germany" );
   locale loc3( "English" );

   if ( loc1 == loc2 )
      cout << "locales loc1 (" << loc1.name( )
      << ")\n and loc2 (" << loc2.name( ) << ") are equal."
      << endl;
   else
      cout << "locales loc1 (" << loc1.name( )
      << ")\n and loc2 (" << loc2.name( ) << ") are not equal."
      << endl;

   if ( loc1 == loc3 )
      cout << "locales loc1 (" << loc1.name( )
      << ")\n and loc3 (" << loc3.name( ) << ") are equal."
      << endl;
   else
      cout << "locales loc1 (" << loc1.name( )
      << ")\n and loc3 (" << loc3.name( ) << ") are not equal."
      << endl;
}
```

```Output
locales loc1 (German_Germany.1252)
and loc2 (German_Germany.1252) are equal.
locales loc1 (German_Germany.1252)
and loc3 (English_United States.1252) are not equal.
```

## <a name="see-also"></a>関連項目

[\<locale>](../standard-library/locale.md)\
[コードページ](../c-runtime-library/code-pages.md)\
[ロケール名、言語、および国/地域識別文字列](../c-runtime-library/locale-names-languages-and-country-region-strings.md)\
[C++ 標準ライブラリのスレッドセーフ](../standard-library/thread-safety-in-the-cpp-standard-library.md)
