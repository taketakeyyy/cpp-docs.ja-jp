---
title: スキーマ (MFC データ アクセス)
ms.date: 11/04/2016
helpviewer_keywords:
- structures [C++], database
- databases [C++], schema
- database schema [C++], about database schemas
- database schema [C++]
- schemas [C++], database
- structures [C++]
ms.assetid: 7d17e35f-1ccf-4853-b915-5b8c7a45b9ee
ms.openlocfilehash: 0eac4f47c3d00c34c1aadaef18202a95f831ad82
ms.sourcegitcommit: 857fa6b530224fa6c18675138043aba9aa0619fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/24/2020
ms.locfileid: "80209094"
---
# <a name="schema--mfc-data-access"></a>スキーマ (MFC データ アクセス)

データベース スキーマは、データベース内のテーブルとデータベース ビューの現在の構造を記述するものです。 通常、ウィザードで生成されたコードでは、レコードセットからアクセスするテーブルのスキーマは変更されないことを想定しています。ただし、データベース クラスでは、ある程度のスキーマの変更 (バインドされていない列の追加、並べ替え、削除など) に対応できます。 テーブルが変更された場合は、そのテーブルのレコードセットを手動で更新し、アプリケーションを再コンパイルする必要があります。

ウィザードで生成されるコードを補うことで、コンパイル時にスキーマの詳細が不明なデータベースが処理されるようにできます。 詳細については、「[レコードセット: データ列の動的なバインド (ODBC)](../data/odbc/recordset-dynamically-binding-data-columns-odbc.md)」を参照してください。

## <a name="see-also"></a>参照

[データ アクセス プログラミング (MFC/ATL)](../data/data-access-programming-mfc-atl.md)<br/>
[SQL](../data/odbc/sql.md)<br/>
[レコードセット (ODBC)](../data/odbc/recordset-odbc.md)
