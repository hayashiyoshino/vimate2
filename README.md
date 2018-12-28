# 開発の進め方と考え方

[twadaさんのツイートから引用](https://twitter.com/t_wada/status/904916106153828352?ref_src=twsrc%5Etfw%7Ctwcamp%5Etweetembed%7Ctwterm%5E904916106153828352&ref_url=https%3A%2F%2Fbracket.qiita.com%2FTkashiro%2Fitems%2F8b966c99099d686fe827)

- テストコードのデスクリプションやコメント、コミットメッセージを書く際に留意したい項目

```md
テストコードには What(何をテストしたいのか) を
コミットログには Why(何故その修正をしたのか) を
コードコメントには Why not(何故その修正以外をやらなかったのか) を記載する
```

# 技術要素

### サーバーサイド

- Ruby 2.5.1
- Ruby on Rails 5.2.2

### フロントエンド
- node
- React
- Jest

### データベース
- Postgresql

### その他
- CircleCI 2.0
- Docker
- Cloudinary(画像ストレージ)

# ローカル環境構築の手引き
※ Docker化する場合は以下の手順を変更する(最初はローカルでやる予定)

- Rubyのインストール(2.5.1)

```ruby
$ rbenv install --list
Available versions:
(インストール可能なリストが出てくる)
$ rbenv install  2.5.1
$ rbenv global 2.5.1
$ rbenv rehash
$ rbenv version
2.5.1
$ ruby --version
ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-darwin17]
$ gem --version
2.7.6
```

- postgresqlのインストールと自動起動の設定

```ruby
$ brew install postgresql
$ brew services start postgresql
# postgresqlの起動を確認する
$ brew services list
「postgresql started」が表示されればOK
```

- redisのインストールと自動起動の設定

```ruby
$ brew install redis
$ brew services start redis
$ brew services list
「redis started」が表示されればOK
```

- リポジトリをクローンしてbundle installする

```ruby
$ git clone git@github.com:Tama-rb/vimate.git
$ cd vimate
$ bundle install --path vendor/bundle
```

- データベースを作成する

```ruby
$ bundle exec rails db:create
$ bundle exec rails db:migrate
```

- RuboCopコマンド

```ruby
$ bundle exec rubocop
```

- RSpecコマンド

```ruby
$ bundle exec rspec
```

# リポジトリの運用基本方針

#### レビューの流れ
1. プルリク作成
2. CI(テスト)が通っていることを確認し、レビュー依頼ラベルをつける
3. プルリク作成者以外のメンバーがレビュー中ラベルに変更
4. レビュー完了したら、レビュー完了ラベルに変更し、approveする
5. approveされたことを確認し、誰かがマージする

#### マージするタイミング
- 自分以外のメンバーにapproveをもらったタイミング
- 基本CIが通っている場合以外はマージしてはいけない
