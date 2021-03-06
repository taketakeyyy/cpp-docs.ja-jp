---
title: ATL コントロールの追加
ms.date: 11/04/2016
helpviewer_keywords:
- ATL projects, adding controls
- controls [ATL], adding to projects
ms.assetid: 10223e7e-fdb7-4163-80c6-44aeafa8e6ce
ms.openlocfilehash: fac1efeb3d373a8324828a8b10f0570f253f6103
ms.sourcegitcommit: a1676bf6caae05ecd698f26ed80c08828722b237
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/29/2020
ms.locfileid: "91499297"
---
# <a name="adding-an-atl-control"></a>ATL コントロールの追加

このウィザードを使用して、可能性のあるすべてのコンテナーのインターフェイスをサポートするプロジェクトにユーザーインターフェイスオブジェクトを追加します。 これらのインターフェイスをサポートするには、ATL アプリケーションとして、または ATL サポートを含む MFC アプリケーションとしてプロジェクトが作成されている必要があります。 Atl [プロジェクトウィザード](../../atl/reference/atl-project-wizard.md) を使用して atl アプリケーションを作成するか、mfc アプリケーション [に atl オブジェクトを追加](../../mfc/reference/adding-atl-support-to-your-mfc-project.md) して、mfc アプリケーションの atl サポートを実装することができます。

## <a name="to-add-an-atl-control-to-your-project"></a>ATL コントロールをプロジェクトに追加するには

1. **ソリューションエクスプローラー**または[クラスビュー](/visualstudio/ide/viewing-the-structure-of-code)で、ATL simple オブジェクトを追加するプロジェクトの名前を右クリックします。

1. ショートカットメニューの [ **追加** ] をクリックし、[ **クラスの追加**] をクリックします。

1. [ [クラスの追加](../../ide/adding-a-class-visual-cpp.md#add-class-dialog-box) ] ダイアログボックスの [テンプレート] ペインで、[ **atl コントロール**] をクリックし、[ **追加** ] をクリックして [atl コントロールウィザード](../../atl/reference/atl-control-wizard.md)を表示します。

**ATL コントロールウィザード**を使用すると、次の3種類のコントロールのいずれかを作成できます。

- 標準コントロール

- 複合コントロール

- DHTML コントロール

また、ウィザードの [**オプション**] ページで [**最小コントロール**] を選択すると、コントロールのサイズを縮小したり、ほとんどのコンテナーで使用されていないインターフェイスを削除したりすることができます。

## <a name="see-also"></a>関連項目

[複合コントロールへの機能の追加](../../atl/adding-functionality-to-the-composite-control.md)<br/>
[ATL COM オブジェクトの基礎](../../atl/fundamentals-of-atl-com-objects.md)
