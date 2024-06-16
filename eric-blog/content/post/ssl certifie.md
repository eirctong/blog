+++
title = 'SSL签发'
date = 2024-06-15T23:24:07+08:00
draft = false
summary = "ssl证书签发指南"
tags = ["ssl", "certificate"]
lastmod = true
pin = true
+++
# 参考资料
http://www.gmloc.me/50.html
https://u.sb/acme-sh-ssl/
1. acme.sh
wget -O -  https://get.acme.sh | sh -s erictong666@gmail.com
1. 生成API KEY
2. https://www.namesilo.com/account/api-manager
3. ![image-20230625200750737](/Users/bytedance/Library/Application Support/typora-user-images/image-20230625200750737.png)
export Namesilo_Key="申请的key"
测试此key是否可用
curl 'https://www.namesilo.com/api/listDomains?version=1&type=xml&key=xxx' 
1. 切换
acme.sh --set-default-ca --server letsencrypt
1. 映射 生成key pem
2. ![image-20230625200720865](/Users/bytedance/Library/Application Support/typora-user-images/image-20230625200720865.png)
acme.sh --issue --dns dns_namesilo --dnssleep 900 -d erichen.top -d *.erichen.top --debug 
1. 绑定到nginx的相关folder
acme.sh --install-cert -d erichen.top \
--key-file       /home/nginxWebUI/cert/erichen.top/erichen.top.key \
--fullchain-file /home/nginxWebUI/cert/erichen.top/erichen.top.cer
最后进行映射 反向代理
# docker-compose 内容
指定本地loopback和映射端口
docker run -d -p 127.0.0.1:31000:3000/tcp \
   -e OPENAI_API_KEY="xx" \
   -e CODE="xx" \
   yidadaa/chatgpt-next-web