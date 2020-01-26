# chromebook C101PAに日本語入力の設定をする

### 参考URL
 - [Chromebook C101PAのcrostiniでlinuxアプリを使ってみた](https://ponpon.asa.link/2018/10/20/c101pa%e3%81%a7crostini%e3%81%a7linux%e3%82%a2%e3%83%97%e3%83%aa%e3%82%92%e4%bd%bf%e3%81%a3%e3%81%a6%e3%81%bf%e3%81%9f/)
 - [Debianでarm64でmozc build](https://matoken.org/blog/2017/06/05/on-debian-mozc-build-with-arm64/)
 - [パッケージのインストール](https://yadi.sk/d/1NZ9khV53JoQSE)
 - [ChromeOSのLinux(Crostini)で日本語入力(自動起動対応)](https://www.axon.jp/entry/2018/10/18/201812)


## 1. 事前準備

- **Linuxのインストール**
『設定』→『Chrome OSについて』→『詳細』→『チャンネル』をdevに変更する。
『設定』→『linux（ベータ版）』→『オンにする』をクリック
これでインストール完了。簡単だなぁと。

- **フォントのインストール**

日本語入力を設定するため、日本語フォントを入れたい。
「源ノ角ゴシック Code JP」を今回は使用する

    $ curl -OL https://github.com/adobe-fonts/source-han-code-jp/archive/2.011R.tar.gz
    $ tar zxf 2.011R.tar.gz
    $ sudo cp ./source-han-code-jp-2.011R/OTF/* /usr/local/share/fonts
    $ sudo fc-cache -fv

 
 - タイムゾーンの設定（必須ではない）
 
 なんとなくログ等を監視する場合に時間がわかりやすいように。

    $ sudo timedatectl set-timezone Asia/Tokyo


- ロケールの設定

		$ sudo  apt install task-japanese
		$ sudo  update-locale  LANG=ja_JP.UTF-8


## 2. 日本語入力の設定

日本語入力の設定においてfcitx-moxcを使用する。
しかし、webに転がっているデータはamd64のものばっか。（私はここで困っていた）
今回使用しているデバイスは
「chromebook C101PA」(ASUS)でCPUがarm系であるとか。

下記の説明は見ておくといいかもしれません。
[組み込み開発におけるARMとは？](https://www.eipc.jp/embedded/arm/)

困ったものだなと思っていたら、
『matoken's memeさん』が[Debianでarm64でmozc build](https://matoken.org/blog/2017/06/05/on-debian-mozc-build-with-arm64/)にて使用されているarm用のパッケージがあるとか。
ありがとうございます。

[パッケージのインストール](https://yadi.sk/d/1NZ9khV53JoQSE)から全ファイルをインストールする。

次にダウンロードファイルにダウンロードされた上のフォルダをすべてlinuxと共有する。
基本的にやり方は「右クリック」→「linuxと共有」とすれば良い。

※一つのファイルを右クリックし、「linuxにインストール」というものがあるのですが、やってもうまく行きませんでした。権限の問題だとは思いますが。

どちらにしろコマンドでインストールしたほうが簡単そう。ということでインストール。

共有されたフォルダは
`/mnt/chromeos/MyFiles/`直下にあるので各.debファイルをインストールする。

	$ sudo apt-get install /mnt/chromeos/MyFiles/*


インストール後、fcixt-mozcをインストールする。

	$ sudo apt-get install fcitx-mozc

このあと設定を開いて設定をするのですが、基本的には下記のやり方で問題ありません。
 - [ChromeOSのLinux(Crostini)で日本語入力(自動起動対応)](https://www.axon.jp/entry/2018/10/18/201812)

ただ問題として、
		
	$ fcitx-configtool


後にInput Methodを確認してみると何も書かれていない場合があった。
同じようになった場合は

	$ fcitx-autostart

を実行後、見てみると問題なく動きます。
上記のURLを参考に自動起動するように設定したほうが良さそうですね。


### 確認したい場合
僕はvscodeをインストールして確認をしてみました。

[https://www.reddit.com/r/Crostini/wiki/howto/install-vscode](https://www.reddit.com/r/Crostini/wiki/howto/install-vscode)
から**Pre-built deb package**の場所から.debファイルをダウンロード。

あとはmozcの.deb同様インストールを行えば『Code-OSS』があるはずなので、起動後、vscode上で適当なファイルを作成し、日本語を入力してみる。


## 最後に
実際にはそこまで難しいものではなかったが、linux初心者には難しいと感じると思いました。実は僕も完全初心者の段階でチャレンジしたら躓いた。
[2019年発売の全てのChromebookがLinux対応に](https://japan.zdnet.com/article/35136835/)
というようにある。今後chromebookが浸透していって欲しいと思う。

次はdockerを入れて動かしてみようかなと思う。
