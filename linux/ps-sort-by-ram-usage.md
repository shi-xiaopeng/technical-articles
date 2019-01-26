```
ps aux --sort -rss
[root@10-40-51-200 ~]# ps aux --sort -rss
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
git      12997  0.1 12.9 860940 504064 ?       Sl   17:18   0:03 unicorn worker[2] -D -E production -c /var/opt/gitlab/g
git      14837  0.1 12.5 785172 487940 ?       Sl   17:32   0:01 unicorn worker[1] -D -E production -c /var/opt/gitlab/g
git      12991  0.1 12.0 822172 467728 ?       Sl   17:18   0:04 unicorn worker[0] -D -E production -c /var/opt/gitlab/g
git      12880  1.5 11.3 852732 441080 ?       Ssl  17:17   0:35 sidekiq 5.2.1 gitlab-rails [0 of 25 busy]
git      12919  0.8 10.7 680652 415756 ?       Sl   17:17   0:19 unicorn master -D -E production -c /var/opt/gitlab/gitl
gitlab-+ 12858  0.7  2.8 1425104 112452 ?      Ssl  17:17   0:18 /opt/gitlab/embedded/bin/prometheus --web.listen-addres
git      12717  0.1  1.5 1428684 59484 ?       Sl   17:17   0:03 ruby /opt/gitlab/embedded/service/gitaly-ruby/bin/gital
git      12719  0.1  1.5 1441616 58700 ?       Sl   17:17   0:03 ruby /opt/gitlab/embedded/service/gitaly-ruby/bin/gital
git      12714  0.5  0.8 439608 32780 ?        Ssl  17:17   0:12 puma 3.12.0 (tcp://localhost:9168) [gitlab-monitor]
gitlab-+ 12849  0.0  0.7 326124 27696 ?        Ss   17:17   0:00 /opt/gitlab/embedded/bin/postgres -D /var/opt/gitlab/po
git      12702  0.1  0.6 476992 23396 ?        Ssl  17:17   0:03 /opt/gitlab/embedded/bin/gitaly /var/opt/gitlab/gitaly/
gitlab-+ 13013  0.0  0.3 433684 15492 ?        Ss   17:18   0:00 postgres: gitlab gitlabhq_production [local] idle
```

