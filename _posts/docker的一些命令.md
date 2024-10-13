---
title: docker如何改变环境变量
top: false
cover: false
toc: true
mathjax: true
comments: true
date: 2024-03-17 21:38:07
tags:
password:
summary:
categories:
- [study]
- [tech]
math:
---

## 命令&步骤

1. 关闭docker 服务

```bash
# systemctl stop docker 
```

2.查看环境变量
```bash
# docker exec -it [container-id] env
```

- 查看Docker Root Dir: /apps/docker
```bash
# docker info
```

- 找到容器短id，再docker inspect [短id], 获取容器的长id：container-id

```bash
# dokcer ps
```



或者  
```bash
# vim var/lib/docker/containers/[container-id]/config.json
```

3.修改环境变量


修改/var/lib/docker/containers/[container-id]/config.v2.json里对应的环境变量

- 修改容器配置信息
```bash
# vim var/lib/docker/containers/[container-id]/config.v2.json  
```

4.然后重启docker服务
  
```bash
# systemctl daemon-reload
# systemctl restart docker  
```


