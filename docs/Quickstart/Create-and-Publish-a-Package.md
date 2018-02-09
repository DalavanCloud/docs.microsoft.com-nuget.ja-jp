---
title: "NuGet パッケージを作成して公開するための入門ガイド | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/03/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "nuget.exe コマンドライン インターフェイスと Visual Studio の両方を使用して、NuGet パッケージを作成して公開するチュートリアル。"
keywords: "NuGet パッケージの作成、NuGet パッケージの公開、NuGet チュートリアル"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 53d29283c9e786fc27e9a608d7d251d8d0b5b0b2
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2018
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="8e570-104">パッケージの作成と公開</span><span class="sxs-lookup"><span data-stu-id="8e570-104">Create and publish a package</span></span>

<span data-ttu-id="8e570-105">.NET クラス ライブラリから NuGet パッケージを作成して、nuget.org に公開する簡単なプロセスです。この記事では、NuGet コマンド ライン インターフェイス (CLI) と Visual Studio を使用して、このプロセスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="8e570-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. This article walks you through the process using the NuGet command-line interface (CLI) and Visual Studio.</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="8e570-106">前提条件</span><span class="sxs-lookup"><span data-stu-id="8e570-106">Pre-requisites</span></span>

1. <span data-ttu-id="8e570-107">[visualstudio.com](https://www.visualstudio.com/) から Visual Studio 2017 の任意のエディションをインストールします。</span><span class="sxs-lookup"><span data-stu-id="8e570-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="8e570-108">[nuget.org/downloads](https://nuget.org/downloads) から `nuget.exe` の最新バージョンをダウンロードし、`.exe` を自分の PATH 内の場所に保存することで、NuGet CLI ツール `nuget.exe` をインストールします。</span><span class="sxs-lookup"><span data-stu-id="8e570-108">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="8e570-109">ダウンロードされるのは、インストーラーではなく、ツール*そのもの*であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8e570-109">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="8e570-110">パッケージ化するコードに適した .NET クラス ライブラリ プロジェクトを作成します。</span><span class="sxs-lookup"><span data-stu-id="8e570-110">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="8e570-111">プロジェクトがまだない場合は、次の手順で単純なものを作成できます。</span><span class="sxs-lookup"><span data-stu-id="8e570-111">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="8e570-112">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C#]、[Windows]** ノードの順に展開して "クラス ライブラリ" テンプレートを選択し、プロジェクトに AppLogger という名前を付け、**[OK]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="8e570-112">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="8e570-113">作成されたプロジェクト ファイルを右クリックし、**[ビルド]** を選択して、プロジェクトが正しく作成されたことを確認します。</span><span class="sxs-lookup"><span data-stu-id="8e570-113">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="8e570-114">DLL は、デバッグ フォルダー (または代わりにその構成をビルドした場合はリリース フォルダー) 内にあります。</span><span class="sxs-lookup"><span data-stu-id="8e570-114">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="8e570-115">実際の NuGet パッケージ内ではもちろん、多くの便利な機能を実装して、他の人がその上にアプリケーションをビルドできます。</span><span class="sxs-lookup"><span data-stu-id="8e570-115">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="8e570-116">しかし、このチュートリアルでは、パッケージを作成するには、テンプレートのクラス ライブラリで十分なため、追加のコードを記述することはありません。</span><span class="sxs-lookup"><span data-stu-id="8e570-116">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="8e570-117">.nuspec パッケージ マニフェスト ファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="8e570-117">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="8e570-118">すべての NuGet パッケージには、その内容と依存関係を説明するマニフェスト &mdash;`.nuspec` ファイル&mdash; が必要です。</span><span class="sxs-lookup"><span data-stu-id="8e570-118">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="8e570-119">`nuget spec` コマンドを使用してこのファイルを作成し、カスタマイズすることができます。</span><span class="sxs-lookup"><span data-stu-id="8e570-119">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="8e570-120">この例では、プロジェクト ファイルから `.nuspec` を作成します。マニフェストは、[パッケージの作成](../create-packages/creating-a-package.md)ページで説明されているような他の方法でも作成できます。</span><span class="sxs-lookup"><span data-stu-id="8e570-120">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="8e570-121">コマンド プロンプトを開き、プロジェクト ファイル (`.csproj`) が格納されているフォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="8e570-121">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="8e570-122">NuGet CLI `spec` コマンドを実行してマニフェストを生成すると、プロジェクトにちなんだ名前 (`AppLogger.nuspec` など) が付けられます。</span><span class="sxs-lookup"><span data-stu-id="8e570-122">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="8e570-123">テキスト エディターでファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="8e570-123">Open the file in a text editor.</span></span> <span data-ttu-id="8e570-124">マニフェストは次のコードのようになります。`<token>` の形式のトークン (`$id$` など) は、パッケージ化プロセス中にプロジェクトの Properties/AssemblyInfo.cs ファイルからの値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="8e570-124">The manifest looks something like the code below, where tokens in the form `<token>` (such as `$id$`) are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="8e570-125">トークンの詳細については、「[Creating the .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file)」 (.nuspec ファイルの作成) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8e570-125">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="8e570-126">nuget.org 全体で一意のパッケージ ID を選択します。[パッケージの作成](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)ページに記載されている名前付け規則を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="8e570-126">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="8e570-127">必ず作成者と説明のタグを更新してください。そうしないと、次の手順でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="8e570-127">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="8e570-128">例として更新された `.nuspec` ファイルを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="8e570-128">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="8e570-129">公開用にビルドされたパッケージの場合は、`<tags>` 要素に特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8e570-129">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="8e570-130">pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="8e570-130">Run the pack command</span></span>

<span data-ttu-id="8e570-131">プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`pack` コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="8e570-131">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```cli
nuget pack AppLogger.csproj
```

<span data-ttu-id="8e570-132">このコマンドは、`.nuspec` ファイルからパッケージの名前とバージョン番号を使用して、`AppLogger.1.0.0.0.nupkg` を作成します。</span><span class="sxs-lookup"><span data-stu-id="8e570-132">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="8e570-133">`.nuspec` ファイルのさまざまなフィールドを既定値から変更していない場合は、コマンドにより警告が発行されます。</span><span class="sxs-lookup"><span data-stu-id="8e570-133">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="8e570-134">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="8e570-134">Publish the package</span></span>

<span data-ttu-id="8e570-135">`.nupkg` ファイルを作成したら、`push` コマンドを使用してそれを nuget.org に公開します。</span><span class="sxs-lookup"><span data-stu-id="8e570-135">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="8e570-136">または、[nuget.org の公開ワークフロー](../create-packages/publish-a-package.md#publish-to-nugetorg)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="8e570-136">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="8e570-137">nuget.org に公開するパッケージは、他の開発者に公開されます。</span><span class="sxs-lookup"><span data-stu-id="8e570-137">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="8e570-138">パッケージを非公開でホストするには、[パッケージのホスティング](../hosting-packages/overview.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="8e570-138">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>

1. <span data-ttu-id="8e570-139">[nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) に無料のアカウントを作成するか、既にある場合はログインします。</span><span class="sxs-lookup"><span data-stu-id="8e570-139">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="8e570-140">新しいアカウントを作成すると、確認メールが送信されます。</span><span class="sxs-lookup"><span data-stu-id="8e570-140">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="8e570-141">パッケージをアップロードするには、その前にアカウントを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8e570-141">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="8e570-142">ログイン後、(右上で) ユーザー名を選択し、**[API キー]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="8e570-142">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="8e570-143">**[作成]** を選択し、キーの名前を入力し、**[API キー]** の下で **[スコープの選択]、[プッシュ]** の順に選択し、**[glob パターン]** に「*」を入力し、\*\*[作成]*\* を選択します。</span><span class="sxs-lookup"><span data-stu-id="8e570-143">Select **Create**, provide a name for your key, select **Select Scopes > Push** under **API Key**, enter \* for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="8e570-144">キーが作成されたら、**[コピー]** を選択して、CLI で必要となるアクセス キーを取得します。</span><span class="sxs-lookup"><span data-stu-id="8e570-144">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![API キーをクリップボードにコピーする](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="8e570-146">安全な場所にキーを保存して、厳重に保管します。</span><span class="sxs-lookup"><span data-stu-id="8e570-146">Save your key in a secure location and keep it secret.</span></span> <span data-ttu-id="8e570-147">キーが誤って流出した場合は、いつでも再生成することができます。</span><span class="sxs-lookup"><span data-stu-id="8e570-147">If your key is accidentally revealed, you can regenerate it at any time.</span></span> <span data-ttu-id="8e570-148">CLI を通じてパッケージをプッシュする必要がなくなった場合は、API キーを削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="8e570-148">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="8e570-149">コマンド プロンプトで、次のコマンドでパッケージ名を指定し、キーを手順 4 でコピーした値に置き換えて、コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="8e570-149">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="8e570-150">nuget.exe によって公開プロセスの結果が表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e570-150">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="8e570-151">nuget.org のプロファイルから、**[パッケージの管理]** を選択して、公開したパッケージを確認します。</span><span class="sxs-lookup"><span data-stu-id="8e570-151">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="8e570-152">確認メールも送信されます。</span><span class="sxs-lookup"><span data-stu-id="8e570-152">You also receive a confirmation email.</span></span> <span data-ttu-id="8e570-153">パッケージがインデックス作成され、他のユーザーが検索して検索結果に表示されるようになるまでには、時間がかかる場合があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8e570-153">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="8e570-154">この間、パッケージのページに次のメッセージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="8e570-154">During that time your package page shows the message below:</span></span>

    ![このパッケージはまだインデックスされていません。](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="8e570-157">**ウイルス スキャン**: nuget.org にアップロードされたすべてのパッケージはウイルス スキャンが行われ、ウイルスが見つかった場合には拒否されます。</span><span class="sxs-lookup"><span data-stu-id="8e570-157">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="8e570-158">nuget.org の一覧にあるすべてのパッケージも定期的にスキャンされます。</span><span class="sxs-lookup"><span data-stu-id="8e570-158">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="8e570-159">以上です。</span><span class="sxs-lookup"><span data-stu-id="8e570-159">And that's it!</span></span> <span data-ttu-id="8e570-160">最初の NuGet パッケージが [nuget.org](https://www.nuget.org/) に公開され、他の開発者がそれを自身のプロジェクトで使用することができます。</span><span class="sxs-lookup"><span data-stu-id="8e570-160">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="8e570-161">関連トピック</span><span class="sxs-lookup"><span data-stu-id="8e570-161">Related topics</span></span>

- [<span data-ttu-id="8e570-162">パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="8e570-162">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="8e570-163">パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="8e570-163">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="8e570-164">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="8e570-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="8e570-165">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="8e570-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="8e570-166">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="8e570-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)