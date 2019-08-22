Pygame Zero へのコントリビュート
================================

.. highlight:: none

Pygame Zero プロジェクトは GitHub でホストされています。

    https://github.com/lordmauve/pgzero

.. _report-issue:

バグ報告や要望を送る
--------------------

Pygame Zero のバグ報告や機能の要望は  `Github issue tracker`_ から送ってください。

バグ報告などを行う前に留意すべき事項は以下の通りです。

* ほかの人も同じことをしている可能性があります。既存のイシューを検索して(open か closed)に関わらず)ほかの人が既にイシューを登録していないか確認してください。
* 開発者はどのバージョンの Pygame Zero を使っているのか、動かしている OS ((Windows, Mac, Linux 等) とそのバージョン(Windows 10, Ubuntu 16.04 等)を知る必要があります。

.. _`Github issue tracker`: https://github.com/lordmauve/pgzero/issues


プルリクエストの作成方法
------------------------

プルリクエストを作成することで、Pygame Zero を変更することができます。

まず最初に :ref:`イシューを報告 <report-issue>` するのが良い方法です。そうすることで変更内容が意味のあるものかどうかを議論することができます。

Github には `プルリクエストの作成方法に関するヘルプ`__ もありますが、ここにその簡易バージョンを記載します。

.. __: https://help.github.com/articles/creating-a-pull-request/

1. Github にログインしていること確認してください。
2. `Pygame Zero の Github ページ`_ へ行きます。
3. "Fork" ボタンをクリックして自分用にリポジトリの fork を作成します。
4. この fork を自分のコンピュータに fork します ::

        git clone git@github.com:yourusername/pgzero.git

   ``yourusername`` は自分の Github ユーザー名に置き換えることを忘れないでください。

5. 変更を行うためのブランチを作成します。ブランチ名は変更内容を反映したものにしてください  ::

        git checkout -b my-new-branch master

6. コードの変更を行います。
7. commit するファイルを add します ::

        git add pgzero

8. 完結なコミット・メッセージを付けてファイルを commit します ::

        git commit -m "Fixed issue #42 by renaming parameters"

   6 から 8 までのステップを必要なだけ繰り返します。

9. 先に fork したリポジトリに commit 内容を push します ::

        git push --set-upstream origin my-new-branch

10. fork の Github ページへ行き、"Create pull request" ボタンをクリックします。


.. _`Pygame Zero の Github ページ`: https://github.com/lordmauve/pgzero


開発用のインストール
--------------------

pip を使ってローカルに編集可能なインストールを行うことができます。チェックアウトしたソースのルートへ移動し、以下を実行してください ::

    pip3 install --editable .

これでインストールしたバージョンにはローカルの変更内容がすべて反映されるようになります。

別の方法として、何もインストールしたくない場合は次のようにすれば実行可能です ::

   python3 -m pgzero <pgzero のスクリプト名>

例::

   python3 -m pgzero examples/basic/demo1.py


テストの実行方法
----------------

テストは次のようにすれば実行されます ::

    python3 setup.py test


.. _translating:

ドキュメント翻訳の手助け
------------------------

Pygame Zero の API 自体は英語ですが、ドキュメントが世界各地域の言語に翻訳されていれば、もっと多くの人たちに Pygame Zero を使ってもらえます。

もしあなたが他の言語に堪能なら、ドキュメントのすべて、あるいは一部を翻訳してコントリビュートすることを、ぜひ検討してください。

ドキュメントは技術文書用のテキストベースのマークアップ言語  reStructuredText_ で書かれています。翻訳の際は元のドキュメントのフォーマットをできる限りそのまま生かすようにしてください。reStructuredText は慣れてしまえばさほど難しいものではありません。

ドキュメントの翻訳版を作成するには、まず Github 上にドキュメントのコピーを作成し、(少なくとも一部を)あなたがサポートしたい他の言語に書き換えてください。この方法のメリットは ``pgzero`` プロジェクト本体にプルリクエストを送る必要がなく、あなたが自分のペースで作業を進められることです。詳しい内容については Read The Docs の `translation guide`_ を参照してください。

もしやってみようかなと感じたら、以下の内容に従って始めてください。

1. まず  `pgzero issue tracker`_ で翻訳開始のイシューをオープンします。その前に、既に誰かが翻訳のイシューを登録していないか、検索して確認してください。そうすることで誰かが既に始めている翻訳作業との重複を防げます(代わりに共同して作業を進めることができます)。
2. 自分自身の新しい Github リポジトリを pgzero-*language* という名前で作詞します。例: スペイン語への翻訳なら  ``pgzero-spanish`` です。
3. リポジトリを自分のコンピュータ上に clone します。
4. Pygame Zero の ``doc/`` ディレクトリをダウンロードして、自分のプロジェクトへ commit します。 `repository ZIP file`_ を展開するだけで OK です。余計なファイルは削除してください。
5. ここまで準備ができたら、docs ディレクトの下にある .rst ファイルを自分の好きなエディタを使って翻訳していきます。でき上がったものは順次 commit、Github に push していきます。
6. ステップ 1 で作成したイシューのコメントとして、リポジトリへのリンクをポストしてください。ある程度進んだら、すぐにこれを行なってください。そうすれば、興味を持った人が翻訳に協力しやすくなります。
7. `Set up the documentation to build on Read The Docs`__ に従いドキュメントを Read The Docs にセットしてアクセスできるようになったら、再びその旨を Github のイシューにコメントしてください。
8. 最後にわたしたちが、Pygame Zero のドキュメントに新たな翻訳版へのリンクを追加します。

.. _reStructuredText: http://www.sphinx-doc.org/en/master/rest.html
.. _`translation guide`: https://docs.readthedocs.io/en/latest
                         /localization.html#project-with-multiple-translations
.. _`pgzero issue tracker`: https://github.com/lordmauve/pgzero/issues/new
.. _`repository ZIP file`: https://github.com/lordmauve/pgzero/archive/master.zip

.. __: https://docs.readthedocs.io/en/latest/getting_started.html#import-your-docs

注意 Pygame Zero は随時アップデートされ、それに連れてドキュメントも変更されます。git を使って英語版の変更部分の diff を確認できますから、対応する部分の翻訳を修正してください。
