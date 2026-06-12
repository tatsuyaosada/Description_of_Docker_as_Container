#### Dockerを例に用いたコンテナによる仮想サーバーの概要と実践
ウェブ班第5回勉強会 担当:長田
***

#### そもそもコンテナって何？
一般的な仮想サーバーはベースとなっているメインOS上に、更にサブシステムとしてゲストOSを乗せ、その上でサーバーを走らせる、と言う手法を取る。一方でコンテナは、ベースOS上にサブシステムとしてゲストOSを載せる必要がない(厳密に言うとLinuxを走らせているのだが...)

イメージとしては

<img width="700" height="400" alt="docker01" src="https://github.com/user-attachments/assets/0644e6fc-03b5-4076-8b1e-190dca0348e6" />

こんな感じ。


#### 環境構築
1. [※WSL2](https://learn.microsoft.com/ja-jp/windows/wsl/install)をインストールする
2. windowsの機能でLinux用サブシステムと仮想マシンプラットフォームを有効にする
3. [Docker_Desktop](https://www.docker.com/ja-jp/products/docker-desktop/)をインストールする

- ※WSLとは？
> [Windows Subsystem for Linux](https://learn.microsoft.com/ja-jp/windows/wsl/install)の略。windows上でLinuxを動かす仮想システム。
