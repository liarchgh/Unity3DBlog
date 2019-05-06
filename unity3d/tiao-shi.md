# 调试

## log

通过定义宏来输出log，容易整理

想要看到log输出的时候可以直接屏蔽宏即可，可以保留log代码

```text
#define LS_LOG

#if LS_LOG
    OutputLog();
#endif
```

