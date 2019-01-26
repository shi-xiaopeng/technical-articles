## redis-server
### start
redis-server [redis.conf]  如果macOS 并使用 homebrew 安装, then the default `conf` file path is `/usr/local/etc/redis.conf`

### stop
redis-cli shupdown, you can specify host by `-h`, port by `-p`.
If you have password, you can first into the redis-cli, 'auth password' to get auth and then `shutdown`

