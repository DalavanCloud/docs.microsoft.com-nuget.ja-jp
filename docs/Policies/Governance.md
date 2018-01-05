---
title: "NuGet プロジェクトのガバナンス | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 94c088ce-ec96-4876-a210-fbdae743942c
description: "コミッター、共同作成者、およびユーザーの役割と責任を含む、NuGet のガバナンス モデル。"
keywords: "NuGet ガバナンス, NuGet のヴェノベレント ディクテーター, コミッターの責任, 共同作成者の責任, ユーザーの責任"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: db2ed774b35d5698a88f9afba43fd30692001f6a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-governance"></a>NuGet のガバナンス

> この文書は、オックスフォード大学の[ヴェノベレント ディクテーター ガバナンス モデル](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel)に基づいています。 これは、[クリエイティブ コモンズの表示 - 継承 2.0 イングランド & ウェールズ ライセンス](http://creativecommons.org/licenses/by-sa/2.0/uk/)にライセンスされています。

NuGet プロジェクトのリーダーは、ヴェノベレント ディクテーターであり、管理はそのコミュニティが行います。 つまり、プロジェクトの日々のメンテナンスはコミュニティが積極的に行いますが、一般の戦略線はヴェノベレント ディクテーターによって描かれます。 意見の相違があった場合、ヴェノベレント ディクテーターが最終決定をします。

ヴェノベレント ディクテーターの仕事は、コミュニティ内の問題を解決し、プロジェクトを協調的に進めることです。 それに対して、コミュニティは、積極的に関わり貢献することによって、ヴェノベレント ディクテーターを意思決定に導きます。

## <a name="roles-and-responsibilities"></a>役割と責任

ここでは、ヴェノベレント ディクテーター、コミッター、共同作成者、およびユーザーの 4 つの役割について説明します。

### <a name="benevolent-dictator"></a>ヴェノベレント ディクテーター

ヴェノベレント ディクテーターまたはプロジェクト リーダーには、NuGet のコア チームが自己推薦されます。 ただし、コミュニティは常にフォークすることができるため、このチームはコミュニティに完全な釈明義務を負っています。 プロジェクト リーダーは、プロジェクトが長期にわたって継続されることを保証しながら、コミュニティ全体を理解し、相対するニーズを可能な限り満たすように努力することが期待されています。

ヴェノベレント ディクテーターの役割は、多くの意味で、独裁的に物事を進めるというよりは、交渉で進めます。 プロジェクトが拡大するときに、正しい人々がそれから影響を受け、プロジェクト リーダーのビジョンの下にコミュニティがまとまるようにすることが重要です。 このときのリーダーの責務は、コミッター (以下参照) がプロジェクトで正しい判断を下すことができるようにすることです。 一般的には、コミッターがプロジェクトの戦略と同調している限り、プロジェクト リーダーは彼らの希望通りに進めさせます。

.NET Foundation スタッフでは、これ以外に、プロジェクト リーダーは、ドメインの登録や技術的なサービス (コード署名など) を含むビジネス処理における Nuget の主な連絡窓口または最初の接点であると考えています。

### <a name="committers"></a>コミッター

コミッターとは、NuGet に継続的に貴重な貢献を行っている共同作成者であり、ヴェノベレント ディクテーターによって任命されます。 任命されると、コミッターはリポジトリに直接コードを書き込むこと、および他の作成者のコントリビューションを評価することの両方が求められます。 コミッターはしばしば開発者ですが、他の方法でも貢献します。

通常、コミッターは、コミュニティおよびプロジェクト リーダーからの尊敬を勝ち取るある水準の専門知識と知力をプロジェクトの特定の局面に提供します。 コミッターの役割は正式なものではなく、プロジェクト リーダーと仮定されるコミュニティに対する影響力があるメンバーが、単に助言やサポートを求めるポジションです。

コミッターは、NuGet の全体的な方向に関しては権限がありません。 ただし、プロジェクト リーダーからは話を聞いてもらえます。 コミュニティで求められていることや包括的な目標をリーダーに認識させ、プロジェクトに対する適切な寄稿の開発を支援したり、それを引き出すことがコミッターの仕事です。 しばしば、コミッターはコミッターの特定の担当専門領域を監督することを非公式に任されており、ソース コードの特定の領域を直接変更する権限が付与されています。 つまり、コミッターには意思決定を行う明確な権限はありませんが、彼らが取る行動は、リーダーによる決定としばしば同じです。

### <a name="contributors"></a>貢献者

共同作成者とは、NuGet に更新プログラムを提出するコミュニティ メンバーです。 これらの更新プログラムは、1 回限りのものと、経時的に発生するものとがあります。 最初は小規模な更新プログラムを提出し、共同作成者、コミッターおよびプロジェクト リーダーが共同作成者の更新プログラムの品質に問題がないと判断した場合に、それを徐々に大きくしていくことが共同作成者には期待されています。 共同作成者は、関連する製品のリリース ノートで確認できます。

最初の更新プログラムがリポジトリに配置される前に、共同作成者は、.NET Foundation の[貢献者ライセンス同意書](http://en.wikipedia.org/wiki/Contributor_License_Agreement)または譲渡契約書に署名する必要があります。 更新プログラムの提出および議論は可能ですが、実際に適切な書類なしにそれをリポジトリにコミットすることはできません。 貢献者ライセンス同意書を取得するには、[contributions@nuget.org](mailto:contributions@nuget.org) にリクエストを送信してください。

共同作成者になるには、次のいずれかのリポジトリにプル要求を送信してください。

- [NuGet クライアント](https://github.com/NuGet/NuGet.Client)
- [NuGet ギャラリー](https://github.com/nuget/nugetgallery)
- [NuGet Docs](https://github.com/nuget/nugetdocs)

プル要求を送信する詳細な手順は、リポジトリによって異なります。

- [NuGet クライアントと NuGet ギャラリーの寄稿手順](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [NuGet Docs の寄稿手順](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Users

ユーザーとは、パッケージの使用者または作成者として NuGet にニーズがあるコミュニティ メンバーです。 ユーザーは、コミュニティの最重要メンバーです。彼らがいないと、プロジェクトには目的がありません。 ユーザーは誰でもなることができ、特定の要件はありません。

ユーザーは可能な限り、NuGet の有効期間およびコミュニティに参加することが推奨されます。 プロジェクト チームは、ユーザーの貢献により、ユーザーのニーズを満たしていることを確認できます。 ユーザーの一般的なアクティビティの一部を次に示します。

- プロジェクトの使用に賛同する
- 新しいユーザーの視点からプロジェクトの長所と短所を開発者に伝える
- 精神的な支えとなる (ありがとうは大きな効果をもたらす)
- 文書やチュートリアルを記述する
- バグ レポートや機能要求を提出する
- バグ バッシュなどコミュニティのイベントに参加する
- インターネット上での掲示板またはフォーラムに参加する

プロジェクトとそのコミュニティへの関与を続けるユーザーは、しばしばそれにますます関わっていくことでしょう。 そのようなユーザーは、やがて前述の共同作成者になります。

## <a name="package-succession-under-special-circumstances"></a>特別な状況下でのパッケージの継承
NuGet のアカウント所有者が、不幸にも資格を取り消されたり、亡くなってしまった場合、そのアカウントが 1 人のユーザーに所有され、そのパッケージが [OSI によって承認されたライセンス](https://opensource.org/licenses/alphabetical)によって公開されるように、コミュニティと連携しパッケージに適切なオーナーが追加されるようにします。 所有権を要求する場合、次の文書を送信する必要があります。

1.  政府発行の写真付き身分証明書の複写。
2.  以前のアカウント保有者の状態を示す以下の文書のいずれか。 
    - 前のアカウント保有者が死亡した場合、政府発行の公的な死亡証明書。
    - 資格を剥奪されたアカウント保有者の管理を担当する医療専門家によって署名された証明書などの認定文書。
3.  所有権があることを示す次のいずれかの文書。 
    - アカウント保有者の生存配偶者であることを示す結婚証明書。
    - 署名された委任状。
    - ユーザーを遺言執行者または信託受益者とする遺言または信託証書。
    - ユーザーがその親である場合、アカウント保有者の出生証明書。
    - ユーザーがアカウント保有者の法定後見人の場合、後見人立証書類。
    
このポリシーを行使する必要がある場合、身分証明書とパッケージのバージョンを [support@nuget.org](mailto:support@nuget.org) に電子メールで送信してください。
    
## <a name="transparency"></a>[透明度]

オープン ソースのプロジェクトのガバナンスの成功には、コミュニティ内で信頼を構築することが不可欠です。 そのために、意志決定を行う場合、透明性を確保しながら、オープンに行う必要があります。 プロジェクトの方向に関する議論は、公開で行う必要があります。 コミュニティは、ヴェノベレント ディクテーターの意思決定に不意を突かれないようにする必要があります。 また、コミュニティ メンバーが意思決定とその内容の全過程を理解できるよう、プロジェクトの意思決定に関する議論を保存記録する必要があります。