---
title: ATL テキストエンコーディング関数
ms.date: 11/04/2016
f1_keywords:
- atlbase/ATL::AtlGetHexValue
- atlbase/ATL::AtlGetVersion
- atlenc/ATL::AtlHexDecode
- atlenc/ATL::AtlHexDecodeGetRequiredLength
- atlenc/ATL::AtlHexEncode
- atlenc/ATL::AtlHexEncodeGetRequiredLength
- atlenc/ATL::AtlHexValue
- atlenc/ATL::BEncode
- atlenc/ATL::BEncodeGetRequiredLength
- atlenc/ATL::EscapeXML
- atlenc/ATL::GetExtendedChars
- atlenc/ATL::IsExtendedChar
- atlenc/ATL::QEncode
- atlenc/ATL::QEncodeGetRequiredLength
- atlenc/ATL::QPDecode
- atlenc/ATL::QPDecodeGetRequiredLength
- atlenc/ATL::QPEncode
- atlenc/ATL::QPEncodeGetRequiredLength
- atlenc/ATL::UUDecode
- atlenc/ATL::UUDecodeGetRequiredLength
- atlenc/ATL::UUEncode
- atlenc/ATL::UUEncodeGetRequiredLength
ms.assetid: 2ae1648b-2b87-4112-92aa-0069fcfd23da
ms.openlocfilehash: 330a73e0d41bf384a799635d5f2e6f09f7e3dd03
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88833856"
---
# <a name="atl-text-encoding-functions"></a>ATL テキストエンコーディング関数

これらの関数は、テキストのエンコードとデコードをサポートします。

|関数|説明|
|-|-|
|[AtlGetHexValue](#atlgethexvalue)|16 進数の数値を取得します。|
|[AtlGetVersion](#atlgetversion)|使用している ATL ライブラリのバージョンを取得するには、この関数を呼び出します。  |
|[AtlHexDecode](#atlhexdecode)|[AtlHexEncode](#atlhexencode)の以前の呼び出しによって、16進数のテキストとしてエンコードされたデータの文字列をデコードします。|
|[AtlHexDecodeGetRequiredLength](#atlhexdecodegetrequiredlength)|指定した長さの 16 進エンコードされた文字列からデコードされたデータを格納できるバッファーのサイズを、バイト単位で取得します。|
|[AtlHexEncode](#atlhexencode)|一部のデータを 16 進テキストの文字列としてエンコードします。|
|[AtlHexEncodeGetRequiredLength](#atlhexencodegetrequiredlength)|指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。|
|[AtlHexValue](#atlhexvalue)|16 進数の数値を取得します。 |
|[AtlUnicodeToUTF8](#atlunicodetoutf8)|Unicode 文字列を UTF-8 に変換します。 |
|[BEncode](#bencode)|"B" エンコーディングを使用して一部のデータを変換します。|
|[BEncodeGetRequiredLength](#bencodegetrequiredlength)|指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。|
|[EscapeXML](#escapexml)|XML での使用には安全でない文字を安全な文字に変換します。|
|[GetExtendedChars](#getextendedchars)|文字列に含まれる拡張文字の数を取得します。|
|[IsExtendedChar](#isextendedchar)|この関数を呼び出して、特定の文字が拡張文字 (32 未満、126より大きい、タブ、ラインフィード、またはキャリッジリターンではない) であるかどうかを確認します。|
|[QEncode](#qencode)|"Q" エンコーディングを使用して一部のデータを変換します。  |
|[QEncodeGetRequiredLength](#qencodegetrequiredlength)|指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。|
|[QPDecode](#qpdecode)|前回の [qの](#qpencode)呼び出しによってなど、引用符で囲まれた印刷可能な形式でエンコードされたデータの文字列をデコードします。|
|[QPDecodeGetRequiredLength](#qpdecodegetrequiredlength)|quoted-printable にエンコードされた指定長の文字列からデコードされたデータを格納できるバッファーのサイズを、バイト単位で取得します。|
|[QPEncode](#qpencode)|一部のデータを quoted-printable 形式にエンコードします。|
|[QPEncodeGetRequiredLength](#qpencodegetrequiredlength)|指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。|
|[UUDecode](#uudecode)|[Uuencode](#uuencode)の前回の呼び出しによって、uuencode されたデータの文字列をデコードします。|
|[UUDecodeGetRequiredLength](#uudecodegetrequiredlength)|指定した長さの uuencode された文字列からデコードされたデータを格納できるバッファーのサイズを、バイト単位で取得します。|
|[UUEncode](#uuencode)|データを uuencode します。 |
|[UUEncodeGetRequiredLength](#uuencodegetrequiredlength)|指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。|

## <a name="requirements"></a>必要条件

**ヘッダー:** atlenc

## <a name="atlgethexvalue"></a><a name="atlgethexvalue"></a> AtlGetHexValue

16 進数の数値を取得します。

```cpp
inline char AtlGetHexValue(char chIn) throw();
```

### <a name="parameters"></a>パラメーター

*chIn*<br/>
16進文字 ' 0 '-' 9 '、' A'-f '、または ' a'-f '。

### <a name="return-value"></a>戻り値

16進数字として解釈される入力文字の数値。 たとえば、' 0 ' の入力は値0を返し、' A ' の入力は値10を返します。 入力文字が16進数字でない場合、この関数は-1 を返します。

## <a name="atlgetversion"></a><a name="atlgetversion"></a> AtlGetVersion

使用している ATL ライブラリのバージョンを取得するには、この関数を呼び出します。

```cpp
ATLAPI_(DWORD) AtlGetVersion(void* pReserved);
```

### <a name="parameters"></a>パラメーター

*変わり*<br/>
予約されたポインター。

### <a name="return-value"></a>戻り値

コンパイル中または実行中の ATL ライブラリのバージョンの DWORD 整数値を返します。

## <a name="example"></a>例

関数は次のように呼び出す必要があります。

[!code-cpp[NVC_ATL_Utilities#95](../../atl/codesnippet/cpp/atl-text-encoding-functions_1.cpp)]

### <a name="requirements"></a>必要条件

**ヘッダー:** atlbase. h

## <a name="atlhexdecode"></a><a name="atlhexdecode"></a> AtlHexDecode

[AtlHexEncode](#atlhexencode)の以前の呼び出しによって、16進数のテキストとしてエンコードされたデータの文字列をデコードします。

```cpp
inline BOOL AtlHexDecode(
   LPCSTR pSrcData,
   int nSrcLen,
   LPBYTE pbDest,
   int* pnDestLen) throw();
```

### <a name="parameters"></a>パラメーター

*pSrcData*<br/>
デコードされるデータを格納している文字列。

*nSrcLen*<br/>
*Psrcdata*の長さ (文字数)。

*pbDest*<br/>
デコードされたデータを受信するために、呼び出し元が割り当てたバッファー。

*pnDestLen*<br/>
Pdest の長さ (バイト単位) を格納し*pbDest*ている変数へのポインター。 関数が成功した場合、変数はバッファーに書き込まれたバイト数を受け取ります。 関数が失敗した場合、変数はバッファーの必要な長さ (バイト単位) を受け取ります。

### <a name="return-value"></a>戻り値

成功した場合は TRUE、失敗した場合は FALSE を返します。

## <a name="atlhexdecodegetrequiredlength"></a><a name="atlhexdecodegetrequiredlength"></a> AtlHexDecodeGetRequiredLength

指定した長さの 16 進エンコードされた文字列からデコードされたデータを格納できるバッファーのサイズを、バイト単位で取得します。

```cpp
inline int AtlHexDecodeGetRequiredLength(int nSrcLen) throw();
```

### <a name="parameters"></a>パラメーター

*nSrcLen*<br/>
エンコードされた文字列の文字数。

### <a name="return-value"></a>戻り値

デコードされた文字列の *nSrcLen* 文字を保持できるバッファーに必要なバイト数。

## <a name="atlhexencode"></a><a name="atlhexencode"></a> AtlHexEncode

一部のデータを 16 進テキストの文字列としてエンコードします。

```cpp
inline BOOL AtlHexEncode(
   const BYTE * pbSrcData,
   int nSrcLen,
   LPSTR szDest,
int * pnDestLen) throw();
```

### <a name="parameters"></a>パラメーター

*pbSrcData*<br/>
エンコードされるデータを格納しているバッファー。

*nSrcLen*<br/>
エンコードされるデータの長さ (バイト単位)。

*szDest*<br/>
エンコードされたデータを受信するために、呼び出し元が割り当てたバッファー。

*pnDestLen*<br/>
*Szdest*の長さ (文字数) を格納している変数へのポインター。 関数が成功した場合、変数はバッファーに書き込まれた文字数を受け取ります。 関数が失敗した場合、変数はバッファーの文字数で必要な長さを受け取ります。

### <a name="return-value"></a>戻り値

成功した場合は TRUE、失敗した場合は FALSE を返します。

### <a name="remarks"></a>解説

ソースデータの各バイトは、2つの16進文字としてエンコードされます。

## <a name="atlhexencodegetrequiredlength"></a><a name="atlhexencodegetrequiredlength"></a> AtlHexEncodeGetRequiredLength

指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。

```cpp
inline int AtlHexEncodeGetRequiredLength(int nSrcLen) throw();
```

### <a name="parameters"></a>パラメーター

*nSrcLen*<br/>
エンコードされるデータのバイト数。

### <a name="return-value"></a>戻り値

*NSrcLen*バイトのエンコードされたデータを保持できるバッファーに必要な文字数。

## <a name="atlhexvalue"></a><a name="atlhexvalue"></a> AtlHexValue

16 進数の数値を取得します。

```cpp
inline short AtlHexValue(char chIn) throw();
```

### <a name="parameters"></a>パラメーター

*chIn*<br/>
16進文字 ' 0 '-' 9 '、' A'-f '、または ' a'-f '。

### <a name="return-value"></a>戻り値

16進数字として解釈される入力文字の数値。 たとえば、' 0 ' の入力は値0を返し、' A ' の入力は値10を返します。 入力文字が16進数字でない場合、この関数は-1 を返します。

## <a name="atlunicodetoutf8"></a><a name="atlunicodetoutf8"></a> AtlUnicodeToUTF8

Unicode 文字列を UTF-8 に変換します。

```cpp
ATL_NOINLINE inline int AtlUnicodeToUTF8(
   LPCWSTR wszSrc,
   int nSrc,
   LPSTR szDest,
   int nDest) throw();
```

### <a name="parameters"></a>パラメーター

*wszSrc*<br/>
変換する Unicode 文字列

*nSrc*<br/>
Unicode 文字列の長さ (文字数)。

*szDest*<br/>
変換された文字列を受信するために、呼び出し元が割り当てたバッファー。

*nDest*<br/>
バッファーの長さ (バイト単位)。

### <a name="return-value"></a>戻り値

変換された文字列の文字数を返します。

### <a name="remarks"></a>解説

変換された文字列に必要なバッファーのサイズを確認するには、この関数を呼び出して、 *szdest* と *ndest*に0を渡します。

## <a name="bencode"></a><a name="bencode"></a> BEncode

"B" エンコーディングを使用して一部のデータを変換します。

```cpp
inline BOOL BEncode(
   BYTE* pbSrcData,
   int nSrcLen,
   LPSTR szDest,
   int* pnDestLen,
   LPCSTR pszCharSet) throw();
```

### <a name="parameters"></a>パラメーター

*pbSrcData*<br/>
エンコードされるデータを格納しているバッファー。

*nSrcLen*<br/>
エンコードされるデータの長さ (バイト単位)。

*szDest*<br/>
エンコードされたデータを受信するために、呼び出し元が割り当てたバッファー。

*pnDestLen*<br/>
*Szdest*の長さ (文字数) を格納している変数へのポインター。 関数が成功した場合、変数はバッファーに書き込まれた文字数を受け取ります。 関数が失敗した場合、変数はバッファーの文字数で必要な長さを受け取ります。

*pszCharSet*<br/>
変換に使用する文字セット。

### <a name="return-value"></a>戻り値

成功した場合は TRUE、失敗した場合は FALSE を返します。

### <a name="remarks"></a>解説

"B" エンコード方式については、RFC 2047 () を参照して [https://www.ietf.org/rfc/rfc2047.txt](https://www.ietf.org/rfc/rfc2047.txt) ください。

## <a name="bencodegetrequiredlength"></a><a name="bencodegetrequiredlength"></a> BEncodeGetRequiredLength

指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。

```cpp
inline int BEncodeGetRequiredLength(int nSrcLen, int nCharsetLen) throw();
```

### <a name="parameters"></a>パラメーター

*nSrcLen*<br/>
エンコードされるデータのバイト数。

*nCharsetLen*<br/>
変換に使用する文字セットの長さ (文字数)。

### <a name="return-value"></a>戻り値

*NSrcLen*バイトのエンコードされたデータを保持できるバッファーに必要な文字数。

### <a name="remarks"></a>解説

"B" エンコード方式については、RFC 2047 () を参照して [https://www.ietf.org/rfc/rfc2047.txt](https://www.ietf.org/rfc/rfc2047.txt) ください。

## <a name="escapexml"></a><a name="escapexml"></a> EscapeXML

XML での使用には安全でない文字を安全な文字に変換します。

```cpp
inline int EscapeXML(
   const wchar_t * szIn,
   int nSrcLen,
   wchar_t * szEsc,
   int nDestLen,
   DWORD dwFlags = ATL_ESC_FLAG_NONE) throw();
```

### <a name="parameters"></a>パラメーター

*szIn*<br/>
変換対象の文字列。

*nSrclen*<br/>
変換する文字列の長さ (文字数)。

*szEsc*<br/>
変換された文字列を受信するために、呼び出し元が割り当てたバッファー。

*nDestLen*<br/>
呼び出し元が割り当てたバッファーの長さ (文字数)。

*dwFlags*<br/>
変換の実行方法を記述する ATL_ESC フラグ。

- 既定の動作を ATL_ESC_FLAG_NONE します。 引用符とアポストロフィは変換されません。
- ATL_ESC_FLAG_ATTR 引用符とアポストロフィは、それぞれとに変換され `&quot;` `&apos;` ます。

### <a name="return-value"></a>戻り値

変換された文字列の長さ (文字数)。

### <a name="remarks"></a>解説

次の表に、この関数によって実行される可能性のある変換を示します。

|source|宛先|
|------------|-----------------|
|\<|&lt;|
|>|&gt;|
|&|&amp;|
|'|&apos;|
|"|&quot;|

## <a name="getextendedchars"></a><a name="getextendedchars"></a> GetExtendedChars

文字列に含まれる拡張文字の数を取得します。

```cpp
inline int GetExtendedChars(LPCSTR szSrc, int nSrcLen) throw();
```

### <a name="parameters"></a>パラメーター

*szSrc*<br/>
分析される文字列。

*nSrcLen*<br/>
文字列の長さ (文字数)。

### <a name="return-value"></a>戻り値

[IsExtendedChar](#isextendedchar)によって決定される文字列内で見つかった拡張文字数を返します。

## <a name="isextendedchar"></a><a name="isextendedchar"></a> IsExtendedChar

この関数を呼び出して、特定の文字が拡張文字 (32 未満、126より大きい、タブ、ラインフィード、またはキャリッジリターンではない) であるかどうかを確認します。

```cpp
inline int IsExtendedChar(char ch) throw();
```

### <a name="parameters"></a>パラメーター

*ハーフ*<br/>
テストする文字

### <a name="return-value"></a>戻り値

文字が拡張されている場合は TRUE、それ以外の場合は FALSE。

## <a name="qencode"></a><a name="qencode"></a> QEncode

"Q" エンコーディングを使用して一部のデータを変換します。

```cpp
inline BOOL QEncode(
   BYTE* pbSrcData,
   int nSrcLen,
   LPSTR szDest,
   int* pnDestLen,
   LPCSTR pszCharSet,
   int* pnNumEncoded = NULL) throw();
```

### <a name="parameters"></a>パラメーター

*pbSrcData*<br/>
エンコードされるデータを格納しているバッファー。

*nSrcLen*<br/>
エンコードされるデータの長さ (バイト単位)。

*szDest*<br/>
エンコードされたデータを受信するために、呼び出し元が割り当てたバッファー。

*pnDestLen*<br/>
*Szdest*の長さ (文字数) を格納している変数へのポインター。 関数が成功した場合、変数はバッファーに書き込まれた文字数を受け取ります。 関数が失敗した場合、変数はバッファーの文字数で必要な長さを受け取ります。

*pszCharSet*<br/>
変換に使用する文字セット。

*pnNumEncoded*<br/>
返された変数へのポインターは、変換する必要があった安全でない文字の数を格納します。

### <a name="return-value"></a>戻り値

成功した場合は TRUE、失敗した場合は FALSE を返します。

### <a name="remarks"></a>解説

"Q" エンコード方式については、RFC 2047 () を参照して [https://www.ietf.org/rfc/rfc2047.txt](https://www.ietf.org/rfc/rfc2047.txt) ください。

## <a name="qencodegetrequiredlength"></a><a name="qencodegetrequiredlength"></a> QEncodeGetRequiredLength

指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。

```cpp
inline int QEncodeGetRequiredLength(int nSrcLen, int nCharsetLen) throw();
```

### <a name="parameters"></a>パラメーター

*nSrcLen*<br/>
エンコードされるデータのバイト数。

*nCharsetLen*<br/>
変換に使用する文字セットの長さ (文字数)。

### <a name="return-value"></a>戻り値

*NSrcLen*バイトのエンコードされたデータを保持できるバッファーに必要な文字数。

### <a name="remarks"></a>解説

"Q" エンコード方式については、RFC 2047 () を参照して [https://www.ietf.org/rfc/rfc2047.txt](https://www.ietf.org/rfc/rfc2047.txt) ください。

## <a name="qpdecode"></a><a name="qpdecode"></a> QPDecode

前回の [qの](#qpencode)呼び出しによってなど、引用符で囲まれた印刷可能な形式でエンコードされたデータの文字列をデコードします。

```cpp
inline BOOL QPDecode(
   BYTE* pbSrcData,
   int nSrcLen,
   LPSTR szDest,
   int* pnDestLen,
   DWORD dwFlags = 0) throw();
```

### <a name="parameters"></a>パラメーター

*pbSrcData*<br/>
からデコードされるデータを格納しているバッファー。

*nSrcLen*<br/>
から *Pbsrcdata*の長さ (バイト単位)。

*szDest*<br/>
入出力デコードされたデータを受信するために、呼び出し元が割り当てたバッファー。

*pnDestLen*<br/>
入出力 *Szdest*の長さ (バイト単位) を格納している変数へのポインター。 関数が成功した場合、変数はバッファーに書き込まれたバイト数を受け取ります。 関数が失敗した場合、変数はバッファーの必要な長さ (バイト単位) を受け取ります。

*dwFlags*<br/>
から変換の実行方法を記述する ATLSMTP_QPENCODE フラグ。

### <a name="return-value"></a>戻り値

成功した場合は TRUE、失敗した場合は FALSE を返します。

### <a name="remarks"></a>解説

引用符で囲まれた印刷可能なエンコード方式については、RFC 2045 () を参照して [https://www.ietf.org/rfc/rfc2045.txt](https://www.ietf.org/rfc/rfc2045.txt) ください。

## <a name="qpdecodegetrequiredlength"></a><a name="qpdecodegetrequiredlength"></a> QPDecodeGetRequiredLength

quoted-printable にエンコードされた指定長の文字列からデコードされたデータを格納できるバッファーのサイズを、バイト単位で取得します。

```cpp
inline int QPDecodeGetRequiredLength(int nSrcLen) throw();
```

### <a name="parameters"></a>パラメーター

*nSrcLen*<br/>
エンコードされた文字列の文字数。

### <a name="return-value"></a>戻り値

デコードされた文字列の *nSrcLen* 文字を保持できるバッファーに必要なバイト数。

### <a name="remarks"></a>解説

引用符で囲まれた印刷可能なエンコード方式については、RFC 2045 () を参照して [https://www.ietf.org/rfc/rfc2045.txt](https://www.ietf.org/rfc/rfc2045.txt) ください。

## <a name="qpencode"></a><a name="qpencode"></a> Qのコード

一部のデータを quoted-printable 形式にエンコードします。

```cpp
inline BOOL QPEncode(
   BYTE* pbSrcData,
   int nSrcLen,
   LPSTR szDest,
   int* pnDestLen,
   DWORD dwFlags = 0) throw ();
```

### <a name="parameters"></a>パラメーター

*pbSrcData*<br/>
エンコードされるデータを格納しているバッファー。

*nSrcLen*<br/>
エンコードされるデータの長さ (バイト単位)。

*szDest*<br/>
エンコードされたデータを受信するために、呼び出し元が割り当てたバッファー。

*pnDestLen*<br/>
*Szdest*の長さ (文字数) を格納している変数へのポインター。 関数が成功した場合、変数はバッファーに書き込まれた文字数を受け取ります。 関数が失敗した場合、変数はバッファーの文字数で必要な長さを受け取ります。

*dwFlags*<br/>
変換の実行方法を記述する ATLSMTP_QPENCODE フラグ。

- ATLSMTP_QPENCODE_DOT、行の先頭にピリオドがある場合は、エンコードされただけでなく出力にも追加されます。

- ATLSMTP_QPENCODE_TRAILING_SOFT `=\r\n` は、エンコードされた文字列にを追加します。

引用符で囲まれた印刷可能なエンコード方式については、 [RFC 2045](https://www.ietf.org/rfc/rfc2045.txt)を参照してください。

### <a name="return-value"></a>戻り値

成功した場合は TRUE、失敗した場合は FALSE を返します。

### <a name="remarks"></a>解説

引用符で囲まれた印刷可能なエンコード方式については、RFC 2045 () を参照して [https://www.ietf.org/rfc/rfc2045.txt](https://www.ietf.org/rfc/rfc2045.txt) ください。

## <a name="qpencodegetrequiredlength"></a><a name="qpencodegetrequiredlength"></a> QPEncodeGetRequiredLength

指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。

```cpp
inline int QPEncodeGetRequiredLength(int nSrcLen) throw ();
```

### <a name="parameters"></a>パラメーター

*nSrcLen*<br/>
エンコードされるデータのバイト数。

### <a name="return-value"></a>戻り値

*NSrcLen*バイトのエンコードされたデータを保持できるバッファーに必要な文字数。

### <a name="remarks"></a>解説

引用符で囲まれた印刷可能なエンコード方式については、RFC 2045 () を参照して [https://www.ietf.org/rfc/rfc2045.txt](https://www.ietf.org/rfc/rfc2045.txt) ください。

## <a name="uudecode"></a><a name="uudecode"></a> UUDecode

[Uuencode](#uuencode)の前回の呼び出しによって、uuencode されたデータの文字列をデコードします。

```cpp
inline BOOL UUDecode(
   BYTE* pbSrcData,
   int nSrcLen,
   BYTE* pbDest,
   int* pnDestLen) throw ();
```

### <a name="parameters"></a>パラメーター

*pbSrcData*<br/>
デコードされるデータを格納している文字列。

*nSrcLen*<br/>
*Pbsrcdata*の長さ (バイト単位)。

*pbDest*<br/>
デコードされたデータを受信するために、呼び出し元が割り当てたバッファー。

*pnDestLen*<br/>
Pdest の長さ (バイト単位) を格納し*pbDest*ている変数へのポインター。 関数が成功した場合、変数はバッファーに書き込まれたバイト数を受け取ります。 関数が失敗した場合、変数はバッファーの必要な長さ (バイト単位) を受け取ります。

### <a name="return-value"></a>戻り値

成功した場合は TRUE、失敗した場合は FALSE を返します。

### <a name="remarks"></a>解説

この uuencoding 実装は、POSIX P 1003.2 b/D11 仕様に従います。

## <a name="uudecodegetrequiredlength"></a><a name="uudecodegetrequiredlength"></a> UUDecodeGetRequiredLength

指定した長さの uuencode された文字列からデコードされたデータを格納できるバッファーのサイズを、バイト単位で取得します。

```cpp
inline int UUDecodeGetRequiredLength(int nSrcLen) throw ();
```

### <a name="parameters"></a>パラメーター

*nSrcLen*<br/>
エンコードされた文字列の文字数。

### <a name="return-value"></a>戻り値

デコードされた文字列の *nSrcLen* 文字を保持できるバッファーに必要なバイト数。

### <a name="remarks"></a>解説

この uuencoding 実装は、POSIX P 1003.2 b/D11 仕様に従います。

## <a name="uuencode"></a><a name="uuencode"></a> UUEncode

データを uuencode します。

```cpp
inline BOOL UUEncode(
   const BYTE* pbSrcData,
   int nSrcLen,
   LPSTR szDest,
   int* pnDestLen,
   LPCTSTR lpszFile = _T("file"),
   DWORD dwFlags = 0) throw ();
```

### <a name="parameters"></a>パラメーター

*pbSrcData*<br/>
エンコードされるデータを格納しているバッファー。

*nSrcLen*<br/>
エンコードされるデータの長さ (バイト単位)。

*szDest*<br/>
エンコードされたデータを受信するために、呼び出し元が割り当てたバッファー。

*pnDestLen*<br/>
*Szdest*の長さ (文字数) を格納している変数へのポインター。 関数が成功した場合、変数はバッファーに書き込まれた文字数を受け取ります。 関数が失敗した場合、変数はバッファーの文字数で必要な長さを受け取ります。

*lpszFile*<br/>
ATLSMTP_UUENCODE_HEADER が *dwFlags*に指定されている場合に、ヘッダーに追加されるファイル。

*dwFlags*<br/>
この関数の動作を制御するフラグ。

- ATLSMTP_UUENCODE_HEADE ヘッダーがエンコードされます。

- ATLSMTP_UUENCODE_END END はエンコードされます。

- ATLSMTP_UUENCODE_DOT Data 手紙が実行されます。

### <a name="return-value"></a>戻り値

成功した場合は TRUE、失敗した場合は FALSE を返します。

### <a name="remarks"></a>解説

この uuencoding 実装は、POSIX P 1003.2 b/D11 仕様に従います。

## <a name="uuencodegetrequiredlength"></a><a name="uuencodegetrequiredlength"></a> UUEncodeGetRequiredLength

指定したサイズのデータからエンコードされた文字列を格納できるバッファーのサイズを、文字数で取得します。

```cpp
inline int UUEncodeGetRequiredLength(int nSrcLen) throw ();
```

### <a name="parameters"></a>パラメーター

*nSrcLen*<br/>
エンコードされるデータのバイト数。

### <a name="return-value"></a>戻り値

*NSrcLen*バイトのエンコードされたデータを保持できるバッファーに必要な文字数。

### <a name="remarks"></a>解説

この uuencoding 実装は、POSIX P 1003.2 b/D11 仕様に従います。

## <a name="see-also"></a>関連項目

[概念](../active-template-library-atl-concepts.md)<br/>
[ATL COM デスクトップ コンポーネント](../atl-com-desktop-components.md)
