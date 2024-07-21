会社等で使っていたGithubアカウントが原因でpush等ができない(Permissionエラー)ことがある。

```
% git push -u origin main     
remote: Permission to Ryo-0912/go-basics.git denied to ryo-ando96.
fatal: unable to access 'https://github.com/Ryo-0912/go-basics.git/': The requested URL returned error: 403
```

解決策

VSCODEでサインインしているユーザからサインアウトする必要がある。

[認証エラー]（https://aisumegane.com/github_vscode_you-do-not-have-permission-to-push-to-on-github_gitgraph_vscode/）
