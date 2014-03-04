---
layout: post
title: SymfonyでのXSS(クロスサイトスクリプティング)対策
date: 2014-03-04
category : suzuki
tags : [Symfony, XSS]
---

## SymfonyでのXSS(クロスサイトスクリプティング)対策

普通phpでXSS対策をする場合、htmlspecialchars()を通してechoします。

ただ、echoするたびにこの関数を書かなくてはいけないので非常にめんどくさい。。

Symfonyではapps/frontend/config/settings.ymlに下記設定を記述することで対策をしてくれます。


escaping_strategy: on
escaping_method:   ESC_SPECIALCHARS


どうしても生のHTMLデータで出力したいという場合は、「echo $sf_data->getRaw('変数名'); 」

とすることでHTMLデータ出力は可能です。

ちなみにアプリケーションを生成する時点で「php symfony generate:app --escaping-strategy=on」とすれば

デフォルトでsetting.ymlにXSS対策用の記述がされます。
