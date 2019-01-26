工作日志这样的制度具有以下特性：
1. 对领导来说 很重要，领导通过这个了解每一名员工的工作情况
2. 员工很不情愿。忙的时候本来就没时间，还要花时间写这个；不
忙的时候，没什么可写的，但是写的太少又觉得太不像样了，于是
不免搜肠刮肚的搞些名堂。

当然领导会美其名曰: 这样可以督促你提高工作效率。
工作效率有没有得到普遍的提高我不敢贸言，扯谎和把一件简单
的事情讲复杂的能力倒可能有普遍的改善和提高。

罢了，不再多言了。看代码：
总体思路是先获取每天工作的代码提交记录，抽取其中的commit信息，然后请求日志草稿接口把commit信息写进去，这样每天下班前打开草稿修改一下就可以提交了。

原先写日志大概花20-25分钟，现在5分钟就能搞定
```
#!/usr/bin/env python
# coding: utf-8

from requests import Request, Session
import subprocess
import datetime

login_name = "xulc@****.net"
pass_code = "*******"
git_dir = "/Users/****/git_***/project_root_dir"
date_val = datetime.datetime.now().strftime("%Y/%m/%d")

def daily_log_commit(username, password, lines, date_val):
    """
    提交工作日志
    :param username: 日志系统账号的用户名
    :param password: 日志系统账号的密码
    :param lines: git 代码提交信息描述
    :return: 
    """
    url = "http://www.tita.com/api/v2/****/2010*****/planDaily/saveDraft"
    login_url = "http://www.tita.com/Account/Account/LogInITalent"
    login_body = {"LoginType": 0,
                  "UserName": username,
                  "Password": password,
                  "IsShowValCode": False,
                  "ValCodeKey": "e44e9417-1a35-4191-946a52407ee4"
                  }
    headers = {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 "
                             "(KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36",
               "X-Requested-With": "XMLHttpRequest"
               }
    # 组装日志草稿内容
    content, plan = "", ""
    for dx, line in enumerate(lines):
        content += "<p>%d. %s</p>" % (dx+1, line)

    print(content, plan)
    params = {"reportType": 8, "date": date_val,
              "content": content,
              "workPlan": plan
              }

    sess = Session()
    sess.headers.update(**headers)
    # 登录
    login_req = Request('POST', login_url, data=login_body)
    login_reqed = sess.prepare_request(login_req)
    auth_resp = sess.send(login_reqed)

    assert auth_resp.status_code == 200

    # 请求保存草稿接口
    craft_req = Request("POST", url, data=params)
    craft_reqed = sess.prepare_request(craft_req)
    craft_resp = sess.send(craft_reqed)

    assert craft_resp.status_code == 200
    print(craft_resp.content)

def get_git_log(date_str, git_dir):
	"""
	获取当天git代码提交记录
	:date_str: 日期字符串
	:git_dir:  可以使用git log命令获取提交信息的路径
	:return:   type list
				提交记录信息列表
	"""
    since_time = "%s 03:00:00" % date_str
    until_time = "%s 20:00:00" % date_str
    cmd_all = "git log " + \
              " --since='%s' " % since_time + \
              " --until='%s' " % until_time + \
              " --author=shixiaopeng " \
              " --no-merges " \
              " --reverse " \
              " --format='%s'"
    print("cmd_all: ", cmd_all)
    s = subprocess.Popen(cmd_all, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE,
                         cwd=git_dir)
    out_data, out_err = s.communicate()

    return out_data.splitlines()

if __name__ == '__main__':
    lines = get_git_log(date_val, git_dir)
    daily_log_commit(login_name, pass_code, lines, date_val)
