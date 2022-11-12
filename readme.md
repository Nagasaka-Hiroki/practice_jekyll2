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
gem "minima", github: "jekyll/minima"
```
\_config.ymlを編集
```
plugins:
  - jekyll-remote-theme

remote-theme: jekyll/minima
```
これで再度確認する。(ローカルで確認しようとしたら`bundle install`せよと警告が出たので実行する。)  
ローカルで実行すると少し見え方が変わった。（フッターとかボディ、フォントが変わった気がする）  
→変化はなし。

確認したところjekyllのバージョンがふるいみたい。
```
$ bundle exec jekyll -v
3.9.2
```
最新は`4.3.1`なのでアップデートする。
```
$ gem update jekyll
```
これで最新になったとりあえず作り直す。

```
$ jekyll -v
jekyll 4.3.1
```
一応、上記の修正も加えておく。  
変化はなし。

以下を読んでいて、プラグインを書いたがGemfileが変わっていないことに気づいたので追加。
> - [https://talk.jekyllrb.com/t/unclear-how-to-access-the-gemfile-on-github-pages/7425](https://talk.jekyllrb.com/t/unclear-how-to-access-the-gemfile-on-github-pages/7425)  

```
gem 'jekyll-remote-theme', '~> 0.4.3'
```
