﻿---
lab:
    title: '01 - Azure Active Directory ID を管理する'
    module: 'モジュール 01 - Identity'
---

# ラボ 01 - Azure Active Directory の管理

# 受講生用ラボ マニュアル

## ラボ シナリオ

Contoso のユーザーが Azure AD を使用して認証できるようにするには、ユーザーとグループ アカウントのプロビジョニングを任されています。グループのメンバーシップは、ユーザーの役職に基づいて自動的に更新する必要があります。テスト ユーザー アカウントを使用してテスト Azure AD テナントを作成し、Contoso Azure サブスクリプションのリソースに対する限定的なアクセス許可をそのアカウントに付与する必要もあります。

## 目標

このラボでは、次の内容を学習します。

+ タスク 1: Azure AD ユーザーを作成および構成する
+ タスク 2: 割り当て済みおよび動的メンバーシップを持つ Azure AD グループを作成する
+ タスク 3: Azure Active Directory (AD) テナントを作成する
+ タスク 4: Azure AD ゲスト ユーザーを管理する 

## 予想時間: 30分間

## 指示

### 演習 1

#### タスク 1: Azure AD ユーザーを作成および構成する

このタスクでは、Azure AD ユーザーを作成して構成します。

1. Azure portal で、**Azure Active Directory** を検索し、選択します。

1. 「Azure Active Directory」 ブレードで、 「**管理**」 セクションまでスクロールダウンし、「**ユーザー設定**」 をクリックして、使用可能な構成オプションを確認します。

1. 「Azure Active Directory」 ブレードの 「**管理**」 セクションで 「**ユーザー**」 をクリックし、ユーザー アカウントをクリックして 「**プロファイル**」 設定を表示します。 

1. **編集**をクリックし、**設定**セクションで、**使用場所** を **米国**に設定し、変更を保存します。

    >**注**: このラボの後半で、Azure AD Premium P2 ライセンスをユーザー アカウントに割り当てるために、この操作が必要です。

1. 「**ユーザー - すべてのユーザー**」 ブレードに戻り、「**+ 新しいユーザー**」 をクリックします。

1. 次の設定で新しいユーザーを作成します (その他は既定のままにします)。

    | 設定 | 値 |
    | --- | --- |
    | ユーザー名 | **az104-01a-aaduser1** |
    | 名前 | **az104-01a-aaduser1** |
    | パスワードを作成します | enabled |
    | 初期パスワード | **Pa55w.rd124** |
    | 使用場所 | **米国** |
    | 役職 | **クラウド管理者** |
    | 部署 | **IT** |

    >**注**: **クリップボードに完全な**ユーザー名**をコピーします**。 これは、タスクの後半で必要となります。

1. ユーザーの一覧で、新しく作成したユーザー アカウントをクリックして、そのブレードを表示します。

1. **管理**セクションで使用できるオプションを確認し、ユーザー アカウントに割り当てられた Azure AD ロールと、Azure リソースに対するユーザー アカウントのアクセス許可を識別できることを確認します。

1. **管理**セクションで、**割り当て済ロール** をクリックし、**+ Add assignment** ボタンをクリックして 、**ユーザー管理者** ロールを **az104-01a-aaduser1**に割り当てます。

    >**注**: 新しいユーザーをプロビジョニングするときに、Azure AD ロールを割り当てるオプションもあります。

1. **InPrivate** ブラウザー ウィンドウを開き、新しく作成したユーザー アカウントを使用して [Azure portal](https://portal.azure.com)にサインインします。パスワードを更新するように求められたら、ユーザーのパスワードを変更します。

    >**注**: ユーザー名を入力するのではなく、クリップボードの内容を貼り付けることができます。

1. **InPrivate** ブラウザー ウィンドウのAzure portal で、 **Azure Active Directory** を検索して選択します。

    >**注**: このユーザー アカウントは Azure Active Directory テナントにアクセスできますが、Azure リソースへのアクセス権はありません。このようなアクセスは、Azure ロールベースのアクセス制御を使用して明示的に付与する必要があるため、このような仕様になっています。 

1. **InPrivate** ブラウザー ウィンドウでの、「Azure AD」 ブレードで 「**管理**」 セクションまでスクロールし、「**ユーザー設定**」 をクリックします。設定オプションを変更する権限は無いことに注意ください。

1. 「**InPrivate** ブラウザー」 ウィンドウの 「Azure AD」 ブレードの 「**管理**」 セクションで、「**ユーザー**」 をクリック し、「**+ 新しいユーザー**」 をクリックします。

1. 次の設定で新しいユーザーを作成します (その他は既定のままにします)。

    | 設定 | 値 |
    | --- | --- |
    | ユーザー名 | **az104-01a-aaduser2** |
    | 名前 | **az104-01a-aaduser2** |
    | パスワードを作成します | enabled |
    | 初期パスワード | **Pa55w.rd124** |
    | 使用場所 | **米国** |
    | 役職 | **システム管理者** |
    | 部署 | **IT** |

1. Azure portal から az104-01a-aaduser1 ユーザーとしてサインアウトし、InPrivate ブラウザー ウィンドウを閉じます。

#### タスク 2: 割り当て済みおよび動的メンバーシップを持つ Azure AD グループを作成する

このタスクでは、割り当て済み動的メンバーシップを持つ Azure Active Directory グループを作成します。

1. ユーザー アカウントでログインしている Azure portal に戻り、AD テナントの 「概要」 ブレードに戻り、「管理」 セクションの 「**ライセンス**」 をクリックします。

    >**注**: 動的グループを実装するには、Azure AD Premium P1 または P2 ライセンスが必要です。

1. 「**管理**」 セクションで、「**すべての製品**」 をクリックします。

1. 「**+ 試用/購入**」 をクリックし、Azure AD Premium P2 の無料試用版をアクティブにします。

1. ブラウザーの画面を更新して、アクティブ化が成功したことを確認します。 

1. 「**ライセンス - すべての**製品」 ブレードで、「Azure Active Directory Premium P2」 エントリを選択し、**Azure Active Directory Premium P2** エントリを選択し、Azure AD Premium P2 のすべてのライセンス オプションをユーザー アカウントと新しく作成した 2 つのユーザー アカウントに割り当てます。  

1. Azure portal で、Azure AD テナント ブレードに戻り、 「**グループ**」 をクリックします。

1. 「**+ 新規グループ**」 ボタンを使用して、次の設定で新しいグループを作成します。

    | 設定 | 値 |
    | --- | --- |
    | グループ タイプ | **セキュリティ** |
    | グループ名 | **IT クラウド管理者** |
    | グループの説明 | **Contoso IT クラウド管理者** |
    | メンバーシップ タイプ | **動的ユーザー** |

    >**注**: 「**メンバーシップ タイプ**」 ドロップダウン リストがグレー表示されている場合は、ブラウザーのページを更新します。

1. 「**動的クエリの追加**」 をクリックします。 

1. 「**動的メンバーシップ ルール**」 ブレードの 「**ルールの構成**」 タブで、次の設定を使用して新しい規則を作成します。

    | 設定 | 値 |
    | --- | --- |
    | プロパティ | **jobTitle** |
    | オペレーター | **Equals** |
    | Value | **クラウド管理者** |

1. ルールを保存し、「**新しいグループ**」 ブレードに戻って 「**作成**」 をクリックします。 

1. Azure AD テナントの 「**グループ - すべてのグループ**」 ブレードに戻り、 「**+ 新しいグループ**」 ボタンをクリックし、次の設定で新しいグループを作成します。

    | 設定 | 値 |
    | --- | --- |
    | グループ タイプ | **セキュリティ** |
    | グループ名 | **IT システム管理者** |
    | グループの説明 | **Contoso IT システム管理者** |
    | メンバーシップ タイプ | **動的ユーザー** |

1. 「**動的クエリの追加**」 をクリックします。 

1. 「**動的メンバーシップ ルール**」 ブレードの 「**ルールの構成**」 タブで、次の設定を使用して新しい規則を作成します。

    | 設定 | 値 |
    | --- | --- |
    | プロパティ | **jobTitle** |
    | 演算子 | **Equals** |
    | 値 | **System Administrator** |

1. ルールを保存し、「**新しいグループ**」 ブレードに戻って 「**作成**」 をクリックします。 

1. Azure AD テナントの 「**グループ | すべてのグループ**」 ブレードに戻り、「**+ 新しいグループ**」 ボタンをクリックし、次の設定で新しいグループを作成します。

    | 設定 | 値 |
    | --- | --- |
    | グループ タイプ | **セキュリティ** |
    | グループ名 | **IT ラボ管理者** |
    | グループの説明 | **Contoso IT ラボ管理者** |
    | メンバーシップ タイプ | **割り当て済み** |

1. **メンバーが選択されていません** をクリックします。 

1. 「**メンバーの追加**」 ブレードで 、「**IT クラウド 管理者 グループ**」 と 「**IT システム管理者グループ**」 を検索して選択し、「**新規グループ**」 ブレードに戻り、**作成**をクリックします。

1. 「**グループ - すべてのグループ**」 ブレードに戻り、「**IT クラウド管理者**」 グループのエントリをクリック し、「**メンバー**」ブレードを表示します。グループ メンバーのリストに「**az104-01a-aaduser1**」が表示されていることを確認します。

1. 「**グループ - すべてのグループ**」 ブレードに戻り、「**IT システム管理者**」 グループのエントリをクリック し、「**メンバー**」ブレードを表示します。グループ メンバーのリストに「**az104-01a-aaduser2**」が表示されていることを確認します。

    >**注**: 動的メンバーシップ グループの更新に遅延が発生する可能性があります。更新を迅速化するには、「グループ」ブレードに移動し、「動的メンバーシップ ルール」 ブレードを表示し、「ルール構文」 テキスト ボックスに一覧表示されているルールの末尾に空白を追加することで編集し、変更を保存します。

#### タスク 3: Azure Active Directory (AD) テナントを作成する

このタスクでは、新しい Azure AD テナントを作成します。

1. Azure portal で、**Azure Active Directory** を検索し、選択します。

1. 「**+ ディレクトリの作成**」 をクリックし、

    | 設定 | 値 |
    | --- | --- |
    | ディレクトリ タイプ | **Azure Active Directory** |
    | 組織名 | **Contoso Lab** |
    | 初期ドメイン名 | 小文字と数字で構成され、文字で始まる有効な DNS 名 | 
    | 国/地域 | **米国** |

   > **注意**: **初期ドメイン名** テキスト ボックスに表示される緑色のチェック マークは、入力したドメイン名が有効で一意であることを示します。

1. 「**Review + create**」 をクリックしてから、「**作成**」 をクリックします。

1. 新しく作成した Azure AD テナントのブレードを表示するには、**ここをクリックして新しいディレクトリに移動するか、 Azure portal のツール バーにあるContoso Lab** リンクまたは **Directory + Subscription** ボタン (「Cloud Shell」ボタンの右側) をクリックします。

#### タスク 4: Azure AD ゲストユーザーを管理します。

このタスクでは、Azure AD ゲスト ユーザーを作成し、Azure サブスクリプション内のリソースへのアクセスを許可します。

1. Contoso Lab Azure AD テナントを表示する Azure portal の**管理** セクションで、 **ユーザー**をクリックし、 「**+ 新しいユーザー**」 をクリックします。

1. 次の設定で新しいユーザーを作成します (その他は既定のままにします)。

    | 設定 | 値 |
    | --- | --- |
    | ユーザー名 | **az104-01b-aaduser1** |
    | 名前 | **az104-01b-aaduser1** |
    | パスワードを作成します | enabled |
    | 初期パスワード | **Pa55w.rd124** |
    | 役職 | **システム管理者** |
    | 部署 | **IT** |

    >**注**: **クリップボードにフル ユーザー名** をコピーしてください。 これは、タスクの後半で必要となります。

1. Azure portal のツール バーにある 「**Directory + Subscription**」 ボタン (「Cloud Shell」 ボタンの右側) を使用して、既定の Azure AD テナントに切り替えます。

1. 「**ユーザー - すべてのユーザー**」 ブレードに戻り、 「**+ 新しいゲスト ユーザー**」 をクリックします。

1. 次の設定で新しいゲストユーザーを作成します (他のユーザーはデフォルトのままにします)。

    | 設定 | 値 |
    | --- | --- |
    | 名前 | **az104-01b-aaduser1** |
    | メール アドレス | このタスクの前にクリップボードにコピーした値を貼り付けます |
    | 使用場所 | **米国** |
    | 役職 | **Lab 管理者** |
    | 部署 | **IT** |

1. 「**招待**」 をクリック します。  

1. 「**ユーザー - すべてのユーザー**」 ブレードに戻り、新しく作成されたゲスト ユーザー アカウントを表すエントリをクリックします。

1. 「**az104-01b-aaduser1 - プロファイル**」 ブレードで、「**グループ**」 をクリックします。

1. 「**+ メンバーシップの追加**」 をクリックし、ゲスト ユーザー アカウントを **IT Lab 管理者グループ** に追加します。


#### リソースのクリーンアップ

   >**注**: 使用しない新しく作成された Azure リソースは必ず削除してください。使用していないリソースを削除することで、予期しないコストが発生しなくなります。この場合、Azure Active Directory テナントとそのオブジェクトに関連する追加料金は発生しませんが、この課題で作成したユーザー アカウント、グループ アカウント、および Azure Active Directory テナントの削除を検討する必要があります。

1. Azure portal で、「**ユーザー - すべてのユーザー**」 ブレードに移動し、 **az104-01b-aaduser1** ゲスト ユーザー アカウントを表すエントリをクリックし 、「**az104-01b-aaduser1 - プロファイル**」 ブレードで、「**削除**」 をクリックし, 確認画面が表示されたら、「**OK**」 をクリックします。

1. 同じ手順を繰り返して、このラボで作成した残りのユーザー アカウントを削除します。

1. 「**グループ - すべてのグループ**」 ブレードに移動し、このラボで作成したグループを選択し、「**削除**」 をクリックして 確認画面が表示されたら、「**OK**」 をクリックします。

1. 「**Azure Active Directory Premium P2 - ライセンスユーザー**」 ブレードに移動し、このラボでライセンス割り当て済みのユーザー アカウントを選択し、「**ライセンスの削除**」 をクリックします。確認画面が表示されたら、「**OK**」 をクリックします

1. Azure portal で、ツール バー「**Directory + Subscription**」 ボタン (「Cloud Shell」 ボタンの右側) を試用して、Contoso Lab Azure AD テナントのブレードを表示します。

1. 「**ユーザー - すべてのユーザー**」 ブレードに移動し、**az104-01b-aaduser1** ユーザー アカウントのエントリをクリックします。「**az104-01b-aaduser1 - プロファイル**」 ブレード上で 「**削除**」 をクリックし、確認画面が表示されたら 「**OK**」 をクリックします。

1. Contoso Lab Azure AD テナントの 「**Contoso Lab - 概要**」 ブレードに移動し、「**ディレクトリの削除**」 をクリックします。Contoso Labディレクトリの 「削除」 ブレードで、「**Azure リソースを削除するアクセス許可を取得します**」 リンクをクリックし、Azure Active Directory の 「**プロパティ**」 ブレードで 「**Azure リソースのアクセス管理**」 を「**Yes**」 に設定し、「**保存**」 をクリックします。

1. Azure portal からサインアウトし、ログインし直します。 

1. 「**ディレクトリの削除 'Contoso Lab'**」 ブレードに戻り、「**削除**」 をクリック します。

#### レビュー

このラボでは、次の内容を学習しました。

- Azure AD ユーザーの作成と構成
- 割り当て済みおよび動的メンバーシップを持つ Azure AD グループの作成
- Azure Active Directory (AD) テナントの作成
- Azure AD ゲスト ユーザーの管理 