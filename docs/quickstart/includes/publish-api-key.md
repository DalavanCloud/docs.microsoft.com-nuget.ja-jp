1. [ご自分の nuget.org アカウントにサインインする](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)か、まだ持っていなければ、アカウントを作成します。

1. (右上で) ユーザー名を選択し、**[API キー]** を選択します。

1. **[作成]** を選択し、キーの名前を指定して、**[スコープの選択] > [プッシュ]** の順に選択します。 **[API キー]** で、**[glob パターン ]** に「*」と入力してから、 **[作成]** を選択します。 (スコープの詳細については、後述の説明をご覧ください。)

1. キーが作成されたら、**[コピー]** を選択して、CLI で必要となるアクセス キーを取得します。

    ![API キーをクリップボードにコピーする](../media/QS_Create-02-APIKey.png)

1. **重要**: キーは、後でもう一度コピーできないため、安全な場所に保存してください。 [API キー] ページに戻ったら、キーを再生成してコピーする必要があります。 CLI を通じてパッケージをプッシュする必要がなくなった場合は、API キーを削除することもできます。

スコープを使用して、別の目的のために別個の API キーを作成できます。 各キーは有効期限の時間枠を備え、特定のパッケージ (またはの glob パターン) に対してスコープを設定できます。 また、各キーは、新しいパッケージと更新のプッシュ、更新のプッシュのみ、リストからの除外など、特定の操作に対してもスコープを設定します。 スコープを使用して、必要なアクセス許可以外は持たない組織のパッケージ管理を行う別の担当者のために、API キーを作成できます。 詳細については、「[Introducing scoped API keys](https://blog.nuget.org/20170202/introducing-scoped-api-keys.html)」 (スコ―プ設定された API キーを導入する) (blogs.nuget.org) をご覧ください。