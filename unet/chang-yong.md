# 常用

## NetworkBehaviour

* isServer

  是否是`Server`，`Host`也会返回`true`

* isClient

  是否是`Client`，`Host`也会返回`true`

* \[SyncVar\]

  修饰的变量会在所有`Client`、`Server`间自动同步，无法修饰内存不连续变量，如List、Dictionary

