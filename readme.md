# path-run [![Build Status](https://travis-ci.org/chinanf-boy/Path-run.svg?branch=master)](https://travis-ci.org/chinanf-boy/Path-run) [![codecov](https://codecov.io/gh/chinanf-boy/Path-run/badge.svg?branch=master)](https://codecov.io/gh/chinanf-boy/Path-run?branch=master) [![explain](http://llever.com/explain.svg)](https://github.com/chinanf-boy/path-run-explain)

> esay change you require paths Now

[中文](./readme.md) | [english](./readme.en.md)

如果改变, 一个文件的位置, 那么相对应, 其他文件对这个文件的引用修改就是个问题

你可以试试 `path-run`, 改动你的文件位置不那么手动

## Install

```
npm install --global path-run
```

## 正确做法使用-Cli

1. 复制文件到目的地

```
- demo
	- index.js
	- input
		- input1.js
		- input2.js
	- output
		- output1.js
		- output2.js
```

```
- demo
	- index.js
	- input
		- ✂️input1.js // <===== copy to output
		- input2.js
	- output
		- ➕output3.js // <===== from input/input1.js
		- output1.js
		- output2.js
```

2. 运行 `cli`


``` bash
path-run demo/input/input1.js demo/output/output3.js
# path-run [input] [output]

```

1⃣️`process.cwd()` 下所有引用 `input` 的 路径 都会变为 `output`
2⃣️ `output` 的 文件 下, 导入相对文件正确导入



3. 移除 `input1.js`

```
- demo
	- index.js
	- input
					<===== ✂️cut
		- input2.js
	- output
		- output3.js // <===== from input/input1.js
		- output1.js
		- output2.js
```

[真实项目-transltemds](https://github.com/chinanf-boy/translate-mds/commit/af88620139276479a86185c731f4862ec54a54e4)

命令行实例

![demo-cli-show](./demo-show/demo.gif)

输入与输出文件的变化

![inpath-diff-outpath](./demo-show/diff.png)

其他导入文件变化

![index-diff](./demo-show/index-diff.png)


---

## 警告⚠️ , `path-run` 不会 改变 `package.json` main 或 bin 字段, 请自行修正

---


## API

### pathRun({options})

#### options

##### 1. InPath

Type: `string`

Abs Path

##### 2. OutPath

Type: `string`

Abs Path
##### 3. cwd

Type: `string`

default : `process.cwd()`

##### return

Type: `Array`

数组中每个值像这样

``` js
const options = {
  files: 'path/to/file',
  from: /foo/g,
  to: 'bar',
};
```

被 `replace-in-file` 使用

https://github.com/adamreisnz/replace-in-file


## CLI

```
npm install --global path-run
```

```
  esay change you require paths Now

  Usage
    $ path-run [input] [output]

  Options
        input  要更改的路径
        output 变成的路径

  Examples
        $ path-run './index' './lib/index'

  will change all process.cwd()/* files require Path 'index' => './lib/index'
```

## 联系

[nodepaths](https://github.com/chinanf-boy/NodePath) js 模块描述

## License

MIT © [chinanf-boy](http://llever.com)
