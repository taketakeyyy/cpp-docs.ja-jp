---
title: Visual C++ でのデータ アクセス
ms.date: 03/28/2017
helpviewer_keywords:
- Visual C++, data access applications
- databases [C++]
- OLE DB [C++], data access technologies
- data [C++], data access technologies
- data access [C++], class libraries for databases
ms.assetid: 95da6237-bbe2-480a-ae50-3a520051ceff
ms.openlocfilehash: a5421ff05fdbad7d78066bb95410aafe69bfaa51
ms.sourcegitcommit: ec6dd97ef3d10b44e0fedaa8e53f41696f49ac7b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88836947"
---
# <a name="data-access-in-visual-c"></a>Visual C++ でのデータ アクセス

ほぼすべてのデータベース製品 (SQL および NoSQL) には、ネイティブ C++ アプリケーション用のインターフェイスが用意されています。 業界標準のインターフェイスは ODBC です。ODBC は主要な SQL データベース製品と多数の NoSQL 製品でサポートされています。 Microsoft 以外の製品の詳細については、ベンダーにお問い合わせください。 さまざまなライセンス条項のサードパーティのライブラリも使用できます。

Microsoft は、2011 年以降、オンプレミスとクラウドの両方で Microsoft SQL Server データベースに接続するネイティブ アプリケーションの標準として ODBC を調整してきました。 詳細については、「[データ アクセス プログラミング \(MFC-ATL\)](data-access-programming-mfc-atl.md)」を参照してください。 C++/CLI ライブラリでは、ネイティブ ODBC ドライバーまたは ADO.NET を使用できます。 詳細については、「 [ADO.NET を使用したデータアクセス (C++/cli)](../dotnet/data-access-using-adonet-cpp-cli.md) 」と「 [Visual Studio でのデータ](/visualstudio/data-tools/accessing-data-in-visual-studio)へのアクセス」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

[データアクセスプログラミング (MFC/ATL)](data-access-programming-mfc-atl.md)<br/>
Visual C++ を使用したレガシ データ アクセス プログラミングについて説明します。このプログラミングには、データベース API での処理が簡単になるように、ATL (Active Template Class Library)、MFC (Microsoft Foundation Class) ライブラリなどのクラス ライブラリの 1 つを使用することをお勧めします。

[Open Database Connectivity (ODBC)](odbc/open-database-connectivity-odbc.md)<br/>
MFC (Microsoft Foundation Class) ライブラリには、ODBC (Open Database Connectivity) を使用したプログラミング用のクラスが用意されています。

[OLE DB プログラミング](oledb/ole-db-programming.md)<br/>
主に、一部のシナリオで (特にリンク サーバーに対してプログラミングするときに) 引き続き必要なレガシ インターフェイス。

## <a name="related-topics"></a>関連トピック

[C と C++ を使用して SQL Database に接続する](/azure/sql-database/sql-database-develop-cplusplus-simple)<br/>
C または C++ アプリケーションから Azure SQL Database に接続します。

[C++ 用 Microsoft Azure Storage クライアント ライブラリ](https://github.com/Azure/azure-storage-cpp)<br/>
[Azure Storage](/azure/storage/common/storage-introduction) は、顧客のニーズに合う耐久性、可用性、スケーラビリティを必要とする最新のアプリケーション向けのクラウド ストレージ ソリューションです。 C++ 用 Azure Storage クライアント ライブラリを使用して C++ から Azure Storage に接続します。

[ODBC Driver for SQL Server](/sql/connect/odbc/microsoft-odbc-driver-for-sql-server)<br/>
最新の ODBC ドライバーには、C/C++ ベースのアプリケーション向けの Microsoft SQL Server および Microsoft Azure SQL Database に対する堅牢なデータ アクセス機能があります。 常時暗号化、Azure Active Directory、AlwaysOn 可用性グループなどの機能をサポートしています。 また、Mac OS と Linux でも使用できます。

[OLE DB Driver for SQL Server](/sql/connect/oledb/oledb-driver-for-sql-server)<br/>
最新の OLE DB ドライバーは、Microsoft SQL Server と Microsoft Azure SQL Database をサポートする単体のデータ アクセス アプリケーション プログラミング インターフェイス (API) です。

[Microsoft Azure C および C++ デベロッパー センター](https://azure.microsoft.com/develop/cpp/)<br/>
Azure を使用すると、柔軟性、スケーラビリティ、信頼性の高い C++ アプリケーションを好みのツールで容易に構築できます。

[C++ から BLOB ストレージを使用する方法](/azure/storage/storage-c-plus-plus-how-to-use-blobs)<br/>
Azure Blob Storage は、非構造化データをクラウド内にオブジェクト/BLOB として格納するサービスです。 Blob Storage は、ドキュメント、メディア ファイル、アプリケーション インストーラーなど、任意の種類のテキスト データやバイナリ データを格納できます。 Blob Storage は、オブジェクト ストレージとも呼ばれます。

[ODBC プログラマー リファレンス](/sql/odbc/reference/odbc-programmer-s-reference)<br/>
ODBC インターフェイスは、C プログラミング言語で使用するために設計されています。 ODBC インターフェイスは、SQL ステートメント、ODBC 関数呼び出し、C プログラミングという 3 つの領域で使用されます。

## <a name="see-also"></a>関連項目

[Visual Studio での C++](../overview/visual-cpp-in-visual-studio.md)
