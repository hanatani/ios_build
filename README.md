https://qiita.com/___fff_/items/17655df4e80ebadd8fc3

https://qiita.com/tkj/items/c6dad4efc0dff4fecd93

https://www.yururiwork.net/archives/1563

#fastlaneのインストール

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

brew -v


brew install rbenv ruby-build


rbenv versions


rbenv install -l


rbenv install 3.1.0   # 今回は最新が3.1.0


rbenv global 3.1.0

rbenv versions # 3.1.0に＊がつく

cd ~

vim ~/.bash_profile

[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"

＃bash反映
source ~/.bash_profile

gem install fastlane

#インストール完了


#これでGemfileが生成されます。

gem install bundler #これいるかも忘れました。
cd プロジェクトファイル
bundle init

#Gemfileを修正します
vim Gemfile
# この行を追加
gem 'fastlane'

#cloneしたら、プロジェクト直下でここから
bundle config set --local path 'vendor/bundle'  

rbenv exec bundle install
＃確認なのでなくてもいい
＃rbenv exec bundle exec fastlane --help

#初期の時だけ
＃rbenv exec bundle exec fastlane init

#これでfastlane実行
rbenv exec bundle exec fastlane lane名
 
#これでプラグイン
rbenv exec bundle exec fastlane add_plugin versioning

