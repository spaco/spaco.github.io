## 什么是Grafana？

Grafana是开源的可视化和分析软件。它使您可以查询，可视化，警报和浏览指标，无论它们存储在哪里。它为您提供了将时间序列数据库（TSDB）数据转换为精美的图形和可视化效果的工具。



## 安装方式

安装地址：https://grafana.com/docs/grafana/latest/installation/


## 安装

```bash
brew install grafana
```

```bash
# 默认配置文件位置 注意：必须重新启动Grafana才能使所有配置更改生效。
/usr/local/etc/grafana/grafana.ini
 
# 默认端口
3000

# 默认用户名和密码
admin admin
```



## 启动

```bash
brew services start grafana
```



## 测试

```bash
浏览器打开: 127.0.0.1:3000
```



## 相关命令

```bash
// start service
brew services start grafana
// stop service
brew services stop grafana
```

