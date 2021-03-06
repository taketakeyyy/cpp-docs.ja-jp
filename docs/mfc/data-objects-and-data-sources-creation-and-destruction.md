---
title: 'データ オブジェクトとデータ ソース : 作成と破棄'
ms.date: 11/04/2016
helpviewer_keywords:
- destroying data objects [MFC]
- object creation [MFC], data source objects
- data sources [MFC], and data objects
- data source objects [MFC], creating
- destruction [MFC], data sources
- data source objects [MFC], destroying
- data objects [MFC], creating
- data objects [MFC], destroying
- data sources [MFC], role
- data sources [MFC], destroying
- destruction [MFC], data objects
- data sources [MFC], creating
ms.assetid: ac216d54-3ca5-4ce7-850d-cd1f6a90d4f1
ms.openlocfilehash: 8d4edc93594bf453c61e03dca7e3117aefaa6c42
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84620496"
---
# <a name="data-objects-and-data-sources-creation-and-destruction"></a>データ オブジェクトとデータ ソース : 作成と破棄

「[データオブジェクトとデータソース (OLE)](data-objects-and-data-sources-ole.md)」で説明されているように、データオブジェクトとデータソースはデータ転送の両側を表します。 ここでは、データ転送を正しく実行するために、これらのオブジェクトとソースをいつ作成し、いつ破棄するかについて説明します。

- [データオブジェクトの作成](#_core_creating_data_objects)

- [データオブジェクトの破棄](#_core_destroying_data_objects)

- [データ ソースの作成](#_core_creating_data_sources)

- [データ ソースの破棄](#_core_destroying_data_sources)

## <a name="creating-data-objects"></a><a name="_core_creating_data_objects"></a>データオブジェクトの作成

データ オブジェクトは、転送先アプリケーション (クライアントまたはサーバー) で使用されます。 転送先アプリケーションのデータ オブジェクトは、転送元アプリケーションと転送先アプリケーション間の接続の片端となります。 転送先アプリケーションのデータ オブジェクトは、データ ソース内のデータへのアクセスと対話に使用されます。

データ オブジェクトが必要な状況は、一般的に 2 つあります。 1 つ目は、ドラッグ アンド ドロップを使用してアプリケーションにデータをドロップする場合です。 2 つ目は、[編集] メニューの [貼り付け] または [形式を選択して貼り付け] を選択する場合です。

ドラッグ アンド ドロップの場合、データ オブジェクトを作成する必要はありません。 既存のデータ オブジェクトへのポインターが `OnDrop` 関数に渡されます。 このデータ オブジェクトは、ドラッグ アンド ドロップ操作の一環としてフレームワークによって作成され、さらにフレームワークによって破棄されます。 貼り付けが別の方法で行われる場合は、必ずしもこれが当てはまるとは限りません。 詳細については、「[データオブジェクトの破棄](#_core_destroying_data_objects)」を参照してください。

アプリケーションで [貼り付け] または [形式を選択して貼り付け] 操作を実行する場合は、`COleDataObject` オブジェクトを作成し、その `AttachClipboard` メンバー関数を呼び出す必要があります。 これにより、データ オブジェクトはクリップボード上のデータと関連付けられます。 その後、貼り付け関数でこのデータ オブジェクトを使用できます。

## <a name="destroying-data-objects"></a><a name="_core_destroying_data_objects"></a>データオブジェクトの破棄

「[データオブジェクトの作成](#_core_creating_data_objects)」で説明されているスキームに従っている場合、データオブジェクトの破棄はデータ転送のごく一部です。 貼り付け関数で作成されたデータ オブジェクトは、関数から制御が戻るときに、MFC によって破棄されます。

貼り付け操作を別の方法で処理する場合は、貼り付け操作が完了した後にデータ オブジェクトが破棄されるようにしてください。 データ オブジェクトが破棄されるまで、アプリケーションではデータをクリップボードに正常にコピーすることができません。

## <a name="creating-data-sources"></a><a name="_core_creating_data_sources"></a>データソースの作成

データ ソースは、データ転送の送信元によって使用されます。この送信元は、データ転送のクライアント側の場合もサーバー側の場合もあります。 転送元アプリケーションのデータ ソースは、転送元アプリケーションと転送先アプリケーション間の接続の片端となります。 転送先アプリケーションのデータ オブジェクトは、データ ソース内のデータとの対話に使用されます。

データ ソースは、アプリケーションでデータをクリップボードにコピーすることが必要な場合に作成されます。 一般的なシナリオは次のようになります。

1. ユーザーがいくつかのデータを選択します。

1. ユーザーは、[**編集**] メニューの [**コピー** ] (または [**切り取り**]) を選択するか、ドラッグアンドドロップ操作を開始します。

1. プログラムの仕様に応じて、アプリケーションは `COleDataSource` オブジェクトを作成するか、`COleDataSource` から派生したクラスからオブジェクトを作成します。

1. 選択したデータは、`COleDataSource::CacheData` グループまたは `COleDataSource::DelayRenderData` グループ内の関数のいずれかを呼び出すと、データ ソースに挿入されます。

1. アプリケーションは、手順 3. で作成したオブジェクトに属する `SetClipboard` メンバー関数 (またはドラッグ アンド ドロップ操作の場合は `DoDragDrop` メンバー関数) を呼び出します。

1. これが**切り取り**操作の場合、または DROPEFFECT_MOVE を返した場合は、 `DoDragDrop` 手順 1. で選択したデータがドキュメントから削除されます。 **DROPEFFECT_MOVE**

このシナリオは、MFC OLE サンプル[OCLIENT](../overview/visual-cpp-samples.md)および[HIERSVR](../overview/visual-cpp-samples.md)によって実装されています。 `GetClipboardData` 関数と `OnGetClipboardData` 関数を除くすべてについて、各アプリケーションの `CView` から派生したクラスのソースを確認してください。 これらの 2 つの関数は、`COleClientItem` または `COleServerItem` から派生したクラスの実装に含まれています。 これらのサンプル プログラムでは、これらの概念を実装する方法の良い例を示しています。

さらに、ドラッグ アンド ドロップ操作の既定の動作を変更する場合にも、`COleDataSource` オブジェクトの作成が必要になることがあります。 詳細については、「 [OLE ドラッグアンドドロップ: ドラッグアンドドロップをカスタマイズ](drag-and-drop-ole.md#customize-drag-and-drop)する」を参照してください。

## <a name="destroying-data-sources"></a><a name="_core_destroying_data_sources"></a>データソースの破棄

データ ソースは、現在データ ソースを管理しているアプリケーションによって破棄する必要があります。 [COleDataSource::D odragdrop](reference/coledatasource-class.md#dodragdrop)の呼び出しなど、データソースを OLE に渡す場合は、を呼び出す必要があり `pDataSrc->InternalRelease` ます。 次に例を示します。

[!code-cpp[NVC_MFCListView#1](../atl/reference/codesnippet/cpp/data-objects-and-data-sources-creation-and-destruction_1.cpp)]

OLE にデータ ソースを渡していない場合は、通常の C++ オブジェクトの場合と同様、データ ソースを破棄します。

詳細については、「[ドラッグアンドドロップ](drag-and-drop-ole.md)、[クリップボード](clipboard.md)、および[データオブジェクトとデータソースの操作](data-objects-and-data-sources-manipulation.md)」を参照してください。

## <a name="see-also"></a>関連項目

[データ オブジェクトとデータ ソース (OLE)](data-objects-and-data-sources-ole.md)<br/>
[COleDataObject クラス](reference/coledataobject-class.md)<br/>
[COleDataSource クラス](reference/coledatasource-class.md)
