## 安装方式

安装地址 ：https://prometheus.io/download/

- 预编译的二进制文件
- docker
- brew
- 源代码

## 安装

```bash
brew install prometheus
```

## 启动

```bash
brew services start prometheus
```

```bash
# 默认配置文件地址
/usr/local/etc/prometheus.yml
```



## 测试

```bash
浏览器打开: localhost:9090
```



## 结合 node_exporter (机器指标导出器)

### 安装 node_exporter

```bash
brew install node_exporter
```

### 启动

```bash
brew services start node_exporter
```

### 测试

```bash
浏览器打开:localhost:9100
```

### prometheus 集成 node_exporter

```bash
vim /usr/local/etc/prometheus.yml

# 加入如下配置项 采集node exporter监控数据
  - job_name: "node_exporter"
    static_configs:
    - targets: ["localhost:9100"]
```

### 重启prometheus

```bash
brew services restart prometheus
```

稍过几秒, prometheus 可视化可以看到收集到的机器节点信息

### 常用命令

```bash
# 查看brew service 状态
brew services list

# 停止 node_exporter service
brew services stop node_exporter
```



