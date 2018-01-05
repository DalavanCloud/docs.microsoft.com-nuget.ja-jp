---
title: "nuget.org プロトコル |Microsoft ドキュメント"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "NuGet のクライアントと対話する継続的に進化 nuget.org プロトコル。"
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a>nuget.org プロトコル

Nuget.org をやり取りするには、クライアントは特定のプロトコルに従う必要があります。 これらのプロトコルが進化を保持するため、クライアントは、特定 nuget.org Api を呼び出すときに使用するプロトコルのバージョンを識別する必要があります。 これにより、古いクライアントの重要ではない方法で変更を nuget.org できます。

> [!Note]
> このページに記載されている Api は、nuget.org に固有とその他の NuGet サーバー実装をこれらの Api を導入することを見込んではありません。 

NuGet のエコシステムで広範に実装されている NuGet API については、次を参照してください。、 [API の概要](overview.md)です。

このトピックでは、さまざまなプロトコルと存在するきたときを示します。

## <a name="nuget-protocol-version-410"></a>NuGet プロトコル バージョン 4.1.0

4.1.0 プロトコル nuget.org アカウントに対してパッケージを検証する、nuget.org 以外のサービスと対話することを確認スコープ キーの使用法を指定します。 なお、`4.1.0`バージョン番号は不透明な文字列がこのプロトコルはサポートされている公式 NuGet クライアントの最初のバージョンと一致するように動作します。

検証はにより、ユーザーが作成した API キーは nuget.org でのみ使用されますされ、その他の検証またはサード パーティのサービスからの検証が 1 回限り使用することを確認スコープ キーによって処理されます。 これらのことを確認スコープ キーを使用して、パッケージが nuget.org の特定のユーザー (アカウント) に所属するを検証することです。

### <a name="client-requirement"></a>クライアントの要件

クライアントは、API の呼び出しを行うときは、次のヘッダーを渡す必要**プッシュ**nuget.org をパッケージ。

```
X-NuGet-Protocol-Version: 4.1.0
```

なお、既存の`X-NuGet-Client-Version`ヘッダー同じ目的が使用されなくなりましたがあり、使用できなくする必要があります。

**プッシュ**プロトコル自体がのドキュメントに記載されている、 [ `PackagePublish`リソース](package-publish-resource.md)です。

クライアントは、外部サービスおよびパッケージは、特定のユーザー (アカウント) に属しているかどうかを検証する必要がありますと対話するを次のプロトコルを使用し、スコープを確認してくださいキーや nuget.org から API キーではないを使用します。

### <a name="api-to-request-a-verify-scope-key"></a>スコープを確認してくださいキーを要求する API

この API は、' | 4 ' によって所有されているパッケージを検証する nuget.org 作成者のスコープを確認してくださいキーの取得に使用されます。

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 可      | 確認してくださいスコープ キーを要求する対象のパッケージ identidier
VERSION        | URL    | string | Ｘ       | パッケージのバージョン
X-NuGet-ApiKey | Header | string | 可      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>応答

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API を確認してくださいスコープ キーを確認するには

この API を使用すると、nuget.org の作成者によって所有されているパッケージのスコープを確認してくださいキーを検証します。

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | 可      | 確認してくださいスコープ キーを要求する対象のパッケージ識別子
VERSION        | URL    | string | Ｘ       | パッケージのバージョン
X-NuGet-ApiKey | Header | string | 可      | たとえば、`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> この確認スコープ API キーの有効期限は 1 日の時刻または初めて使用するとき、先に生じた方です。

#### <a name="response"></a>応答

状態コード | 説明
----------- | -------
200         | API キーは無効です。
403         | API キーは無効であるか、パッケージに対してをプッシュする権限がありません。
404         | によって参照されるパッケージ`ID`と`VERSION`(省略可能) は存在しません