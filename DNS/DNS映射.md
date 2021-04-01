

# 解决污染

1. 打开 www.ipaddress.com 查询下面四个网站的 IP

   > https://github.com/
   > https://assets-cdn.github.com/
   > http://global.ssl.fastly.net/
   > codeload.github.com

2. 修改 hosts 文件【C:\Windows\System32\drivers\etc】，进行 DNS 映射，以下文字写进hosts 中

   ~~~shell
   # GitHub
   140.82.114.3 github.com
   185.199.108.153 assets-cdn.github.com
   185.199.109.153 assets-cdn.github.com
   185.199.110.153 assets-cdn.github.com
   185.199.111.153 assets-cdn.github.com
   140.82.113.9 codeload.github.com
   199.232.68.249 global.ssl.fastly.net
   ~~~

3. 然后 win + R 输入 cmd，打开命令行界面

   ~~~sh
   # 输入刷新 DNS 缓存即可
   ipconfig/flushdns 
   ~~~

4. 如果某一天发现网速又变慢了, 可以重新按上面的步骤查询最新的 ip 即可

5. …