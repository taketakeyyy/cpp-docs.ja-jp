---
title: プロバイダーでのプロパティの設定
ms.date: 10/29/2018
helpviewer_keywords:
- OLE DB providers, properties
- properties [C++], OLE DB provider
ms.assetid: 26a8b493-7ec4-4686-96d0-9ad5d2bca5ac
ms.openlocfilehash: 3717282d284990b1b8038f6954ee971938cf7921
ms.sourcegitcommit: a1676bf6caae05ecd698f26ed80c08828722b237
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91509482"
---
# <a name="setting-properties-in-your-provider"></a>プロバイダーでのプロパティの設定

必要なプロパティのプロパティグループとプロパティ ID を検索します。 詳細については、 **OLE DB プログラマーリファレンス**の「 [OLE DB のプロパティ](/previous-versions/windows/desktop/ms722734(v=vs.85))」を参照してください。

ウィザードによって生成されたプロバイダーコードで、プロパティグループに対応するプロパティマップを見つけます。 通常、プロパティグループの名前は、オブジェクトの名前に対応します。 コマンドと行セットのプロパティは、コマンドまたは行セットにあります。データソースと初期化プロパティは、データソースオブジェクトにあります。

プロパティマップで、 [PROPERTY_INFO_ENTRY_EX](./macros-for-ole-db-provider-templates.md#property_info_entry_ex) マクロを追加します。 PROPERTY_INFO_ENTRY_EX には、次の4つのパラメーターがあります。

- プロパティに対応するプロパティ ID。 プロパティ名の先頭から最初の7文字 ("DBPROP_") を削除します。 たとえば、を追加する場合は、 `DBPROP_MAXROWS` を `MAXROWS` 最初の要素として渡します。 これがカスタムプロパティの場合は、完全な GUID 名 (など) を渡し `DBMYPROP_MYPROPERTY` ます。

- プロパティのバリアント型 ( **OLE DB プログラマーリファレンス**の[OLE DB プロパティ](/previous-versions/windows/desktop/ms722734(v=vs.85)))。 データ型に対応する VT_ の種類 (VT_BOOL、VT_I2 など) を入力します。

- プロパティが読み取り可能で書き込み可能であるかどうか、およびそのプロパティが属するグループを示すフラグ。 たとえば、次のコードは、行セットグループに属している読み取り/書き込みプロパティを示しています。

    ```cpp
    DBPROPFLAGS_ROWSET | DBPROPFLAGS_READ | DBPROPFLAGS_WRITE
    ```

- プロパティの基本値。 たとえば、ブール型の場合は、整数型の場合は0になり `VARIANT_FALSE` ます。 プロパティは、変更されない限り、この値を持ちます。

    > [!NOTE]
    > 一部のプロパティは、ブックマークや更新など、他のプロパティに接続または連結されています。 コンシューマーが1つのプロパティを true に設定すると、別のプロパティも設定される可能性があります。 OLE DB プロバイダーテンプレートでは、 [Cutlprops:: OnPropertyChanged](./cutlprops-class.md#onpropertychanged)メソッドを使用してこれをサポートしています。

## <a name="properties-ignored-by-microsoft-ole-db-providers"></a>Microsoft OLE DB プロバイダーによって無視されるプロパティ

Microsoft OLE DB プロバイダーは、次の OLE DB プロパティを無視します。

- `DBPROP_MAXROWS` は読み取り専用プロバイダー (つまり、とが) に対してのみ機能 `DBPROP_IRowsetChange` `DBPROP_IRowsetUpdate` します **`false`** 。それ以外の場合、このプロパティはサポートされません。

- `DBPROP_MAXPENDINGROWS` は無視されます。プロバイダーによって独自の制限が指定されています。

- `DBPROP_MAXOPENROWS` は無視されます。プロバイダーによって独自の制限が指定されています。

- `DBPROP_CANHOLDROWS` は無視されます。プロバイダーによって独自の制限が指定されています。

## <a name="see-also"></a>関連項目

[OLE DB プロバイダーテンプレートの操作](../../data/oledb/working-with-ole-db-provider-templates.md)
