pushできない時の可能性
- ローカルで作業中に、別の人がリモートにpushした可能性

⇒ ローカルの元のブランチにリモートブランチの内容をpullしてくる

- ローカルとリモートでコミット履歴が異なる可能性

⇒ ローカルとリモートでコミット履歴を合わせる必要がある

git log --onelineでローカルにコミットされた履歴を確認できる

GitHubのCode ⇒ commits ⇒ ローカルでの作業ブランチからリモートのコミット履歴を確認できる

⇒ リモートのコミット履歴に合わせるために以下を実施。

参照 : https://www-creators.com/archives/1097#git_pull

①次のコマンドで、現在、リモートにある特定のブランチAの状態を追跡しているローカルのブランチに反映させることができる。

```php
git fetch origin (作業ブランチ)
```

ex) リモート`origin`にある`mock`ブランチを、それを追跡しているローカルにある`origin/mock`
に反映する。

```php
git fetch origin mock
From https://github.com/skrum-inc/goukakujou-web
 * branch            mock       -> FETCH_HEAD
 * [new branch]      mock       -> origin/mock
```

②最後に、以下のコマンドを実行。

このコマンドで、

**現在いる作業ブランチの状態**を、リモート追跡のブランチに強制的に合わせることができる。

```php
git reset --hard origin/(作業ブランチ)
```

ex) 

```php
git reset --hard origin/mock          
HEAD is now at b887931 Merge pull request #3 from skrum-inc/Feature/create_base_code_auth
```
