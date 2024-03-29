cherry-pickは、rebaseとコミットの分岐元を変えるという意味では似ていると思ったので、rebaseディレクトリ内に記載。

```cherry-pick```は、特定のコミットだけを現在いるコミットに追加することができる。

# 対象 : １つの特定のコミット

現在、masterブランチのコミットFにいるとする。

<img width="374" alt="スクリーンショット 2024-03-29 16 42 56" src="https://github.com/Ryo-0912/Git/assets/82032550/f56bcefc-bf86-4da6-b254-e1b131bbdeb4">

```git cherry-pick E```実行

<img width="323" alt="スクリーンショット 2024-03-29 16 44 51" src="https://github.com/Ryo-0912/Git/assets/82032550/d4ad1f51-c513-4f05-a59e-89cbd0c7e1ba">



# 対象 : 複数の特定のコミット

もし、複数のコミットを一括で追加したい場合は次のようなコマンド実行。

```git cherry-pick D E J```

<img width="538" alt="スクリーンショット 2024-03-29 16 43 18" src="https://github.com/Ryo-0912/Git/assets/82032550/ed5d572e-9ae0-49d5-9c4b-fa482f4c9692">

最終結果。

<img width="532" alt="スクリーンショット 2024-03-29 16 43 33" src="https://github.com/Ryo-0912/Git/assets/82032550/59343227-0a36-4f9c-bbb5-1fb998ffab8c">
