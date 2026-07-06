# studio909.jp 更新メモ

## お知らせ（INFORMATION）の追加方法

`_data/news.yml` の上の方に、以下の4行セットを追記してコミットするだけ。

```yaml
- date: 2026.07.15
  tag: MEDIA
  title: ○○様にて△△が掲載されました
  url: https://example.com/article
```

- `tag` は `MEDIA` / `SNS` / `EVENT` のいずれか
- **並び順は日付から自動ソート**されるので、ファイル内のどこに書いてもOK
- `index.html` は触らなくてよい

コミット後、GitHub Pagesが自動でビルドして数十秒〜数分で反映される。

## 仕組み

- GitHub Pages標準のJekyllを使用（追加設定・Actions不要）
- `index.html` 冒頭の `---` 2行（front matter）がJekyll処理のスイッチ。**消さないこと**
- ニュース一覧は `index.html` 内の `{% for item in sorted_news %}` ループが
  `_data/news.yml` を読んで生成している

## 注意

- YAMLの `title` に `:` （半角コロン）を含む場合は全体を `"..."` で囲む
- URLはXの投稿からコピーする場合、ブラウザのアドレスバーか「リンクをコピー」
  から直接コピーする（Excelなどを経由するとIDが壊れることがある）
- ローカルで確認したい場合: `bundle exec jekyll serve`（なくてもGitHub側でビルドされる）
