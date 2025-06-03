这是一个使用 Github Action 自动部署 ASP.NET Web API 到 IIS 的示例
使用 appleboy/ssh-action 连接到 windows server
需要注意的是，该 action 在 ssh 目标是windows系统时，执行多行命令存在bug，只能按照下面方式书写脚本：
```yml
script: |
  echo "first cmd" & echo "second cmd" & (if exist c:\somepath ( echo "if cmd" & echo "if cmd2" ) else ( echo "else cmd" )) & echo "last cmd"
```
要点：
1. 在单行中书写脚本
2. 使用 & 分割命令
3. if-else 等组合命令用 `()` 包围，视作一条命令

说明：
yaml 的 string 参数可以使用 > 标记来忽略换行符，但经过测试无法工作。目前只有这种方式最稳定。
