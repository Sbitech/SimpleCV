# SimpleCV

> [!WARNING]  
> このプロジェクトはもはや積極的にメンテナンスされていません。新しいコンピュータビジョンプロジェクトの場合は、以下のような代替手段を検討してください：
> - [OpenCV](https://opencv.org/) - 幅広いサポートと活発なコミュニティ開発がある強力なコンピュータビジョンタスク用ライブラリ。
> - [PyTorch](https://pytorch.org/) + [TorchVision](https://pytorch.org/vision/stable/index.html) - ディープラーニングとコンピュータビジョンタスクのためのフレームワーク。
> - [TensorFlow](https://www.tensorflow.org/) - 機械学習とコンピュータビジョンのための堅牢なエコシステム。
> - [scikit-image](https://scikit-image.org/) - Python用の軽量画像処理ライブラリ。
>
> 現在のところ更新予定はありませんが、将来的にこのプロジェクトが再開される可能性があります。SimpleCVを必要とするレガシープロジェクトの場合は、コードベースは現状のまま提供されます。

[![Build Status](https://travis-ci.org/sightmachine/SimpleCV.png?branch=develop)](https://travis-ci.org/sightmachine/SimpleCV)


クイックリンク:

 * [概要](#about)
 * [インストール](#installation)
    * [Docker](#docker)
    * [Ubuntu](#ubuntu-1204)
    * [仮想環境](#virtualenv)
    * [Arch Linux](#arch-linux)
    * [Fedora](#fedora)
    * [MacOS](#mac-os-x-106-and-above)
    * [Windows](#windows-7vista)
    * [Raspberry Pi](#raspberry-pi)
 * [SimpleCVシェル](#simplecv-interactive-shell-or-how-to-run-simplecv)
 * [動画 & チュートリアル](#videos---tutorials-and-demos)
 * [モバイル版SimpleCV - Android](#simplecv-on-mobile-android)
 * [ヘルプ](#getting-help)
 * [インストールのトラブルシューティング](#troubleshooting-installation-problems)
    * [必要なライブラリ](#required-libraries)
    * [オプションのライブラリ](#optional-libraries)


<a id="about"></a>
## 概要
---------------------------
SimpleCVを使ってコンピュータに視覚を与える、オープンソースのコンピュータビジョンフレームワーク

SimpleCVは、OpenCVとPythonプログラミング言語を使用したオープンソース機械視覚フレームワークです。
カメラ、画像操作、特徴抽出、フォーマット変換のための簡潔で読みやすいインターフェースを提供します。私たちの使命は、一般ユーザーに基本的な機械視覚機能の包括的なインターフェースを提供し、上級ユーザーにエレガントなプログラミングインターフェースを提供することです。

SimpleCVが気に入った理由：

* 初心者プログラマーでも簡単な機械視覚テストを書くことができます
* カメラ、ビデオファイル、画像、ビデオストリームはすべて相互運用可能です
* 画像特徴の情報を簡単に抽出、並び替え、フィルタリングできます
* 操作は高速で、覚えやすい名前が付けられています
* 線形代数は必須ではありません

SimpleCVの"Hello World"は以下の通りです：

    import SimpleCV
    camera = SimpleCV.Camera()
    image = camera.getImage()
    image.show()

より多くのコードスニペットについては、[SimpleCV examplesウェブサイト](http://examples.simplecv.org)または[SimpleCV/examples](http://github.com/sightmachine/SimpleCV/tree/master/SimpleCV/examples)のサンプルスクリプトをご覧ください。

---------------------------
<a id="installation"></a>
## インストール

SimpleCVをインストールする最も簡単な方法は、ウェブサイト(http://www.simplecv.org)に含まれているディストリビューション(Windows、Mac、Linux)用のパッケージを使用することです。多くのプラットフォームでテストされていますが、パッケージインストーラーで動作しないシナリオがあるかもしれません。以下にインストール方法を示します。問題が発生した場合は、このREADMEファイルの最後のトラブルシューティングセクションを参照してください。

<a id="docker"></a>
### Docker
Dockerを使用すると、環境がまったく同じように設定されるため、SimpleCVをインストールする推奨方法です。

*警告*: Dockerを使用するとウェブカメラは動作しません。また、Image.show()でも動作しないため、基本的にIPythonノートブック内でsimplecvを使用する必要があります。

最初のステップは、まだインストールしていない場合はDockerをマシンにインストールすることです。Windows、Mac、Linuxで動作します。手順については以下を参照してください：
<a href="https://docs.docker.com/installation/">https://docs.docker.com/installation/</a>

Dockerをインストールしたら、以下を実行するだけでsimplecvを実行できます(OSによってはsudoで実行する必要があります)：

    docker pull sightmachine/simplecv

ダウンロードに少し時間がかかるかもしれませんが、完了したら以下を実行します(OSによってはsudoで実行する必要があります)：

    docker run -p 54717:8888 -t -i sightmachine/simplecv

次に、ウェブブラウザを開いて以下にアクセスします：

    http://localhost:54717

**注**: MacまたはWindowsを使用している場合は、boot2dockerを実行する必要があるため少し異なります。boot2docker upを実行すると、dockerサービスのIPアドレスが表示されます。192.168.59.103のようなものですが、ランダムなので変更される可能性があります。IPアドレスがわかったら、代わりにそのIPアドレスと正しいポートにアクセスします：

    http://192.168.59.103:54717

IPythonノートブックインターフェースが表示されます。新しいノートブックを作成して以下を入力します：

    from SimpleCV import *
    disp = Display(displaytype='notebook')
    img = Image('simplecv')
    img.save(disp)

SimpleCVロゴが表示され、SimpleCV環境が完全に設定されます。これで遊び始めることができます。

<a id="ubuntu-1204"></a>
### Ubuntu 12.04
pipでインストール

	sudo apt-get install ipython python-opencv python-scipy python-numpy python-pygame python-setuptools python-pip
	sudo pip install https://github.com/sightmachine/SimpleCV/zipball/develop

SimpleCVリポジトリのクローンを使用してインストール

    sudo apt-get install ipython python-opencv python-scipy python-numpy python-pygame python-setuptools git
    git clone https://github.com/sightmachine/SimpleCV.git
    cd SimpleCV/
    sudo pip install -r requirements.txt
    sudo python setup.py install

次に、シェルから'simplecv'を実行するだけです。

### 仮想環境

これは、python仮想環境[virtualenv] (http://www.virtualenv.org)下でSimpleCVをインストールする方法です。システムライブラリをクリーンに保ち、余分なライブラリをインストールしたくない場合に役立ちます。この方法はUbuntu 12.04でのみテストされていますが、他のオペレーティングシステムに移植することも可能です。

以下のコマンドを実行します：

    sudo apt-get install python-opencv python-setuptools python-pip gfortran g++ liblapack-dev libsdl1.2-dev libsmpeg-dev mercurial
    sudo pip install virtualenv
    virtualenv venv
    cd venv
    mkdir src
    ln -s /usr/local/lib/python2.7/dist-packages/cv2.so lib/python2.7/site-packages/cv2.so
    ln -s /usr/local/lib/python2.7/dist-packages/cv.py lib/python2.7/site-packages/cv.py
    ./bin/pip install -r requirements.txt
    mkdir src
    wget -O src/pygame.tar.gz https://bitbucket.org/pygame/pygame/get/6625feb3fc7f.tar.gz
    cd src
    tar zxvf pygame.tar.gz
    cd ..
    ./bin/python src/pygame-pygame-6625feb3fc7f/setup.py -setuptools install
    ./bin/pip install https://github.com/sightmachine/SimpleCV/zipball/develop





<a id="archlinux"></a>
### Arch Linux
pipでインストール

    pacman -S python2-numpy opencv2.4.4_1 python-pygame python2-setuptools ipython2 python2-pip
    pip install https://github.com/sightmachine/SimpleCV/zipball/develop

SimpleCVリポジトリのクローンを使用してインストール

    pacman -S python2-numpy opencv2.4.4_1 python-pygame python2-setuptools ipython2
    git clone https://github.com/sightmachine/SimpleCV.git
    cd SimpleCV/
    sudo python setup.py install

AURを使用して開発バージョンをインストール

    yaourt -S simplecv-git

<a id="fedora"></a>
### Fedora
#### Fedora 20以降

    sudo yum -y install python-SimpleCV

#### Fedora 18
pipでインストール

    sudo yum -y install python-ipython opencv-python scipy numpy pygame python-setuptools python-pip
    sudo python-pip install https://github.com/sightmachine/SimpleCV/zipball/develop

SimpleCVリポジトリのクローンを使用してインストール

    sudo yum -y install python-ipython opencv-python scipy numpy pygame python-setuptools python-pip git
    git clone https://github.com/sightmachine/SimpleCV.git
    cd SimpleCV/
    sudo python setup.py install

<a id="macos">
### Mac OS X (10.6以降)
</a>

**一般的なOSXの概要**

注：もともと、Macのすべての依存関係をスーパーパックにまとめようとしました。しかし、Mac OSのバージョン間の多くの違いにより、これは非常に困難であることが判明しました。現在、Macではソースからビルドする必要があり、できるだけ簡単にするよう努めています。問題が発生した場合はバグを報告してください。


---------------------------
**JHawkinsによる明示的な（すべての手順の）手順**

*これらの手順は、OSXでPython開発を始めたばかりの人を対象としています。SimpleCVをゼロから構築するために必要なすべてのツールを設定する手順を説明します。どの手順を使用するかわからない場合は、おそらくこれらを使用する必要があります。*

App Store経由でXcodeをインストールします
Xcodeを起動し、Xcode >> 環境設定 >> ダウンロード >> コマンドラインツールの横にある「インストール」をクリックします
ターミナルがすでに実行中の場合は、シャットダウンして再起動します
OS Xの/usr/localの権限は制限が厳しすぎるため、以下を実行して変更する必要があります：

    sudo chown -R `whoami` /usr/local

ターミナル経由でhomebrewをインストールします：

    ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"

XcodeのCLIツールをインストールするよう指示する単一の警告は無視してください（すでにインストールしています）
homebrewが正しくインストールされ動作していることを確認するには、以下を実行します：

    brew doctor

エラーがある場合は解決してから進んでください。Googleは友達です。
注：Parallelsを介してVMを実行していて、"osxfuse"に関連する複数の警告が表示された場合は、システム環境設定 >> FUSE for OS X >> OSXFUSEを削除をクリックしてください。必要になったら後で追加できます。
doctorが「raring to brew」と表示したら、以下を実行します：

    brew update

次に

    brew upgrade

homebrewを介してOpenCVをインストールするには、以下を実行します：

    brew tap homebrew/science
    brew install opencv

~/.bash_profileに要求された行を追加してください：

    export PYTHONPATH="/usr/local/lib/python2.7/site-packages:$PYTHONPATH"

変更を有効にするために~/.bash_profileファイルを読み込みます：

    source ~/.bash_profile

homebrewを介してGitをインストールするには、以下を実行します：

    brew install git
