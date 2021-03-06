# X-TileでRVizをリサイズする
## X Tileのインストール  
X-TileはPython3で動いているので、Kinetic環境だとPipでインストはややこしい。debパッケージ作成してインストールする。  
*Debian Helper* がインストールされていなければ、先にインストールしておく。
~~~
sudo apt install debhelper
~~~
YOODSからX-Tileをcloneする。
~~~
git clone https://github.com/YOODS/x-tile.git
~~~
Cloneされたディレクトリにて以下実行。エラーがたくさん出てもdebパッケージファイル(**x-tile...deb**)が出来ていれば良し。
~~~
./create_debian_package.sh
~~~
ひとつ上のディレクトリに **x-tile...deb** というDebパッケージが作成されるので、dpkgでインストール
~~~
sudo dpkg -i x-tile_3.3-0_all.deb
~~~
## RVizを強制リサイズ  
セットアップを開いた時、RVizとパネルが重なって見づらい。X-Tileを使ってRVizを強制リサイズして、重ならないようにしよう。
### 設定ファイル

|ファイル名|コンテンツ|意味|
|:----|:----|:----|
|~/.config/x-tile/-apps-x-tile-0-custom|0,0,1550,928|ウィンドウサイズ設定①。パネル表示時のウインドウサイズとする|
|~/.config/x-tile/-apps-x-tile-0-custom_2|0,0,1920,928|ウィンドウサイズ設定②。最大表示時のウインドウサイズとする|
|~/.config/x-tile/-apps-x-tile-0-process_whitelist|rviz|リサイズするプロセス名|

### コマンド  
以下のコマンドにて、RVizがサイズ設定①にリサイズされる
~~~
x-tile 1
~~~
以下は同様にサイズ設定②にリサイズ
~~~
x-tile 2
~~~
### dashboardへの追加  
dashboardのLauncherにpre,postプロパティが追加されました。これでlaunchの前後で実行するコマンドを指定できます。セットアップの起動設定にx-tileを実行することで、Rvizとパネルの重複を回避できます。以下dashboard.yamlの設定例。
~~~
launch_setup:
  label: "セットアップ"
  package: rovi_visual_teach
  file: setup.launch
  pre: "x-tile 1"
  post: "x-tile 2"
~~~
