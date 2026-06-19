#### Dockerを例に用いたコンテナによる仮想サーバーの概要と実践
***

#### そもそもコンテナって何？
一般的な仮想サーバーはベースとなっているホストOS上に、更にサブシステムとしてゲストOSを乗せ、その上でサーバーを走らせると言う手法を取る。一方でコンテナは、ベースOS上にサブシステムとしてゲストOSを載せる必要がない(厳密に言うとLinuxを走らせているのだが...)

> アプリ(Docker等コンテナを生成するもの)とWindowsのファイルシステムを完全に隔離する

と言い換えても良いかもしれない。

イメージとしては

<img width="700" height="400" alt="docker01" src="https://github.com/user-attachments/assets/0644e6fc-03b5-4076-8b1e-190dca0348e6" />

こんな感じ。

#### で、何が優れてるの？
1. ゲストOSを走らせないので、ベースとなるホストOSに影響を及ぼす事が無い(Windowsを破壊する事がない)
2. コンテナのイメージ(イメージについては後述)を他のコンテナに移植する事が容易。
   自分の開発環境を他人や本番環境、あるいはテスト環境へ丸ごとエクスポート出来る。
3.


#### 環境構築
1. [※WSL2](https://learn.microsoft.com/ja-jp/windows/wsl/install)をインストールする
2. windowsの機能でLinux用サブシステムと仮想マシンプラットフォームを有効にする
3. [Docker_Desktop](https://www.docker.com/ja-jp/products/docker-desktop/)をインストールする

- ※WSLとは？
> [Windows Subsystem for Linux](https://learn.microsoft.com/ja-jp/windows/wsl/install)の略。windows上でLinuxを動かす仮想システム。


#### 参考文献
