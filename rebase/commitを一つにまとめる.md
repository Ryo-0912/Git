以下のgit graphから見てわかるように、現在fix_requests_of_webhookブランチで作業中。

```
XXX-web % git log --graph                     
* commit 61425702bccca8654308e92a2231e0a389cca74d (HEAD -> fix_requests_of_webhook)
| Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| Date:   Thu Sep 28 16:50:45 2023 +0900
| 
|     fix_fix
| 
* commit cb938a66c3af15226414f067dece9a7648d610af
| Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| Date:   Thu Sep 28 15:57:30 2023 +0900
| 
|     fix requests of webhook
|   
*   commit 5f3bc156a6c15c58084a05d329b6039719b90b1b (⭐️)
|\  Merge: e059e760 b519765f
| | Author: BBBBB <BBB.BBBB@BBBB.co.jp>
| | Date:   Wed Sep 27 16:00:11 2023 +0900
| | 
| |     Merge pull request #98 from skrum-inc/PIC-131-fix-fb-sheet-no-9
| |     
| |     Change the destination of each button
| | 
| * commit b519765fb30333a4728d1b3700cae75d90495264 (origin/PIC-131-fix-fb-sheet-no-9, PIC-131-fix-fb-sheet-no-9)
| | Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| | Date:   Wed Sep 27 15:42:36 2023 +0900
| | 
| |     fix
| | 
| * commit bb2cefac52e0bcef5784519ac195bbeb691c9c68
| | Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| | Date:   Wed Sep 27 15:40:29 2023 +0900
```

このブランチでcommitしたfix_fixとfix requests of webhookというコミットを一つにすることを考える。

ただし、fix_requests_of_webhookのチェックアウト元である**5f3bc156a6c15c58084a05d329b6039719b90b1b**コミットは変えてはいけない。

このような時は、以下のコマンドを実行。

```
XXX-web % git rebase -i 5f3bc156a6c15c58084a05d329b6039719b90b1b(⭐️)
[detached HEAD ad266f65] fix requests of webhook
 Date: Thu Sep 28 15:57:30 2023 +0900
 12 files changed, 27 insertions(+), 24 deletions(-)
Successfully rebased and updated refs/heads/fix_requests_of_webhook.
```

この後、出てくるエディターでfix_fixの箇所をpickup→s(squash)に変更し、保存。

そして、commitメッセージを***fix requests of webhook rebased***に変更。

すると、次のようになる。

```
XXX-web % git log --graph
* commit ad266f655613aa11e8e9b61a4659b40895c48c0d (HEAD -> fix_requests_of_webhook)
| Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| Date:   Thu Sep 28 15:57:30 2023 +0900
| 
|     fix requests of webhook rebased
|   
*   commit **5f3bc156a6c15c58084a05d329b6039719b90b1b**
|\  Merge: e059e760 b519765f
| | Author: BBBBB <BBB.BBBB@BBBB.co.jp>
| | Date:   Wed Sep 27 16:00:11 2023 +0900
| | 
| |     Merge pull request #98 from skrum-inc/PIC-131-fix-fb-sheet-no-9
| |     
| |     Change the destination of each button
| | 
| * commit b519765fb30333a4728d1b3700cae75d90495264 (origin/PIC-131-fix-fb-sheet-no-9, PIC-131-fix-fb-sheet-no-9)
| | Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| | Date:   Wed Sep 27 15:42:36 2023 +0900
| | 
| |     fix
| | 
| * commit bb2cefac52e0bcef5784519ac195bbeb691c9c68
| | Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| | Date:   Wed Sep 27 15:40:29 2023 +0900
| | 
| |     Change the destination of each button
| | 
* | commit e059e760df049f8ab52dd44d1792b2b6e8c1293c
| | Author: CCCCC <CCC.CCCC@CCCC.co.jp>
| | Date:   Wed Sep 27 15:35:17 2023 +0900
:...skipping...
* commit ad266f655613aa11e8e9b61a4659b40895c48c0d (HEAD -> fix_requests_of_webhook)
| Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| Date:   Thu Sep 28 15:57:30 2023 +0900
| 
|     fix requests of webhook
|   
*   commit 5f3bc156a6c15c58084a05d329b6039719b90b1b
|\  Merge: e059e760 b519765f
| | Author: BBBBB <BBB.BBBB@BBBB.co.jp>
| | Date:   Wed Sep 27 16:00:11 2023 +0900
| | 
| |     Merge pull request #98 from skrum-inc/PIC-131-fix-fb-sheet-no-9
| |     
| |     Change the destination of each button
| | 
| * commit b519765fb30333a4728d1b3700cae75d90495264 (origin/PIC-131-fix-fb-sheet-no-9, PIC-131-fix-fb-sheet-no-9)
| | Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| | Date:   Wed Sep 27 15:42:36 2023 +0900
| | 
| |     fix
| | 
| * commit bb2cefac52e0bcef5784519ac195bbeb691c9c68
| | Author: AAAAA <AAA.AAAA@AAAA.co.jp>
| | Date:   Wed Sep 27 15:40:29 2023 +0900
```
