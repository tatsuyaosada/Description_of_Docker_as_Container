#### Dockerを例に用いたコンテナによる仮想サーバーの概要と実践

***

#### そもそもコンテナって何？
一般的な仮想サーバーはベースとなっているホストOS上に、更にサブシステムとしてゲストOSを乗せ、その上でサーバーを走らせると言う手法を取る。当然ながら、そこには両者のOSのプロセスの干渉が発生し、不具合の元となる事も少なくない。分かり易い例としては、XAMPPを使っている人であれば、ホストOSとのポートの競合等でApache等が動作しない、なんてケースは日常茶飯事であろう。

一方でコンテナは、ベースOS上にサブシステムとしてゲストOSを載せる必要がない。ベースOSのプロセスに干渉する事が無い。

> アプリ(Docker等コンテナを生成するもの)とWindowsのファイルシステムを完全に隔離する

と言い換えても良いかもしれない。

全体像としては

<img width="700" height="400" alt="docker01" src="https://github.com/user-attachments/assets/0644e6fc-03b5-4076-8b1e-190dca0348e6" />

こんな感じ。


#### で、何が優れてるの？
1. ゲストOSを走らせないので、ベースとなるホストOSに影響を及ぼす事が無い
>Windowsのプロセスを利用しないのでホストOSを破壊する事がない
2. 可搬性が高く、コンテナのイメージ(イメージについては後述)を他のコンテナに移植する事が容易。
   自分の開発環境を他人や本番環境、あるいはテスト環境へ丸ごとエクスポート出来る。


#### と言うわけでコンテナを使うメリットとデメリット

一番は、ホストOSのプロセスに干渉しない、と言う事。XAMPPを使っている人は


#### で、コンテナってのは何となく理解出来たけど、じゃあDockerって何？
コンテナ生成のデファクトスタンダード。このアプリケーションが生まれたからコンテナと言う概念が出来たとも言われている(※諸説有)


#### Dockerによるコンテナの作成
コンテナは言ってしまえばただの箱に過ぎません。その中にイメージと言われるテンプレートを導入する事で初めてミドルウェアとして稼働します。例えばウェブサーバーを立ち上げたければApacheやNode.js、データベースサーバーならMariaDB等、と言った感じ。Dockerではこれを[Dockerfile]()と呼称します。


<figure>
<img width="400" height="154" alt="docker-image" src="https://github.com/user-attachments/assets/dcda1f1d-a18f-484e-9ef7-10bf6c8866e0" />
</figure>


簡単なものであれば自分で用意する事も出来ますが、よくある構成であれば[DockerHub](https://hub.docker.com/)と言うサイトでイメージが配布されています。

上述した様にコンテナイメージは可搬性が極めて高いため、ほぼそのまま流用する事が出来ます。これが非常に便利で、万が一何かしらの理由でコンテナが壊れても新しいコンテナを作り、同じイメージを導入すれば同じものが即座に復元出来ます。また、別の開発環境

#### コンテナのライフサイクル

1. Create(作成)
   - コンテナにイメージを取り込んだ状態。環境構築としては完成と言えなくもないが、残念ながらこの状態では動作しない。
   - 実行コマンド : <code>docker create</code>
2. Running(実行)
   - イメージによって作成されたコンテナを起動する。これにより、対応するイメージのアプリケーションとして動作する様になる。
   - 実行コマンド : <code>docker start</code> もしくは <code>docker run</code>
3. Paused(一時停止)
   - コンテナの稼働を<strong>一時的</strong>に停止する。プロセスは停止しますが、メモリ上には状態が維持される。要するに残る。
   - 実行コマンド ： <code>docker pause</code> 
4. Exited/Stopped(停止)
   - コンテナの稼働を完全にシャットダウンした状態。もちろん再度稼働させる事も出来る。3の一時停止との違いは、PCのメモリを解放するか否か。
   - 実行コマンド ： <code>docker stop</code>
5.Removed(削除)
   - コンテナをイメージや状態ごと文字通り削除する。例えばMariaDB等、データベース系のミドルウェアをこのコンテナで動かしていた場合、当然それも削除される。
   - 実行コマンド : <code>docker rm</code>

<hr>
基本的なイメージはこんな感じ

<img width="564" height="400" alt="container-lifecycle02" src="https://github.com/user-attachments/assets/e9c8efd2-e6ba-4241-9b4d-06dade4dcc69" />

<hr>
もう少し詳細なものだと...

<img width="1133" height="516" alt="20200702233743" src="https://github.com/user-attachments/assets/cda0eddd-d56b-4c00-bc3e-7eb3ed89de28" />


#### 開発環境の構築
1. [※WSL2](https://learn.microsoft.com/ja-jp/windows/wsl/install)をインストールする
2. windowsの機能でLinux用サブシステムと仮想マシンプラットフォームを有効にする
3. [Docker_Desktop](https://www.docker.com/ja-jp/products/docker-desktop/)をインストールする

- ※WSLとは？
> [Windows Subsystem for Linux](https://learn.microsoft.com/ja-jp/windows/wsl/install)の略。windows上でLinuxを動かす仮想システム。


#### 参考文献
