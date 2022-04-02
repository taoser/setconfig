# setconfig
Automatic processing method for adding, modifying and deleting PHP configuration files.

## 使用方法

> app即为config/app.php文件

```html
	$data = [
		true,false,111,
		'aaa'=>'bbb',
		......
	];
	$conf = new \Taoser\SetConfig\SetArr('app');
	$conf->add($data);
```

### 添加数组节点

> 支持嵌套4级数组，最后一级数组只能是数值数组，只能对数值数组添加备注，不能对关联数组添加备注

```
$add = [
    1,true,false,
    "//支持备注的添加",
    "base_path() . DIRECTORY_SEPARATOR . 'public',"
    'a'    => 1,
    'b'    => 'b',
    'c'    => true,
    'd'    => false,
    'e'    => "support\bootstrap\Session::class,",
    'f'    => [
        22,true,false,
        'aa'    => 11,
        'bb'    => 'bb',
        'cc'    => true,
        'dd'    => false,
        "//支持备注的添加",
        'ee'    => "base_path() . DIRECTORY_SEPARATOR . 'public',"
        'ff'    => [
            333,true,false,
            'aaa'    => 11,
            'bbb'    => 'bb',
            'ccc'    => true,
            'ddd'    => false,
            'eee'    => "support\bootstrap\Session::class,",
            'fff'    => [
                "//支持备注的添加",
                'aaaa'    => 11,
                'bbbb'    => 'bb',
                'cccc'    => true,
                'dddd'    => false,
                'eeee'    => "support\bootstrap\Session::class,",
            ],
        ],
        'gg'    => [
            1,true,false,
            "base_path() . DIRECTORY_SEPARATOR . 'public',"
            'aa'    => 11,
            'bb'    => 'bb',
            'cc'    => true,
            'dd'    => false,
            'ee'    => "support\bootstrap\Session::class,",
        ],
    ],
    'g'    => [
        1,true,false,
        'ga'    => 11,
        'gb'    => 'bb',
        'gc'    => true,
        'gd'    => false,
        'ge'    => "support\bootstrap\Session::class,",
        'gf'    => [
            1,true,false,
            "base_path() . DIRECTORY_SEPARATOR . 'public',"
            'gaa'    => 11,
            'gbb'    => 'bb',
            'gcc'    => true,
            'gdd'    => false,
            'gee'    => "support\bootstrap\Session::class,",
        ],
    ],
];

$conf = new \Taoser\SetConfig\SetArr('app');
$conf->add($add);
```

### 编辑数组节点

> 数组编辑，不能直接对一围数值型索引数组进行操作，索引数组的编辑需要先delete删除，再add添加value。

```
$edit = [
    'a'    => 1,
    'b'    => 'b',
    'c'    => true,
    'd'    => false,
    'e'    => "support\bootstrap\Session::class,",
    'f'    => [
        'aa'    => 11,
        'bb'    => 'bb',
        'cc'    => true,
        'dd'    => false,
        'ee'    => "base_path() . DIRECTORY_SEPARATOR . 'public',"
        'ff'    => [
            'aaa'    => 11,
            'bbb'    => 'bb',
            'ccc'    => true,
            'ddd'    => false,
            'eee'    => "support\bootstrap\Session::class,",
            'fff'    => [
                'aaaa'    => 11,
                'bbbb'    => 'bb',
                'cccc'    => true,
                'dddd'    => false,
                'eeee'    => "support\bootstrap\Session::class,",
            ],
        ],
        'gg'    => [
            1,true,false,
            "base_path() . DIRECTORY_SEPARATOR . 'public',"
            'aa'    => 11,
            'bb'    => 'bb',
            'cc'    => true,
            'dd'    => false,
            'ee'    => "support\bootstrap\Session::class,",
        ],
    ],
    'g'    => [
        'ga'    => 11,
        'gb'    => 'bb',
        'ge'    => "support\bootstrap\Session::class,",
        'gf'    => [
            'gaa'    => 11,
            'gbb'    => 'bb',
            'gcc'    => true,
            'gdd'    => false,
            'gee'    => "support\bootstrap\Session::class,",
        ],
    ],
];

$conf = new \Taoser\SetConfig\SetArr('app');
$conf->edit($edit);
```

### 删除数值

> 可删除//备注，bool, key等,索引数组给定value即会删除，关联数组需要给定key,value值为空,0,false,null均会删除。

```
$del = [
    true,false,111,'US-A',
	"// 删除备注",
	"base_path() . DIRECTORY_SEPARATOR . 'public',",
    'a'    => 0,
    'b'    => 0,
    'c'    => 0,
    'd'    => 0,
    'e'    => 0,
    'f'    => [
        'aa'    => '',
        'bb'    => '',
        'cc'    => '',
        'dd'    => '',
        'ee'    => ""
        'ff'    => [
            'aaa'    => false,
            'bbb'    => false,
            'ccc'    => false,
            'ddd'    => false,
            'eee'    => false,
            'fff'    => [
                'aaaa'    => null,
                'bbbb'    => null,
                'cccc'    => null,
                'dddd'    => null,
                'eeee'    => null,
            ],
        ],
];

$conf = new \Taoser\SetConfig\SetArr('app');
$conf->delete($del);
```
