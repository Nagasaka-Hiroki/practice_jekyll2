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

上手く行ったので設定についてメモする。

## 設定について
設定についておおよそ以下の内容で問題なく動作できる。
```
$ jekyll new --skip-bundle .
$ echo "gem 'webrick', '~> 1.7'" >> Gemfile
$ vim Gemfile
# github-pagesの行をアンコメントアウト、jekyllの行をコメントアウト。
$ bundle install
$ vim _config.yml
# baseurlとurlを設定。今回の場合だと以下の通り
baseurl: "/practice_jekyll2" # the subpath of your site, e.g. /blog
url: "https://nagasaka-hiroki.github.io" # the base hostname & protocol for your site, e.g. http://example.com
```

> - [https://www.youtube.com/watch?v=EmSrQCDsMv4&t=0s](https://www.youtube.com/watch?v=EmSrQCDsMv4&t=0s)  
一応参考。jekyll talkで調べていると出てきた。
> - [https://talk.jekyllrb.com/t/cannot-deploy-site-via-github/6883/2](https://talk.jekyllrb.com/t/cannot-deploy-site-via-github/6883/2)
リンクを発見したjekyll talkの質問。

前回の失敗の原因はチュートリアルのナビゲーションでデプロイしていたことが原因だと考えている。  
→疑問は各ファイルでパーマリンクを書いた場合、ナビゲーションでどのようにそのリンクを参照するか？  
直に全部打ち込んでも解決できるかもしれないが方法はないだろうか？  
(推測：_config.ymlにlinkを記述。各ファイルではsite.link（書き方は現状曖昧） とか？そういった形で利用 & ymlのアンカー機能でyml間で参照するとかだろうか？)
> - [http://jekyllrb-ja.github.io/docs/variables/](http://jekyllrb-ja.github.io/docs/variables/)  
これは`_config.yml`の変数の設定の使い方（変数）について言及している。