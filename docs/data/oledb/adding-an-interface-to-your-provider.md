---
title: プロバイダーへのインターフェイスの追加
ms.date: 05/09/2019
helpviewer_keywords:
- OLE DB provider templates, object interfaces
ms.assetid: b0fc7cf8-428a-4584-9d64-ce9074d0eb66
ms.openlocfilehash: b13d1224388dc7d3218dea1c70b5aa8a595fcbdb
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80212332"
---
# <a name="adding-an-interface-to-your-provider"></a>プロバイダーへのインターフェイスの追加

> [!NOTE]
> ATL OLE DB プロバイダー ウィザードは、Visual Studio 2019 以降では使用できません。

インターフェイスを追加するオブジェクトを決定します (通常は **OLE DB プロバイダー ウィザード**で作成されたデータ ソース、行セット、コマンド、またはセッション オブジェクトです)。 インターフェイスを追加する必要があるオブジェクトが、プロバイダーで現在サポートされていない可能性もあります。 その場合は、**ATL OLE DB プロバイダー ウィザード**を実行してオブジェクトを作成します。 **クラス ビュー**でプロジェクトを右クリックし、メニューの **[追加]**  >  **[新しい項目]** をクリックします。 **[インストール済み]**  >  **[Visual C++]**  >  **[ATL]** を選択したら、 **[ATL OLEDB プロバイダー]** をクリックします。 インターフェイスのコードを別のディレクトリに配置し、そのファイルをプロバイダー プロジェクトにコピーすることもできます。

インターフェイスをサポートする新しいクラスを作成した場合は、オブジェクトがそのクラスから継承するようにします。 たとえば、次のようにクラス `IRowsetIndexImpl` を行セット オブジェクトに追加します。

```cpp
template <class Creator>
class CCustomRowset :
    public CRowsetImpl< CCustomRowset<Creator>, CCustomWindowsFile, Creator>,
    public IRowsetIndexImpl< ... >
```

COM_INTERFACE_ENTRY マクロを使用して、オブジェクトの COM_MAP にインターフェイスを追加します。 マップがない場合は作成します。 次に例を示します。

```cpp
BEGIN_COM_MAP(CCustomRowset)
     COM_INTERFACE_ENTRY(IRowsetIndex)
END_COM_MAP()
```

行セット オブジェクトの場合、その親オブジェクトのマップを連結して、オブジェクトが親クラスに委任できるようにします。 この例では、COM_INTERFACE_ENTRY_CHAIN マクロをマップに追加します。

```cpp
BEGIN_COM_MAP(CCustomRowset)
     COM_INTERFACE_ENTRY(IRowsetIndex)
     COM_INTERFACE_ENTRY_CHAIN(CRowsetImpl)
END_COM_MAP()
```

## <a name="see-also"></a>参照

[OLE DB プロバイダー テンプレートの操作](../../data/oledb/working-with-ole-db-provider-templates.md)
