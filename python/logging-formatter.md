logging 的日期格式时间带精确到 毫秒
```
formatter = logging.Formatter(fmt='%(asctime)s.%(msecs)03d %(name)-12s %(levelname)-8s %(message)s',
                              datefmt='%m/%d/%Y %H:%M:%S')
```
