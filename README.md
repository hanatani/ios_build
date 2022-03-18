https://qiita.com/___fff_/items/17655df4e80ebadd8fc3

https://qiita.com/tkj/items/c6dad4efc0dff4fecd93
export http_proxy=http://192.168.120.14:8080
export https_proxy=http://192.168.120.14:8080

https://www.yururiwork.net/archives/1563

$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"


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


source ~/.bash_profile


gem install fastlane



#インストール完了


cd プロジェクトファイル


bundle init
#これでGemfileが生成されます。

#Gemfileを修正します
vim Gemfile

# この行を追加
gem 'fastlane'


bundle config set --local path 'vendor/bundle'  

export http_proxy=http://192.168.120.14:8080



rbenv exec bundle install


rbenv exec bundle exec fastlane --help


rbenv exec bundle exec fastlane init
#最初は2を選択したあとは指示にしたがってEnterを押せば
#fastlane/Appfile と fastlane/Fastfile が作られます。


#Fastfile に下記で.ipaファイルができます
gym(
      scheme: "sample App",
      configuration: "Debug",
      export_method: "development",
      output_directory: "./build/ipa/" + Time.new.strftime("%Y/%m/%d/%H%M"),
      output_name: "MyApp.ipa",
      include_bitcode: false,
      export_options: {
         compileBitcode: false,
         uploadBitcode: false,
      }
    ) 


