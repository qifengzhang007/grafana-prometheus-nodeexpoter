# grafana-prometheus-node-expoter

#### 1.前言  
> 服务器性能监控集成环境  
grafana + prometheus + node-expoter



####  2.三个核心角色介绍  
 - 1.node_exporter:   
   在 9100 端口启动一个服务，自身抓取linux系统底层的运行状态数据，例如：cpu状态、内存占用、磁盘占用、网络传输状态等，等待其他上层服务软件抓取
 
- 2.prometheus :   
  从 部署在不同服务器的多个 node_exporter 提供的服务端口 9100 主动获取数据，存储在自带的数据库 TSDB.  
  
 - 3.grafana :  
   提供可登陆的数据展示系统，从 prometheus 提供的接口获取数据，可视化呈现服务器性能指标。  
   
###  3.三个核心角色配置   
```code  

#1.node_exporter 
    如果服务器比较多，可以屏蔽 docker-compose.yml 中的 grafana、prometheus 键底下的全部，只保留 node_exporter  在其他服务器部署


# 2.prometheus

    参见 prometheus_config/prometheus.yml 文件，有详细的配置示例


# 3.grafana
    # 必须设置权限，否则 grafana 启动报错
    为挂载的数据目录设置权限，相关的目录请参考 grafana 配置文件的 volumes 选项指定的路径
    chmod  777  -R  /home/data/project2021/grafana

```

### 4.快速部署本项目
```code   
    #  1. 安装 docker 环境，请自行百度搜索。
    #  2. 安装 docker-compose，参考：
    #  3.下载/克隆 本项目到你服务器的某个位置，在 docker-compose.yml 同目录执行  docker-compose  up -d 即可
```
 启动效果图
 ![效果图](https://www.ginskeleton.com/images/gpn.png)

###  5.可能遇到的问题  
```code  

    1.采集不到数据，grafana界面无数据  
     如果是云服务器，内网地址采集不到数据，请换成外网ip尝试.  
     
     2.其他问题  
    请在本项目仓库直接提 issue  
```


### 6.最终效果图  
![效果图](https://www.ginskeleton.com/images/linux1.png)  
![效果图](https://www.ginskeleton.com/images/linux2.png)  