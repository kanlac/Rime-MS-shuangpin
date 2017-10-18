# Rime-MS-shuangpin

由于 iOS 上第三方输入法不甚稳定，且原生键盘默认的微软码表同我正在使用的自然码差异不大，所以决定尽早更换输入方案（虽然并不熟练）。而 Mac 上鼠须管并没有默认提供微软的方案，于是按照已有的 `double_pinyin.schema.yaml` 自建了一个。

对照两个自然码和微软双拼两个码表，只有「R」，「Y」，「O」，「;」这几个键位存在差异，所以只需要更改这几项的码表映射和上屏显示就 ok 了。

### 创建双拼文件
在 terminal 中执行：
```
$ cd /Users/USER_NAME/Library/Rime
$ touch double_pinyin_mspy.schema.yaml
$ open .
```

用编辑器（如 [Sublime Text](double_pinyin_mspy.schema.yaml)）打开 double_pinyin.schema 文件，全选内容复制到刚刚创建的 yaml 文件，更改 schema 段下的值，并将 translator - prism 下的值改为 `double_pinyin_mspy`。

### 修改码表映射
在 Speller - algebra 段下：
/用 # 注释掉的代码为需被替换的代码/
```
# 为 R 增加 er 映射
# - xform/[uv]an$/R/
- xform/er|[uv]an$/R/

# 为 Y 增加 v 映射，并移除 ing 映射
# - xform/ing$|uai$/Y/
- xform/v|uai$/Y/

# 添加 ; 映射
- xform/ing$/;/

# 将 O 作为零声母填充
- xform/^([aoe].*)$/O$1/
```


### 上屏全拼显示
在 translator - preedit_format 段下：
/用 # 注释掉的代码为需被替换的代码/
```
- xform/(\w)r/$1er/

# - xform/(\w)y/$1ing/
- xform/(\w)y/$1v/

- xform/(\w);/$1ing/
```


### 应用方案
在 default.yaml 的 schema_list 中，添加 `double_pinyin_mspy` 键。保存文件后重新部署，再通过 ctrl + ` 选单切换即可使用。
