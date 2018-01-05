---
title: "復元コマンドは NuGet CLI |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Nuget.exe restore コマンドのリファレンス"
keywords: "nuget の参照を復元、restore コマンドのパッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a>restore コマンド (NuGet CLI)

**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 2.7 +

NuGet 2.7 +: ダウンロードし、表示されないすべてのパッケージをインストール、`packages`フォルダーです。

NuGet 3.3 + を使用するプロジェクトと`project.json`: が生成されます、`project.lock.json`ファイルと`<project>.nuget.props`ファイル、必要な場合です。 (両方のファイルをソース管理から省略できます)。

NuGet 4.0 以降でプロジェクトをパッケージで参照が含まれますプロジェクト ファイルで直接: 生成、`<project>.nuget.props`ファイルの場合は、必要に応じて、`obj`フォルダーです。 (ファイルをソース管理から省略できます)。

Mac OSX およびモノラルで CLI を使用して Linux では、パッケージの復元はサポートされていません PackageReference 形式とします。

## <a name="usage"></a>使用方法

```
nuget restore <projectPath> [options]
```

ここで`<projectPath>`、ソリューションの場所を指定します、`packages.config`ファイル、または`project.json`ファイル。 参照してください[解説](#remarks)下詳細については動作します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| DirectDownload | *(4.0 以降)*バイナリなどのメタデータ キャッシュの値を設定せず直接パッケージをダウンロードします。 |
| DisableParallelProcessing | 同時に複数のパッケージの復元を無効にします。 |
| FallbackSource | *(3.2 +)*プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| MSBuildPath | *(4.0 以降)*よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。 |
| MSBuildVersion | *(3.2 +)*このコマンドで使用する MSBuild のバージョンを指定します。 サポートされている値は、4、12、14、15 です。 既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。 |
| NoCache | NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。 |
| 非対話型 | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| OutputDirectory | パッケージがインストールされているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 |
| PackageSaveMode | パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`です。 |
| パッケージファイル | `OutputDirectory` と同じ。 |
| Project2ProjectTimeOut | タイムアウト (秒) プロジェクト間参照を解決するためです。 |
| 再帰 | *(4.0 以降)* UWP と .NET Core プロジェクトのすべての参照プロジェクトを復元します。 使用してプロジェクトには適用されません`packages.config`です。 |
| RequireConsent | ダウンロードして、パッケージをインストールする前にパッケージを復元が有効になっていることを確認します。 詳細については、「[パッケージの復元](../consume-packages/package-restore.md)です。 |
| SolutionDirectory | ソリューション フォルダーを指定します。 ソリューションのパッケージを復元するときに無効です。 |
| ソース | 復元操作に使用する (Url) とパッケージ ソースの一覧を指定します。 コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../Consume-Packages/Configuring-NuGet-Behavior.md)です。 |
| 詳細度 |> の出力に表示される詳細データの量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="remarks"></a>コメント

Restore コマンドでは、次の手順を実行します。

1. Restore コマンドの操作モードを決定します。
    projectPath ファイルの種類 | 動作
    | --- | --- |
    ソリューション (フォルダー) | NuGet 検索、`.sln`ファイルとそれ以外の場合はエラーを使用します。 `(SolutionDir)\.nuget`開始フォルダーとして使用されます。
    `.sln`ファイル | ソリューションで識別されるパッケージを復元します。エラーは、`-SolutionDirectory`を使用します。 `$(SolutionDir)\.nuget`開始フォルダーとして使用されます。
    `packages.config`、 `project.json`、またはプロジェクト ファイル | 解決して、依存関係をインストール ファイルに表示されているパッケージを復元します。
    その他のファイルの種類 | ファイルがあると見なされます、 `.sln` ; 上記と同じファイルのない場合は、ソリューションでは、NuGet により、エラーが発生します。
    (指定されていない projectPath) | -NuGet は、現在のフォルダーにソリューション ファイルを検索します。 パッケージ; を復元する 1 つが使用される 1 つのファイルが見つかった場合、複数のソリューションが見つからない場合は、NuGet は、エラーを示します。
    |-NuGet 検索ソリューション ファイルが存在しない場合、`packages.config`または`project.json`しパッケージを復元するを使用します。
    |-場合ないソリューション ファイル`packages.config`、または`project.json`が見つかると、NuGet は、エラーを示します。

1. 次の優先順位 (NuGet は、これらのフォルダーが見つからない場合に、エラーを提供) を使用して、パッケージ フォルダーを決定します。

    - `%userprofile%\.nuget\packages`値`project.json`です。
    - 指定されたフォルダー`-PackagesDirectory`です。
    - `repositoryPath`で vale`Nuget.Config`
    - 指定されたフォルダー`-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. ソリューションのパッケージを復元するには、NuGet は、次を行います。
    - ソリューション ファイルを読み込みます。
    - 表示されているソリューション レベルのパッケージを復元`$(SolutionDir)\.nuget\packages.config`に、`packages`フォルダーです。
    - 表示されているパッケージを復元`$(ProjectDir)\packages.config`に、`packages`フォルダーです。 指定されたパッケージごとに、必要ない限り、並列でパッケージを復元`-DisableParallelProcessing`を指定します。

## <a name="examples"></a>例

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```