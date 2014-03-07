---
layout: post
title: Symfony、HTTPクライアント機能を提供してくれるプラグイン
date: 2014-03-06
category : miyagi
tags : [Symfony]
---

##サーバ間処理で便利

##sfWebBrowserPlugin

// 接続先URL
$url   = "http://hobe.jp/index.php";
// クエリリクエスト
$query = array("a"=>1, "b"=>2);

// POSTによる送信
$request = new sfWebBrowser();
$request->post($url, $query);
// HTTP 応答メッセージから応答コードを取得
$request->getResponseCode()
// サーバーから応答コードとともに HTTP 応答メッセージが返された場合、そのメッセージを取得
$request->getResponseMessage()


##同じような処理をphpのみで書くと
$url   = "http://hobe.jp/index.php";
$query = http_build_query(array("a"=>1, "b"=>2));
$header = array(
                "Content-Type: application/x-www-form-urlencoded",
                 "Content-Length: ".strlen($data)
);
$context = array(
                 "http"    => array(
                 "method"  => "POST",
                 "header"  => implode("\r\n", $header),
                 "content" => $data,
                 'timeout' => 30
                )
);
$result = @file_get_contents($url, false, stream_context_create($context));
if($result === FALSE) {
    if(count($http_response_header) > 0) {
        $stat_tokens = explode(' ', $http_response_header[0]);
            switch($stat_tokens[1]) {
                // 404 Not found の場合
                case 404:
                    echo "404";
                    break;
                // 500 Internal Server Error の場合
                case 500:
                    echo "500";
                    break;
                // その他
                default:
                    echo "その他エラー";
                    break;
            }
    // タイムアウトの場合
    } else {
        echo "タイムアウト";
    }
// 成功
} else {
    echo "成功";
}

なんか便利そう！！
