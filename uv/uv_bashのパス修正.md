原因は、`uv` が未インストールなのではなく、インストール先が `PATH` に入っていないことです。

確認した実体:

```text
C:\Users\tatti\.local\bin\uv.exe
uv 0.12.5
```

## 一時的に実行する

現在の Git Bash で次を実行してください。

```bash
export PATH="$HOME/.local/bin:$PATH"
uv --version
uv run uv-test00
```

`pyproject.toml` の定義は以下なので、コマンド名は `uv-test00` が正解です。

```toml
[project.scripts]
uv-test00 = "uv_test00:main"
```

## 永続的に修正する

Git Bash で次を実行します。

```bash
"$HOME/.local/bin/uv.exe" tool update-shell
```

その後、VS Codeのターミナルをすべて閉じて、新しいGit Bashを開いてください。これは `uv` 公式のPATH設定用コマンドです。[uv公式ドキュメント](https://docs.astral.sh/uv/concepts/tools/)

確認:

```bash
which uv
uv --version
uv run uv-test00
```

期待される `which uv` の結果:

```text
/c/Users/tatti/.local/bin/uv
```

- 変更内容: なし（診断のみ）
- 変更ファイル: なし
- 検証結果: 一時的にPATHを追加するとGit Bashで `uv 0.12.5` を認識
- 残る点: `uv run` 自体は、仮想環境作成や依存関係取得を伴う可能性があるため未実行です
