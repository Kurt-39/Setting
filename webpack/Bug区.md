问题描述:
```log
22 error @ dev: `webpack-dev-server --inline --hot --open --port 5008`
22 error Exit status 1
23 error Failed at the @ dev script.
23 error This is probably not a problem with npm. There is likely additional logging output above.
24 verbose exit [ 1, true ]
```

当出现

```
html-webpack-plugin缺失
```

的情况,解决办法是重新执行指令:

```linux
cnpm install webpack@3.6.0 webpack-dev-server@2.9.1 html-webpack-plugin@2.30.1 --save-dev
```

