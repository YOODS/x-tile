# X-TileでRVizをリサイズする
## X Tileのインストール  
### ダウンロード
X-TileはPython3で動いているので、Kinetic環境だとPipでインストするとややこしい。以下からdebパッケージをDLしてパッチする
~~~
https://www.giuspen.com/x-tile/#downl
~~~
dpkgでインストール
~~~
sudo dpkg -i x-tile_3.3-0_all.deb
~~~
### パッチ
このReposのcore.pyをパッチする
~~~
sudo cp modules/core.py /usr/share/x-tile/modules
~~~
## RVizを強制リサイズ  
セットアップを開いた時、RVizとパネルが重なって見づらい。X-Tileを使ってRVizを強制リサイズして、重ならないようにしよう。
### 設定ファイル

|ファイル名|コンテンツ|意味|
|:----|:----|:----|
|~/.config/x-tile/-apps-x-tile-0-custom|0,0,1900,622|ウィンドウサイズ設定①。最大表示時のウインドウサイズとする|
|~/.config/x-tile/-apps-x-tile-0-custom_2|0,0,1300,622|ウィンドウサイズ設定②。パネル表示時のウインドウサイズとする|
|~/.config/x-tile/-apps-x-tile-0-process_whitelist|rviz|リサイズするプロセス名|

### コマンド  
以下のコマンドにて、Rvizウィンドウがサイズ設定①にリサイズされる
~~~
x-tile 1
~~~
以下は同様にサイズ設定②にリサイズ
~~~
x-tile 2
~~~

dashboardのLauncherにコマンド指定できるように改変すれば、Rvizとパネルの重複を回避できる
