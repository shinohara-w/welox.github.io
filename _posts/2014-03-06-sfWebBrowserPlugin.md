---
layout: post
title: Symfony�AHTTP�N���C�A���g�@�\��񋟂��Ă����v���O�C��
date: 2014-03-06
category : miyagi
tags : [Symfony]
---

##�T�[�o�ԏ����ŕ֗�

##sfWebBrowserPlugin

// �ڑ���URL
$url   = "http://hobe.jp/index.php";
// �N�G�����N�G�X�g
$query = array("a"=>1, "b"=>2);

// POST�ɂ�鑗�M
$request = new sfWebBrowser();
$request->post($url, $query);
// HTTP �������b�Z�[�W���牞���R�[�h���擾
$request->getResponseCode()
// �T�[�o�[���牞���R�[�h�ƂƂ��� HTTP �������b�Z�[�W���Ԃ��ꂽ�ꍇ�A���̃��b�Z�[�W���擾
$request->getResponseMessage()


##�����悤�ȏ�����php�݂̂ŏ�����
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
                // 404 Not found �̏ꍇ
                case 404:
                    echo "404";
                    break;
                // 500 Internal Server Error �̏ꍇ
                case 500:
                    echo "500";
                    break;
                // ���̑�
                default:
                    echo "���̑��G���[";
                    break;
            }
    // �^�C���A�E�g�̏ꍇ
    } else {
        echo "�^�C���A�E�g";
    }
// ����
} else {
    echo "����";
}

�Ȃ񂩕֗������I�I