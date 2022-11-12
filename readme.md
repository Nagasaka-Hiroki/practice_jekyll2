# Jekyll学習2
## 概要
GitHub上で上手く表示されない問題とナビゲーションが上手く行かないのを修正できるように努める。

## プロジェクト作成
```
$ jekyll new --skip-bundle .
#Gemfileを編集
#jekyllをコメントアウト
#github-pagesをアンコメントアウト
#webrickを追加
$ bundle install
```
上記で土台は完成。

しかし、いつもどおり見え方が変（GitHub上で）。

以下を参考に修正。
> - [https://github.com/jekyll/minima/issues/419](https://github.com/jekyll/minima/issues/419)
> - [https://github.com/jekyll/minima/issues/411](https://github.com/jekyll/minima/issues/411)

Gemfileを編集
```
gem "minima", "~> 2.0", github: "jekyll/minima"
```
\_config.ymlを編集
```
plugins:
  - jekyll-remote-theme
remote-theme: jekyll/minima
```
これで再度確認する。(ローカルで確認しようとしたら`bundle install`せよと警告が出たので実行する。)  
ローカルで実行すると少し見え方が変わった。（フッターとかボディ、フォントが変わった気がする）

