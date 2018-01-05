---
title: "NuGet 3.2 RC のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 330577fa-7965-4433-98ad-b4b4575e1452
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.2 RC のリリース ノートします。"
keywords: "NuGet 3.2 RC のリリース ノート、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4b5f83f521cb326f5b3a5e6c202cdcb77acde5e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-32-rc-release-notes"></a>NuGet 3.2 RC のリリース ノートには

[NuGet 3.1.1 リリース ノート](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 リリース ノート](../release-notes/nuget-3.2.md)

NuGet 3.2 リリース候補版がリリースされた機能強化や、3.1.1 の修正プログラムのコレクションとして、2015 年 9 月 2日をリリースします。  また、これらは、まず新しい dist.nuget.org リポジトリに公開されている最初のリリースです。

## <a name="new-features"></a>新機能

* 同じフォルダーに存在するプロジェクトを異なるようになりましたが`project.json`ファイルをフォルダーの各プロジェクトに固有です。  各プロジェクトの名前、`project.json`ファイル`{ProjectName}.project.json`NuGet を正しく参照してプロジェクトごとにそのコンテンツを適切に使用するとします。  新しい機能をサポートしているこの[1102](https://github.com/NuGet/Home/issues/1102)
* `NuGet.Config`では、相対パス - として globalPackagesFolder [1062](https://github.com/NuGet/Home/issues/1062)

## <a name="command-line-updates"></a>更新プログラムのコマンドライン

これは、NuGet v3 のサーバーをサポートする nuget.exe クライアントの最初のバージョンで管理されているプロジェクトのパッケージを復元する、`project.json`ファイル。

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a>さまざまなクライアントとのやり取りを向上させるためには、このリリースで解決された認証済みのフィードの問題が発生しました。

* インストールの復元の相互作用 - 認証されたフィードには、最初の要求の資格情報の送信だけ/ [1300](https://github.com/NuGet/Home/issues/1300)、 [456](https://github.com/NuGet/Home/issues/456)
* Push コマンドからの構成 - 資格情報が解決しない[1248](https://github.com/NuGet/Home/issues/1248)
* ユーザー エージェントとヘッダーが NuGet リポジトリが統計情報の追跡のために送信されるようになりました[929](https://github.com/NuGet/Home/issues/929)

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a>多数の NuGet リポジトリをリモートで作業しようとしています。 ネットワーク障害を適切に処理する機能強化を行いました。

* -リモートのフィードに接続できない場合に、エラー メッセージが改善[1238](https://github.com/NuGet/Home/issues/1238)
* 正常時に返される 1、エラー状態が発生した - NuGet 復元コマンドを修正[1186](https://github.com/NuGet/Home/issues/1186)
* 今すぐネットワーク接続の再試行すべて 200 ミリ秒の場合は HTTP 5xx エラー: 5 回試行の最大の[1120](https://github.com/NuGet/Home/issues/1120)
* Push コマンドの中にサーバーのリダイレクト応答の処理強化[1051](https://github.com/NuGet/Home/issues/1051)
* `nuget install -source`では、URL またはリポジトリ名の引数として無効です Nuget.Config を[1046。](https://github.com/NuGet/Home/issues/1046)
* いないに配置されていたリポジトリの復元中に足りないパッケージが警告ではなくエラーとして報告されるようになりました[1038](https://github.com/NuGet/Home/issues/1038)
* Unix または Linux のシナリオ - \r\n の multipartwebrequest 処理を修正[776](https://github.com/NuGet/Home/issues/776)

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a>さまざまなコマンドに関する問題の修正プログラムの数があります。

* Push コマンドが、パッケージ ソースの構成 - に対して put コマンドの前に、の取得を行いません[1237](https://github.com/NuGet/Home/issues/1237)
* 一覧のコマンドは、バージョン番号を不要になった繰り返されます[1185](https://github.com/NuGet/Home/issues/1185)
* パック-ビルド引数を持つようになりました正しくサポートする c# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)
* Visual Studio 2015 - で修正された問題の f# プロジェクトをパックしていますがビルドされた[1048](https://github.com/NuGet/Home/issues/1048)
* パッケージは既に存在 - したときに、今すぐいいえ ops を復元[1040](https://github.com/NuGet/Home/issues/1040)
* 強化されたエラー メッセージ`packages.config`ファイル形式が正しくありません - [1034](https://github.com/NuGet/Home/issues/1034)
* 復元コマンドでの修正`-SolutionDirectory`- の相対パスを使用するスイッチ[992](https://github.com/NuGet/Home/issues/992)
* ソリューション全体の更新プログラム - をサポートするために更新されたコマンドの向上[924](https://github.com/NuGet/Home/issues/924)

このリリースで解決される問題の完全な一覧は含まれて NuGet GitHub[コマンド ライン マイルス トーン](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)です。

## <a name="visual-studio-extension-updates"></a>Visual Studio 拡張機能の更新

### <a name="new-features-in-visual-studio"></a>Visual Studio での新機能

* により、パッケージを復元する際に、ソリューションをビルドするソリューション ノードで、ソリューション エクスプ ローラーに追加された新しいコンテキスト メニュー項目 ([1274](https://github.com/NuGet/Home/issues/1274))。

![新しいコンテキスト メニュー項目の 'パッケージを復元'](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a>更新し、Visual Studio での修正

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a>認証されたフィードに対する修正プログラム ロールアップし、拡張機能でアドレス指定されます。  拡張機能に、以下の認証は行われても。

* これで、フィードを正しく認証 NuGet v3 を正しく処理の代わりに v2 認証フィード - として[1216](https://github.com/NuGet/Home/issues/1216)
* 認証の資格情報を使用するプロジェクトで修正された要求`project.json`v2 フィード - との通信および[1082](https://github.com/NuGet/Home/issues/1082)

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a>ネットワーク接続には、Visual Studio で、ユーザー インターフェイスが影響を受けるし、次の修正プログラムとこれに対処し。

* パッケージのバージョンでのローカル キャッシュの保守性の向上[1096](https://github.com/NuGet/Home/issues/1096)
* フィードを不要になったしようとすると v2 フィード - として扱うことを示す v3 に接続するときにエラーの動作を変更[1253](https://github.com/NuGet/Home/issues/1253)
* 複数のパッケージ ソースのパッケージをインストールするときに、インストールの失敗を防ぐようになりました[1183](https://github.com/NuGet/Home/issues/1183)

おには、ビルド操作との対話の処理が向上しました。

* 1 つのプロジェクトが失敗した場合 - のパッケージを復元する場合は、プロジェクトをビルドを続行するようになりました[1169](https://github.com/NuGet/Home/issues/1169)
* ソリューションの再構築 - 強制的に、ソリューション内の別のプロジェクトが依存するプロジェクトにパッケージをインストールする[981](https://github.com/NuGet/Home/issues/981)
* -プロジェクトへの変更を正しくロールバックに失敗したパッケージのインストールを修正[1265](https://github.com/NuGet/Home/issues/1265)
* 不注意による削除の修正、`developmentDependency`属性内のパッケージで`packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)
* 呼び出す`install.ps1`ある適切な`$package.AssemblyReferences`に渡されたオブジェクト[1245](https://github.com/NuGet/Home/issues/1245)
* プロジェクトが、正常な状態の間を UWP プロジェクトでパッケージのアンインストールを妨げなく[1128](https://github.com/NuGet/Home/issues/1128)
* ソリューションが混在している`packages.config`と`project.json`せず、2 番目のプロジェクトが正しくビルドようになりましたビルド操作 - [1122](https://github.com/NuGet/Home/issues/1122)
* リンクまたは別のフォルダーに配置された場合、app.config ファイルを正しく検索[1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894)
* UWP プロジェクトが一覧にないパッケージをインストールできるよう[1109](https://github.com/NuGet/Home/issues/1109)
* パッケージの復元は今すぐ、ソリューションが許可されません - 保存された状態で[1081](https://github.com/NuGet/Home/issues/1081)


ファイルが修正された構成への更新を処理します。

* パッケージの後続のビルドを上から配信されなくターゲット ファイルを削除する、`project.json`マネージ プロジェクトに[1288](https://github.com/NuGet/Home/issues/1288)
* 不要になった - ASP.NET 5 ソリューションのビルド中に Nuget.Config ファイルの変更[1201](https://github.com/NuGet/Home/issues/1201)
* パッケージの更新プログラムの中にバージョン制約を許可される変更されなく[1130](https://github.com/NuGet/Home/issues/1130)
* ロック ファイル今すぐロックされたままのビルド時に[1127](https://github.com/NuGet/Home/issues/1127)
* 今すぐ変更`packages.config`いない更新プログラムの中に書き換えたと[585](https://github.com/NuGet/Home/issues/585)


ソース管理の TFS とのやり取りが改善されます。

* 不要になった - TFS にバインドされているパッケージのインストールが失敗している[番号 1164](https://github.com/NuGet/Home/issues/1164)、 [980](https://github.com/NuGet/Home/issues/980)
* TFS 2013 の統合に使用できるように修正された NuGet ユーザー インターフェイス[1071](https://github.com/NuGet/Home/issues/1071)
* 正しくパッケージ フォルダーに由来する復元パッケージへの参照を修正[1004](https://github.com/NuGet/Home/issues/1004)

最後に、私たちも向上してこれらの項目。

* ログ メッセージの詳細度が小さくなります`project.json`マネージ プロジェクトに[1163](https://github.com/NuGet/Home/issues/1163)
* これで、正しくインストールされているバージョンのパッケージ、ユーザー インターフェイスで表示・ [1061](https://github.com/NuGet/Home/issues/1061)


Visual Studio 拡張機能は含まれて NuGet GitHub の課題の完全な一覧[3.2 マイルス トーン](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)

## <a name="known-issues"></a>既知の問題

あることができます、GitHub の問題一覧上の問題を追跡するために続行: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)