https://qiita.com/___fff_/items/17655df4e80ebadd8fc3

https://qiita.com/tkj/items/c6dad4efc0dff4fecd93

https://www.yururiwork.net/archives/1563

mac環境構築　fastlaneのインストール 
----

# マネージドRuby環境+Bundler

## 初期構築

下記コマンドhomebrewをダウンロード
```sh
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

バージョン確認
```sh
brew -v
```

homebrewでrbenvをインストール
```sh
brew install rbenv ruby-build
```

バージョン確認
```sh
rbenv versions
```

macOSを使用する場合、システムRubyは推奨されません。システム環境を変更せずにRubyをインストールする方法
```sh
rbenv install --l 　　 # => インストール可能なバージョン一覧の表示
rbenv install 3.1.0 # => rubyのインストール 今回は最新が3.1.0
rbenv global 3.1.0  # => defaultで使うrubyのバージョン
rbenv versions # => 3.1.0に＊がつく
```

bash_profileを開いて追記
```sh
vim ~/.bash_profile
```
```sh
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"
```

bash_profile反映
```sh
source ~/.bash_profile
```

fastlaneインストール
```sh
gem install fastlane # => インストール完了
```

## Bundler
Gemfileが生成
```sh
cd プロジェクトファイル
bundle init　# => これでGemfileファイルが生成されます。
```
Gemfileにfastlaneの記述を追加
```sh
vim Gemfile
```
```sh
gem 'fastlane' # => を追加一番下に追記
```

## bundleインストール
bundle installしたときの'vendor/undle'pathのおまじない
[^※1]
[^※1]: 今回、.bundle/configはgitの履歴に含んでいるのでcloneした場合はいらないと思います。
```sh
cd プロジェクトファイル
bundle config set --local path 'vendor/bundle'  
```
bundleインストール
```sh
rbenv exec bundle install
```

確認
```sh
rbenv exec bundle exec fastlane --help
```

# fastlane 初期化
fastlane/Fastfail　下記ファイルが作成される
```sh
rbenv exec bundle exec fastlane init # => 初期の時だけ
```

アプリのバージョン上げる為に、xcode11以降はプラグインを入れる必要があるようです
[^※2]
[^※2]: gitの履歴に含んでいるはずなのでこのアプリを動かく分には実行は必要ないと思います
```sh
rbenv exec bundle exec fastlane add_plugin versioning
```

# fastlane 実行
fastlaneフォルダと同じディレクトリで実行します
```sh
rbenv exec bundle exec fastlane lane名
rbenv exec bundle exec fastlane build version:minor # => 引数を指定する場合
```

# fastlaneを使いまわす方法
fastlane/Fastfailの中身を新しいプロジェクトのFastfailに必要な箇所をコピペする。下記ついては任意の物に書き換え必要です。
- scheme
- xcodeproj
- output_directory
- output_name
- provisioningProfiles

# build_GitHubのlaneについては
githubのActions secretsに定数を作ってそれぞれの値を用意しておくことが前提です。
・.github\workflows\main.yml　例：${{ secrets.PROVISIONING_PROFILE }}

PROVISIONING_PROFILE
```sh
base64 sampleAppProvisioning-11.mobileprovision | tr -d "\n" | pbcopy
```

CERTIFICATES_P12
```sh
base64 証明書.p12 | tr -d "\n" | pbcopy
```

