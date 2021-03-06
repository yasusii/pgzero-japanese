イベントのフック
================

イベントのフック(検知)を定義すると Pygame Zero はそのイベントに対応する処理を呼び出してくれるようになっています。この仕組みにより、イベント・ループの仕組みをわざわざ自分で書く必要はありません。

ゲーム・ループのフック
----------------------

通常、ゲームのプログラムでは次のようなゲーム・ループを書く必要があります ::

    while game_has_not_ended():
        process_input()
        update()
        draw()

そしてもっと複雑な入力処理を書く必要があるのですが、Pygame Zero を使うと ``update()`` と ``draw()`` という関数をゲームプログラムに定義するだけで済みます。

.. function:: draw()

    ゲームのスクリーンの再描画が必要なとき、Pygame Zero はこの関数を呼び出します。

    ``draw()`` に引数はありません。

    Pygame Zero は何も変更がなく、再描画の必要がなければ処理をスキップするようになっています。ゲーム・ループの繰り返しで、次の条件が当てはまるときだけスクリーンの再描画が行われます。

    * 関数 ``update()`` が定義されているとき(後述)。
    * クロック・イベントが発生したとき。
    * 入力イベントが発生したとき。

    ここで注意してほしいのは、draw 関数で表示内容を変更したり動かしたりするときの書き方です。たとえば次のコードは間違っています。エイリアンをスクリーン上で横に動かしたいのですが、意図したようには動きません。 ::

        def draw():
            alien.left += 1
            alien.draw()

    以下が正しいコードです。表示内容を変えたり動かしたり、あるいは単にスクリーンに色を塗りたいときは、 ``update()`` を使います ::

        def draw():
            alien.draw()

        def update():
            alien.left += 1

.. function:: update() または update(dt)

    Pygame Zero はゲームを進めるためにこの関数を呼び出します。この関数は1秒間に60回、くり返し呼び出されます。

    update 関数はアプローチの異なる二通りの書き方があります。

    簡単なゲームの場合、 ``update()`` 呼び出しから次の呼び出しまでの1ステップに必要な時間はわずか、ほんの一瞬とみなせます。おそらくその時間がどれくらいか気にすることもないでしょう。この場合1フレームで行う処理は、オブジェクトをある決まったピクセル数だけ動かしたり、あるいは決まった割合で加速させたり、などです。

    より高度なアプローチは、呼び出しから呼び出しの間にかかった時間をベースに運動と物理の計算を行うことです。この方法を使うとアニメーションを滑らかに表示できる一方で、計算量が大きくなる可能性があり、またその計算に時間が長くかかったときに予想外の振舞いをしないよう注意しなければなりません。

    時間ベースのアプローチを使用する場合は、update が一つの引数を受け取るようにします。関数updateに引数が設定されている場合、Pygame Zero は秒単位の経過時間を引数として渡します。この結果、その時間に応じた動きを計算をすることが可能になります。


イベント処理のフック
--------------------

ゲームループのフックと同様に、Pygame Zero プログラムでは特定の名前で関数を定義することにより、入力イベントも処理することができます。

``update()`` と同じように、Pygame Zero はイベントハンドラ関数を調べてその呼び出し方法を判別します。ですからイベントハンドラ関数の引数は必須ではありません。たとえば Pygame Zero は以下の ``on_mouse_down`` 関数のバリエーションの内、どれを使ってもちゃんと呼び出してくれます。

    def on_mouse_down():
        print("マウスのボタンがクリックされました")

    def on_mouse_down(pos):
        print("マウスのボタンが", pos, "の位置でクリックされました")

    def on_mouse_down(button):
        print("マウスの", button, "ボタンがクリックされました")

    def on_mouse_down(pos, button):
        print("マウスの", button, "ボタンが", pos, "の位置でクリックされました")

判別は引数の名前によって行なわれます。ですから引数を使う場合、名前は正確に入力する必要があります。それぞれのイベント・フックで使用できる引数の内訳を以下に記載します。

.. function:: on_mouse_down([pos], [button])

    マウスボタンが押されたときに呼び出されます。

    :param pos: (x, y)形式のタプルで、ボタンが押されたときのマウス・ポインタの位置を示します。
    :param button: 列挙型 :class:`mouse` の値で押されたボタンがどれかを示します。

.. function:: on_mouse_up([pos], [button])

    マウスボタンが離されたときに呼び出されます。

    :param pos: (x, y)形式のタプルで、ボタンが離されたときのマウス・ポインタの位置を示します。
    :param button: 列挙型 :class:`mouse` の値で離されたボタンがどれかを示します。

.. function:: on_mouse_move([pos], [rel], [buttons])

    マウスが動かされたときに呼び出されます。

    :param pos: (x, y)形式のタプルで、動かした先のマウス・ポインタの位置を示します。
    :param rel: (delta_x, delta_y)形式のタプルで、マウス・ポインタの位置の変化量を示します。
    :param buttons: 列挙型 :class:`mouse` の値の集合です。移動の間押されていたボタン(複数)を示します。

マウスのドラッグを処理したいときは、次のコードを参考にしてください ::

    def on_mouse_move(rel, buttons):
        if mouse.LEFT in buttons:
            # マウスがドラッグされた。`rel` を使って続く処理を記述する
            ...

.. function:: on_key_down([key], [mod], [unicode])

    キーが押されたときに呼び出されます。

    :param key: 整数で、押されたキーを示します(:ref:`下記参照 <buttons-and-keys>`)。
    :param unicode: キーで入力された文字。ただし制御文字のように表示できない文字の場合もあります。キーに対応しているユニコードが無い場合は空文字列となります。
    :param mod: 押された修飾キーのビットマスク。

.. function:: on_key_up([key], [mod])

    キーが離されたときに呼び出されます。

    :param key: 整数で、離されたキーを示します(:ref:`下記参照 <buttons-and-keys>`)。
    :param mod: 押された修飾キーのビットマスク。


.. function:: on_music_end()

    :ref:`音楽のトラック <music>` が完了したときに呼び出されます。

    ただしトラックにループ設定がされている場合、この関数が呼び出されることはないので注意してください。


.. _buttons-and-keys:

マウスのボタンとキー
''''''''''''''''''''

組込みのオブジェクト ``mouse`` と ``keys`` は前述のイベントでどのボタンやキーが押されたのかを示すために使われます。

マウスのスクロールホイールのイベントは次に記載したボタンの定数 ``WHEEL_UP`` または ``WHEEL_DOWN`` のボタン操作として扱われます。

.. class:: mouse

    マウスのボタンを示す組込みの列挙型オブジェクトで、 ``on_mouse_*`` ハンドラに渡されます。

    .. attribute:: LEFT
    .. attribute:: MIDDLE
    .. attribute:: RIGHT
    .. attribute:: WHEEL_UP
    .. attribute:: WHEEL_DOWN

.. class:: keys

    キーを示す組込みの列挙型オブジェクトで、 ``on_key_*`` ハンドラに渡されます。

    .. attribute:: BACKSPACE
    .. attribute:: TAB
    .. attribute:: CLEAR
    .. attribute:: RETURN
    .. attribute:: PAUSE
    .. attribute:: ESCAPE
    .. attribute:: SPACE
    .. attribute:: EXCLAIM
    .. attribute:: QUOTEDBL
    .. attribute:: HASH
    .. attribute:: DOLLAR
    .. attribute:: AMPERSAND
    .. attribute:: QUOTE
    .. attribute:: LEFTPAREN
    .. attribute:: RIGHTPAREN
    .. attribute:: ASTERISK
    .. attribute:: PLUS
    .. attribute:: COMMA
    .. attribute:: MINUS
    .. attribute:: PERIOD
    .. attribute:: SLASH
    .. attribute:: K_0
    .. attribute:: K_1
    .. attribute:: K_2
    .. attribute:: K_3
    .. attribute:: K_4
    .. attribute:: K_5
    .. attribute:: K_6
    .. attribute:: K_7
    .. attribute:: K_8
    .. attribute:: K_9
    .. attribute:: COLON
    .. attribute:: SEMICOLON
    .. attribute:: LESS
    .. attribute:: EQUALS
    .. attribute:: GREATER
    .. attribute:: QUESTION
    .. attribute:: AT
    .. attribute:: LEFTBRACKET
    .. attribute:: BACKSLASH
    .. attribute:: RIGHTBRACKET
    .. attribute:: CARET
    .. attribute:: UNDERSCORE
    .. attribute:: BACKQUOTE
    .. attribute:: A
    .. attribute:: B
    .. attribute:: C
    .. attribute:: D
    .. attribute:: E
    .. attribute:: F
    .. attribute:: G
    .. attribute:: H
    .. attribute:: I
    .. attribute:: J
    .. attribute:: K
    .. attribute:: L
    .. attribute:: M
    .. attribute:: N
    .. attribute:: O
    .. attribute:: P
    .. attribute:: Q
    .. attribute:: R
    .. attribute:: S
    .. attribute:: T
    .. attribute:: U
    .. attribute:: V
    .. attribute:: W
    .. attribute:: X
    .. attribute:: Y
    .. attribute:: Z
    .. attribute:: DELETE
    .. attribute:: KP0
    .. attribute:: KP1
    .. attribute:: KP2
    .. attribute:: KP3
    .. attribute:: KP4
    .. attribute:: KP5
    .. attribute:: KP6
    .. attribute:: KP7
    .. attribute:: KP8
    .. attribute:: KP9
    .. attribute:: KP_PERIOD
    .. attribute:: KP_DIVIDE
    .. attribute:: KP_MULTIPLY
    .. attribute:: KP_MINUS
    .. attribute:: KP_PLUS
    .. attribute:: KP_ENTER
    .. attribute:: KP_EQUALS
    .. attribute:: UP
    .. attribute:: DOWN
    .. attribute:: RIGHT
    .. attribute:: LEFT
    .. attribute:: INSERT
    .. attribute:: HOME
    .. attribute:: END
    .. attribute:: PAGEUP
    .. attribute:: PAGEDOWN
    .. attribute:: F1
    .. attribute:: F2
    .. attribute:: F3
    .. attribute:: F4
    .. attribute:: F5
    .. attribute:: F6
    .. attribute:: F7
    .. attribute:: F8
    .. attribute:: F9
    .. attribute:: F10
    .. attribute:: F11
    .. attribute:: F12
    .. attribute:: F13
    .. attribute:: F14
    .. attribute:: F15
    .. attribute:: NUMLOCK
    .. attribute:: CAPSLOCK
    .. attribute:: SCROLLOCK
    .. attribute:: RSHIFT
    .. attribute:: LSHIFT
    .. attribute:: RCTRL
    .. attribute:: LCTRL
    .. attribute:: RALT
    .. attribute:: LALT
    .. attribute:: RMETA
    .. attribute:: LMETA
    .. attribute:: LSUPER
    .. attribute:: RSUPER
    .. attribute:: MODE
    .. attribute:: HELP
    .. attribute:: PRINT
    .. attribute:: SYSREQ
    .. attribute:: BREAK
    .. attribute:: MENU
    .. attribute:: POWER
    .. attribute:: EURO
    .. attribute:: LAST

そのほかにも修飾キーを表す定数があります。

.. class:: keymods

    ``on_key_up`` または ``on_key_down`` イベント発生のとき押されていた修飾キーを示す定数です。

    .. attribute:: LSHIFT
    .. attribute:: RSHIFT
    .. attribute:: SHIFT
    .. attribute:: LCTRL
    .. attribute:: RCTRL
    .. attribute:: CTRL
    .. attribute:: LALT
    .. attribute:: RALT
    .. attribute:: ALT
    .. attribute:: LMETA
    .. attribute:: RMETA
    .. attribute:: META
    .. attribute:: NUM
    .. attribute:: CAPS
    .. attribute:: MODE

