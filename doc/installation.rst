Pygame Zero のインストール
==========================

Mu エディタに同梱のものを使う
-----------------------------

`Mu エディタ <https://codewith.mu>`_ はプログラミング初心者向けのエディタで、あらかじめ Pygame Zero が同梱されています。

`モードの選択 <https://codewith.mu/en/tutorials/1.0/modes>`_ で Pygame Zero 選ぶと Pygame Zero が使えるようになります。プログラム入力後、 `プレイのボタン <https://codewith.mu/en/tutorials/1.0/pgzero>`_ を押すと Pygame Zero で実行されます。

.. caution::

    Mu エディタに同梱されている Pygame Zero のバージョンは最新ではない場合もあります。Mu に次のコードを入力し、実行することでバージョンを確認できます ::

        import pgzero
        print(pgzero.__version__)


スタンドアローン版のインストール
--------------------------------

まず最初に  **Python 3** をインストールする必要があります。 **Linux** や **Raspberry Pi** を使っているなら、あらかじめインストールされているはずです。そのほかのシステムを使っている場合は `python.org <https://www.python.org/>` からダウンロードしてください。

Windows
'''''''

Pygame Zero のインストールには **pip** を使います。 `コマンドプロンプト`__ で次のように入力してください。

.. __: https://www.lifewire.com/how-to-open-command-prompt-2618089

::

    pip install pgzero


Mac
'''

ターミナルで次のように入力してください

::

   pip install pgzero


Mac 版 Python 3.4 をサポートした Pygame の wheel は提供されていないので注意してください。このためバージョン 3.6 以上(または 2.7)の Python を使う必要があります。利用可能な wheel のリストについては `pyPI_` を参照してください。

.. _pyPI: https://pypi.org/project/Pygame/#files

Linux
'''''

ターミナル・ウィンドウで次のように入力してください

::

   sudo pip install pgzero

Linux のディストリビューションやバージョンによっては  ``pip3`` となっている場合があります。もし ``sudo: pip: command not found`` のようなエラーが表示されたら、次の内容を試してみてください ::

    sudo pip3 install pgzero

pip 自体が入っておらず、自分でインストールしなくてはならない場合もあります。エラーが出るときは先のコマンドをやり直す前に次のコマンドを試してみてください ::


    sudo python3 -m ensurepip


.. _install-repl:

REPL のインストール
-------------------

:doc:`Pygame Zero の REPL <repl>` はオプションの機能です。インストールするには ``pip`` のコマンドラインに ``pgzero[repl]`` を指定します ::

    pip install pgzero[repl]

REPL がインストールされているかどうか分からないときに上記内容を実行しても大丈夫です。既にインストール済であっても、既存の環境を壊すことはありません。

