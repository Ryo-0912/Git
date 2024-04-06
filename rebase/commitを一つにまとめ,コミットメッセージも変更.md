以下のgit graphから見てわかるように、現在firstブランチで作業中。

```
% git log --graph
* commit f98a5611195160b1ce279db95c0c645ed9696091 (HEAD -> first)
| Author: Ryo Ando <ryo.ando@skrum.co.jp>
| Date:   Sat Apr 6 17:16:47 2024 +0900
| 
|     third.html追加
| 
* commit 0afe77c00fc5e2c409435c8b22d909104467937e
| Author: Ryo Ando <ryo.ando@skrum.co.jp>
| Date:   Sat Apr 6 17:16:23 2024 +0900
| 
|     second.html追加
| 
* commit d96c40e631768b69883140f9ff6a9e12f7374cde
| Author: Ryo Ando <ryo.ando@skrum.co.jp>
| Date:   Sat Apr 6 17:15:47 2024 +0900
| 
|     first.html追加
|   
*   commit 5b15e79a045963a3865f5bbb25ebf6a68611d62a (origin/develop, origin/HEAD, develop)
|\  Merge: e62112f 9d1d18f
| | Author: test-user <test.user@skrum.co.jp>
| | Date:   Thu Apr 4 17:42:57 2024 +0900
```

このブランチ内でcommitした3つのcommitを一つのcommitにすることを考える。

ブランチを切った箇所から3つのcommitをしているので、以下のコマンドを実行。

```
% git rebase -i HEAD~3
```

すると、次のようなエディターが開く。

```
pick d96c40e first.html追加
pick 0afe77c second.html追加
pick f98a561 third.html追加

# Rebase 5b15e79..f98a561 onto 5b15e79 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
```

一つにまとめたいので、次のように編集し、保存。

```
pick d96c40e first.html追加
squash 0afe77c second.html追加
squash f98a561 third.html追加

# Rebase 5b15e79..f98a561 onto 5b15e79 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
```

すると、すぐに、次のようなエディターが開くが、特に何もせず、終了。

```
# This is a combination of 3 commits.
# This is the 1st commit message:

first.html追加

# This is the commit message #2:

second.html追加

# This is the commit message #3:

third.html追加

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sat Apr 6 17:15:47 2024 +0900
#
# interactive rebase in progress; onto 5b15e79
# Last commands done (3 commands done):
#    squash 0afe77c second.html追加
#    squash f98a561 third.html追加
# No commands remaining.
# You are currently rebasing branch 'first' on '5b15e79'.
#
# Changes to be committed:
#       new file:   first.html
#       new file:   second.html
#       new file:   third.html
#
# Untracked files:
#       .DS_Store
#       .history/
#       app/Http/Requests/Api/MatchingGoodRequest.php
#       app/Http/UseCases/SendGoodMessageUseCase.php
#       app/Http/UseCases/SendGoodUseCase.php
#       app/Repositories/InspectMessageGood/
#       storage/bridge-d540d-c8e276592470.json
#       user.html
#
~                                                                                             
"~/sample/.git/COMMIT_EDITMSG" 40L, 1002B
```

現状を確認する。

```
% git log --graph
* commit 86743506e9421aeaf49b430f2fda66d4ba278a48 (HEAD -> first)
| Author: Ryo Ando <ryo.ando@skrum.co.jp>
| Date:   Sat Apr 6 17:15:47 2024 +0900
| 
|     first.html追加
|     
|     second.html追加
|     
|     third.html追加
|   
*   commit 5b15e79a045963a3865f5bbb25ebf6a68611d62a (origin/develop, origin/HEAD, develop)
|\  Merge: e62112f 9d1d18f
| | Author: test-user <test.user@skrum.co.jp>
| | Date:   Thu Apr 4 17:42:57 2024 +0900
| | 
| |     Merge pull request #156 from skrum-inc/fix_sub_photo
| | 
| * commit 9d1d18fd7a78efa32473e11220f032c51610137c (origin/fix_sub_photo)
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:23:38 2024 +0900
| | 
| |     fix
| | 
| * commit 630d6408d9650ff6d22eb698e38d5929adf9b3d6
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:11:12 2024 +0900
| | 
| |     fix
| | 
| * commit e03eecf18a93666a0797abf05d4e0a2e928ad42d
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:02:51 2024 +0900
| | 
| |     fix
| | 
| * commit f5eba22610d376bdcc450f6e5c0297632c35604b
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 17:57:13 2024 +0900
| | 
| |     fix
| | 
```

コミットメッセージが適切でないので、変更する。

```
% git rebase -i HEAD~1
```

下のような。エディターが開くので、pick->editに変更し、終了。
```
pick 8674350 first.html追加

# Rebase 5b15e79..8674350 onto 5b15e79 (1 command)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
#         create a merge commit using the original merge commit's
#         message (or the oneline, if no original merge commit was
#         specified); use -c <commit> to reword the commit message
# u, update-ref <ref> = track a placeholder for the <ref> to be updated
#                       to this position in the new commits. The <ref> is
#                       updated at the end of the rebase
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
"~/sample/.git/rebase-merge/git-rebase-todo" 32L, 1510B
```

エディターを閉じると、次のような出力がされるので、```git commit --amend```を実行。

```
% git rebase -i HEAD~1 
Stopped at 8674350...  first.html追加
You can amend the commit now, with

  git commit --amend 

Once you are satisfied with your changes, run

  git rebase --continue
```

git commit --amendを実行すると、次のようなエディターが開く。

```
first.html追加

second.html追加

third.html追加

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sat Apr 6 17:15:47 2024 +0900
#
# interactive rebase in progress; onto 5b15e79
# Last command done (1 command done):
#    edit 8674350 first.html追加
# No commands remaining.
# You are currently editing a commit while rebasing branch 'first' on '5b15e79'.
#
# Changes to be committed:
#       new file:   first.html
#       new file:   second.html
#       new file:   third.html
#
# Untracked files:
#       .DS_Store
#       .history/
#       app/Http/Requests/Api/MatchingGoodRequest.php
#       app/Http/UseCases/SendGoodMessageUseCase.php
#       app/Http/UseCases/SendGoodUseCase.php
#       app/Repositories/InspectMessageGood/
#       storage/bridge-d540d-c8e276592470.json
#       user.html
#
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
"~/sample/.git/COMMIT_EDITMSG" 32L, 842B
```

ここで、始めてコミットメッセージを変更する。

```
first.html,second.html.third.htmlを追加

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sat Apr 6 17:15:47 2024 +0900
#
# interactive rebase in progress; onto 5b15e79
# Last command done (1 command done):
#    edit 8674350 first.html追加
# No commands remaining.
# You are currently editing a commit while rebasing branch 'first' on '5b15e79'.
#
# Changes to be committed:
#       new file:   first.html
#       new file:   second.html
#       new file:   third.html
#
# Untracked files:
#       .DS_Store
#       .history/
#       app/Http/Requests/Api/MatchingGoodRequest.php
#       app/Http/UseCases/SendGoodMessageUseCase.php
#       app/Http/UseCases/SendGoodUseCase.php
#       app/Repositories/InspectMessageGood/
#       storage/bridge-d540d-c8e276592470.json
#       user.html
#
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~                                                                                             
~   
```

コミットメッセージが変更されていることを確認。

```
% git log --graph
* commit 39e958da8445025db53e4b746dab58bf467c5e63 (HEAD)
| Author: Ryo Ando <ryo.ando@skrum.co.jp>
| Date:   Sat Apr 6 17:15:47 2024 +0900
| 
|     first.html,second.html.third.htmlを追加
|   
*   commit 5b15e79a045963a3865f5bbb25ebf6a68611d62a (origin/develop, origin/HEAD, develop)
|\  Merge: e62112f 9d1d18f
| | Author: test-user <test.user@skrum.co.jp>
| | Date:   Thu Apr 4 17:42:57 2024 +0900
| | 
| |     Merge pull request #156 from skrum-inc/fix_sub_photo
| | 
| * commit 9d1d18fd7a78efa32473e11220f032c51610137c (origin/fix_sub_photo)
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:23:38 2024 +0900
| | 
| |     fix
| | 
| * commit 630d6408d9650ff6d22eb698e38d5929adf9b3d6
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:11:12 2024 +0900
| | 
| |     fix
| | 
| * commit e03eecf18a93666a0797abf05d4e0a2e928ad42d
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:02:51 2024 +0900
| | 
| |     fix
| | 
| * commit f5eba22610d376bdcc450f6e5c0297632c35604b
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 17:57:13 2024 +0900
| | 
| |     fix
| | 
| * commit f1b64097b626008184db1c9d0c8f9b71ab623446
|/  Author: Ryo Ando <ryo.ando@skrum.co.jp>
|   Date:   Wed Apr 3 16:59:42 2024 +0900
|   
:
```

最後に、```git rebase --continue```を実行。

再度、現状を確認。

```
% git log --graph
* commit 39e958da8445025db53e4b746dab58bf467c5e63 (HEAD -> first)
| Author: Ryo Ando <ryo.ando@skrum.co.jp>
| Date:   Sat Apr 6 17:15:47 2024 +0900
| 
|     first.html,second.html.third.htmlを追加
|   
*   commit 5b15e79a045963a3865f5bbb25ebf6a68611d62a (origin/develop, origin/HEAD, develop)
|\  Merge: e62112f 9d1d18f
| | Author: test-user <test.user@skrum.co.jp>
| | Date:   Thu Apr 4 17:42:57 2024 +0900
| | 
| |     Merge pull request #156 from skrum-inc/fix_sub_photo
| | 
| * commit 9d1d18fd7a78efa32473e11220f032c51610137c (origin/fix_sub_photo)
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:23:38 2024 +0900
| | 
| |     fix
| | 
| * commit 630d6408d9650ff6d22eb698e38d5929adf9b3d6
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:11:12 2024 +0900
| | 
| |     fix
| | 
| * commit e03eecf18a93666a0797abf05d4e0a2e928ad42d
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 18:02:51 2024 +0900
| | 
| |     fix
| | 
| * commit f5eba22610d376bdcc450f6e5c0297632c35604b
| | Author: Ryo Ando <ryo.ando@skrum.co.jp>
| | Date:   Wed Apr 3 17:57:13 2024 +0900
| | 
| |     fix
| | 
| * commit f1b64097b626008184db1c9d0c8f9b71ab623446
|/  Author: Ryo Ando <ryo.ando@skrum.co.jp>
|   Date:   Wed Apr 3 16:59:42 2024 +0900
|   
:
```
