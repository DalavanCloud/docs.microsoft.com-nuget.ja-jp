---
title: NuGet クライアント ツールのインストール
description: Visual Studio 用にクライアント ツール、dotnet コマンド ライン インターフェイス (CLI)、nuget CLI、およびパッケージ マネージャーをインストールするためのガイダンス。
author: karann-msft
ms.author: karann
ms.date: 04/09/2018
ms.topic: quickstart
ms.openlocfilehash: 9e8aa2250c6fc2843f74a925c56f953be5d48221
ms.sourcegitcommit: 1591bb230e106b94162a87dd1d86fe427366730a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2018
ms.locfileid: "52671137"
---
# <a name="installing-nuget-client-tools"></a>NuGet クライアント ツールのインストール

> **パッケージをインストールする場合は、[Nuget パッケージのインストール方法](consume-packages/ways-to-install-a-package.md)に関するページをご覧ください。**

パッケージ コンシューマーまたはパッケージ作成者として NuGet を使用するには、[コマンド ライン インターフェイス (CLI) ツール](#cli-tools)だけでなく、[Visual Studio の NuGet 機能](#visual-studio)も使用できます。 この記事では、さまざまなツールの機能とそれらのインストール方法について簡単に説明します。また、各ツールの[機能の可用性](#feature-availability)の比較も示します。 NuGet でパッケージの利用を開始するには、パッケージをインストールして使用する方法に関するページを参照してください ([.NET CLI](quickstart/install-and-use-a-package-using-the-dotnet-cli.md) 向けページと [Visual Studio](quickstart/install-and-use-a-package-in-visual-studio.md) 向けページがあります)。 NuGet パッケージの作成を開始するには、NET Standard パッケージの作成と公開に関するページを参照してください ([dotnet CLI](quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) 向けページと [Visual Studio](quickstart/create-and-publish-a-package-using-visual-studio.md) 向けページがあります)。

| ツール&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 説明 | ダウンロード&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
|:------------- |:-------------|:-----|
| [dotnet.exe](#dotnetexe-cli) | .NET Core SDK 含まれており、すべてのプラットフォームで NuGet のコア機能を提供します。 | [.NET Core SDK](https://www.microsoft.com/net/download/) |
| [nuget.exe](#nugetexe-cli) | Windows のすべての NuGet 機能と、Mono で実行される場合の Mac および Linux の ほとんどの機能を提供します。 | [nuget.exe](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) |
| [Visual Studio](#visual-studio) | Windows 上で、パッケージ マネージャー UI およびパッケージ マネージャー コンソール (.NET 関連のワークロードに含まれます) を介して NuGet 機能を提供します。 Mac 上で、UI 経由で特定の機能を提供します。 Visual Studio Code で、拡張機能によって NuGet 機能が提供されます。 | [Visual Studio 2017](https://www.visualstudio.com/downloads/) |

さらに、[MSBuild CLI](reference/msbuild-targets.md) は、パッケージを復元および作成する機能を提供します。これはおもにビルド サーバーで有用です。 MSBuild は、NuGet を使用するための汎用ツールではありません。

## <a name="cli-tools"></a>CLI ツール

`dotnet.exe` と `nuget.exe` の 2 つの NuGet CLI ツールがあります。 比較については、「[機能の可用性](#feature-availability)」をご覧ください。

### <a name="dotnetexe-cli"></a>dotnet.exe CLI

.NET Core 2.0 CLI (`dotnet.exe`) は、すべてのプラットフォーム (Windows、Mac、Linux) で機能し、パッケージのインストール、復元、および公開など、NuGet のコア機能を提供します。 `dotnet` は、.NET Core プロジェクト ファイル (`.csproj`など) に直接統合されます。これは、ほとんどのシナリオで役立ちます。 また、`dotnet` は、各プラットフォーム用に直接構築されているので、Mono をインストールする必要はありません。

インストール:

- 開発者用コンピューターに [.NET Core SDK](https://aka.ms/dotnetcoregs) をインストールします。
- ビルド サーバーの場合は、「[継続的インテグレーション (CI) で .NET Core SDK とツールを使用する](/dotnet/core/tools/using-ci-with-cli)」の手順に従ってください。

詳細については、[.NET Core コマンド ライン インターフェイス ツール](/dotnet/core/tools/index?tabs=netcore2x#tabpanel_fXL5YCOYDa_netcore2x)に関するセクションをご覧ください。

### <a name="nugetexe-cli"></a>nuget.exe CLI

NuGet CLI (`nuget.exe`) は、すべての NuGet 機能を提供する Windows 用のコマンド ライン ユーティリティです。[Mono](http://www.mono-project.com/docs/getting-started/install/) を使用して Mac OSX および Linux でも実行できますが、いくつかの制限があります。 `dotnet` とは異なり、`nuget.exe` CLI はプロジェクト ファイルに影響を与えず、パッケージのインストール時に `packages.config` を更新しません。

インストール:

[!INCLUDE [install-cli](includes/install-cli.md)]

> [!Tip]
> Windows で既存の nuget.exe を最新バージョンに更新するには、`nuget update -self` を使用します。

> [!Note]
> 最新の推奨される NuGet CLI はいつでも、`https://dist.nuget.org/win-x86-commandline/latest/nuget.exe` で入手できます。 古い継続的インテグレーション システムとの互換性を維持するために、以前の URL (`https://nuget.org/nuget.exe`) では現在、[非推奨の 2.8.6 CLI ツール](https://github.com/NuGet/NuGetGallery/issues/5381)が提供されています。

## <a name="visual-studio"></a>Visual Studio

- Visual Studio Code: NuGet 機能は、Marketplace 拡張機能から入手できます。また、CLI ツールの `dotnet.exe` または `nuget.exe` を使用して入手することもできます。

- Visual Studio for Mac: NuGet の機能は直接組み込まれています。 チュートリアルについては、「[プロジェクトに NuGet パッケージを含める](/visualstudio/mac/nuget-walkthrough)」をご覧ください。 他の機能については、CLI ツールの `dotnet.exe` または `nuget.exe` を使用します。

- Windows 上の Visual Studio: **NuGet パッケージ マネージャー**は、Visual Studio 2012 以降に含まれます。 パッケージ マネージャーは、[パッケージ マネージャー UI](tools/package-manager-ui.md) と[パッケージ マネージャー コンソール](tools/package-manager-console.md)を提供します。NuGet の操作のほとんどは、これらを使用して実行できます。
  - Visual Studio 2017 インストーラーには、NuGet パッケージ マネージャーと .NET を使用するすべてのワークロードが含まれます。 個別にインストール、またはパッケージ マネージャーがインストールされていることを確認するには、Visual Studio 2017 インストーラーを実行し、**[個別のコンポーネント] > [コード ツール] > [NuGet パッケージ マネージャー]** の下でオプションを確認します。
  - パッケージ マネージャー UI とパッケージ マネージャー コンソールは、Windows 上の Visual Studio 固有です。 現在、Visual Studio for Mac では、これらを使用できません。
  - Visual Studio では、`nuget.exe` CLI が自動的に含まれないため、前述のとおり、個別にインストールする必要があります。
  - パッケージ マネージャー コンソール コマンドは、Windows 上の Visual Studio 内でのみ機能し、他の PowerShell 環境では機能しません。
  - Visual Studio 2010 以前の場合、"Visual Studio 用 NuGet パッケージ マネージャー" 拡張機能をインストールします。
  - さらに、Visual Studio 2013 および 2015 用の NuGet 拡張機能は、[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)からダウンロードできます。
  - リリース予定の NuGet の機能をプレビューしたい場合は、[Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/) をインストールします。これは、Visual Studio の安定版リリースと同時に実行できます。 問題を報告したり、プレビューに関するアイデアを共有したりするには、[NuGet GitHub リポジトリ](https://github.com/Nuget/Home/issues)で懸案事項を開きます。

## <a name="feature-availability"></a>機能の可用性

| 機能 | dotnet CLI | nuget CLI (Windows) | nuget CLI (Mono) | Visual Studio (Windows) | Visual Studio for Mac |
| --- | --- | --- | --- | --- | --- |
| パッケージの検索 |  | &#10004; | &#10004; | &#10004; | &#10004; |
| パッケージのインストール/アンインストール | &#10004; | &#10004;(1) | &#10004; | &#10004; | &#10004; |
| パッケージの更新 | &#10004; | &#10004; | | &#10004; | &#10004; |
| パッケージの復元 | &#10004; | &#10004; | &#10004;(2) | &#10004; | &#10004; |
| パッケージ フィードの管理 (ソース) | | &#10004; | &#10004; | &#10004; | &#10004; |
| フィード上でのパッケージの管理 | &#10004; | &#10004; | &#10004; | | |
| フィードの API キーの設定 | | &#10004; | &#10004; | | |
| パッケージの作成 (3) | &#10004; | &#10004; | &#10004;(4) | &#10004; | |
| パッケージの公開 | &#10004; | &#10004; | &#10004; | &#10004; |  |
| パッケージのレプリケート |  | &#10004; | &#10004; | | |
| "*グローバル パッケージ*" フォルダーおよびキャッシュ フォルダーの管理 | &#10004; | &#10004; | &#10004; | | |
| NuGet の構成の管理 | | &#10004; | &#10004; | | |

(1) プロジェクト ファイルには影響しません。代わりに `dotnet.exe` を使用します。

(2) `packages.config` ファイルでのみ機能し、ソリューション (`.sln`) ファイルでは機能しません。

(3) 各種の高度なパッケージ機能は、Visual Studio UI ツールで表示されない場合のみ、CLI を通じて使用できます。

(4) `.nuspec` ファイルでは機能しますが、プロジェクト ファイルでは機能しません。

### <a name="related-topics"></a>関連トピック

- [dotnet コマンド](tools/dotnet-commands.md)
- [NuGet CLI リファレンス](tools/nuget-exe-cli-reference.md)
- [パッケージ マネージャー UI のリファレンス](tools/package-manager-ui.md)
- [パッケージ マネージャー コンソールのリファレンス](tools/package-manager-console.md)
- [パッケージ マネージャー コンソール PowerShell のリファレンス](tools/powershell-reference.md)
- [パッケージの作成](create-packages/creating-a-package.md)
- [パッケージの公開](create-packages/publish-a-package.md)

さらに、Windows で作業する開発者は、[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)を探索することもできます。これは、NuGet パッケージを視覚的に調査、作成、および編集する、オープン ソースのスタンドアロン ツールです。 たとえば、パッケージをリビルドせずにパッケージ構造に試験的な変更を加える際に非常に役立ちます。
