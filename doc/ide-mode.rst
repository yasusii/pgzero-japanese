IDLE や 他の IDE での Pygame Zero 実行
======================================

.. versionadded:: 1.2

通常 Pygame Zero は次のようなコマンドで実行します ::

    pgzrun my_program.py

しかし IDLE や Edublocks などの IDE 上からは ``python`` だと実行できますが、 ``pgzrun`` は実行できません。

Pygame Zero は ``python`` を使い、普通の Python プログラムとして実行する方法も提供しています。それにはまず、プログラムの冒頭に次の行を追加します ::

    import pgzrun

そして次の行をプログラムの最後に追加してください ::

    pgzrun.go()

例
--

これはスクリーンに円を描く Pygame Zero プログラムです。この内容はそのまま IDLE にペーストして実行できます ::

    import pgzrun


    WIDTH = 800
    HEIGHT = 600

    def draw():
        screen.clear()
        screen.draw.circle((400, 300), 30, 'white')


    pgzrun.go()
