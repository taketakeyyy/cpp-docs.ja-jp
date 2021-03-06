---
title: ツール ヒント用 TTN_NEEDTEXT 通知の処理
ms.date: 11/04/2016
f1_keywords:
- TTN_NEEDTEXT
helpviewer_keywords:
- TTN_NEEDTEXT message [MFC]
- notifications [MFC], tool tips
- tool tips [MFC], notifications
ms.assetid: d0370a65-21ba-4676-bcc5-8cf851bbb15c
ms.openlocfilehash: 75850dbf92587cf654d4f7a39ea54af1fd9dd5bd
ms.sourcegitcommit: c21b05042debc97d14875e019ee9d698691ffc0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84620078"
---
# <a name="handling-ttn_needtext-notification-for-tool-tips"></a>ツール ヒント用 TTN_NEEDTEXT 通知の処理

[ツールヒントを有効](enabling-tool-tips.md)にする際には、オーナーウィンドウのメッセージマップに次のエントリを追加することによって**TTN_NEEDTEXT**メッセージを処理します。

[!code-cpp[NVC_MFCControlLadenDialog#40](codesnippet/cpp/handling-ttn-needtext-notification-for-tool-tips_1.cpp)]

*memberFxn*<br/>
このボタンにテキストが必要な場合に呼び出されるメンバー関数。

ツールヒントの ID は常に0であることに注意してください。

次のように、クラス定義でハンドラー関数を宣言します。

[!code-cpp[NVC_MFCControlLadenDialog#53](codesnippet/cpp/handling-ttn-needtext-notification-for-tool-tips_2.h)]

斜体のパラメーターは次のとおりです。

*id*<br/>
通知を送信したコントロールの識別子。 使用されていません。 コントロール id は、 **NMHDR**構造体から取得されます。

*pNMHDR*<br/>
[Nmttdispinfo](/windows/win32/api/commctrl/ns-commctrl-nmttdispinfow)構造体へのポインター。 この構造体の詳細につい[ては、TOOLTIPTEXT 構造体](tooltiptext-structure.md)にも記載されています。

*pResult*<br/>
を返す前に設定できる結果コードへのポインター。 **TTN_NEEDTEXT**ハンドラーは、 *pResult*パラメーターを無視できます。

フォームビューの通知ハンドラーの例を次に示します。

[!code-cpp[NVC_MFCControlLadenDialog#54](codesnippet/cpp/handling-ttn-needtext-notification-for-tool-tips_3.cpp)]

呼び出し `EnableToolTips` (から取得したこのフラグメント `OnInitDialog` ):

[!code-cpp[NVC_MFCControlLadenDialog#55](codesnippet/cpp/handling-ttn-needtext-notification-for-tool-tips_4.cpp)]

## <a name="see-also"></a>関連項目

[CFrameWnd から派生していないウィンドウのツール ヒント](tool-tips-in-windows-not-derived-from-cframewnd.md)
