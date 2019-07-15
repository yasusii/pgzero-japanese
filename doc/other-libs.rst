Pygame Zero に似たライブラリ
==========================

Pygame Zero は Python のトレンド、"zero" ライブラリ・シリーズのひとつとしてスタートしました。仲間たちがこれらの素晴しいライブラリを作っています。その内いくつかは、Pygame Zero と一緒に合わせて使うこともできます。

Network Zero
------------

`Network Zero`_ を使うと複数のマシン、あるいは同一マシンの複数プロセスの相互検知とネットワーク通信を簡単に実現できます。

.. 注意::

    Network Zero を Pygame Zero と一緒に使う場合、ブロック(ネットワークのメッセージ待ちで処理を止めてしまうこと)をさせてはいけません。Pygame Zero の中でこのブロックが発生すると、スクリーンのアニメーションや入力に対する応答処理なども止まってしまいます。 ``wait_for_s`` または ``wait_for_reply_s`` には常にオプションの値  ``0`` 秒を指定し、ブロックしないようにしてください。

.. _`Network Zero`: https://networkzero.readthedocs.io


GUI Zero
--------

`GUI Zero`_ はウィンドウ、ボタン、スライダー、テキストボックスなどのグラフィカル・ユーザー・インターフェース (GUI) を作成するためのライブラリです。

ただし GUI Zero と Pygame Zero はそれぞれ異なるやり型でスクリーンの描画を行なっているため、両者を一緒に使うことはできません。

.. _`GUI Zero`: https://lawsie.github.io/guizero/


GPIO Zero
---------

`GPIO Zero`_ は  `Raspberry Pi`_ の General Purpose Input/Output (GPIO) 
ピンに接続されたデバイスを制御するためのライブラリです。

GPIO Zero 自体が独自のスレッドで動作するため、問題なく Pygame Zero と組み合わせて使うことができます。

.. 注意::

    GPIO Zero のサンプルコードをコピーして試す際、 ``time.sleep()`` の呼び出しや ``while True:`` ループをそのまま使わないようにしてください。これらの処理は Pygame Zero のスクリーン・アニメーションや入力に対する応答処理などを止めてしまいます。関数を定期的に呼び出したいときは  :ref:`clock` を、フレーム毎に値のチェックをしたいときは :func:`update()` を使うようにしてください。

.. _`GPIO Zero`: https://gpiozero.readthedocs.io/
.. _`Raspberry Pi`: https://www.raspberrypi.org/


Adventurelib
------------

`Adventurelib`_ はテキストベースのゲームを書きやすくするためのライブラリです(ただし、何でも自動的にやってくれるわけではありません!)。

テキストベースのゲームを作るにはグラフィカルなゲームとはまったく異なるスキルが必要です。

Adventurelib は Pygame Zero よろもやや高度なレベルの Python プログラマを対象としています。

また Adventurelib は今のところ Pygame Zero と組み合わせて使うことはできません。

.. _Adventurelib: https://adventurelib.readthedocs.io/


Blue Dot
--------

`Blue Dot`_ を使うと、Android デバイスを Bluetooth リモート・コントローラにして、Raspberry Pi プロジェクトをワイヤレスで制御できます。

Blue Dot は通常、自身の独自のスレッドで動作するため、問題なく Pygame Zero と組み合わせて使うことができます。

.. 注意::

    Pygame Zero と一緒に使う場合、 ``time.sleep()`` の呼び出し、 ``while True:`` ループや Blue Dot の  ``wait_for_press`` および ``wait_for_release`` の使用は避けてください。これらの処理は Pygame Zero のスクリーン・アニメーションや入力に対する応答処理などを止めてしまいます。関数を定期的に呼び出したいときは  :ref:`clock` を、フレーム毎に値のチェックをしたいときは :func:`update()` を使うようにしてください。

.. _`Blue Dot`: https://bluedot.readthedocs.io/


.. ヒント::

    ここに掲載した以外のライブラリをご存じですか？

    もし知っていたらイシュートラッカーに `イシューを登録して <https://github.com/lordmauve/pgzero/issues/new>`_ 知らせてください。
