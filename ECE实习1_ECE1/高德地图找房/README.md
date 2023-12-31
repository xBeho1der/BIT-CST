# 高德地图找房

***
**运行方法**  

- **由于数据较多，需要等所有房源信息加载完毕之后，方可进行路线规划**
- 终端进入文件夹后，输入 python -m http.server 8080启动服务器
- 在浏览器中输入 <http://localhost:8080> 即可查看效果
- 示例图
- ![avatar](/ECE实习1_ECE1\高德地图找房\示例图.png)

***

## 项目文件介绍

- 示例图.png  
  - 用于在README.md文件中展示运行效果
- data_download.py  
  - 用于从链家网站进行数据爬取与数据清洗，并存入infoList.csv文件中
- infoList.csv
  - 用于存储从链家网站上爬取房源信息
- index.html
  - html页面源代码
- server.py
  - 用于搭建服务器
- requirements.txt
  - 项目依赖包
- 实践概述.md
- README.md
  - 项目说明文档

## 项目功能介绍

### 数据爬取与数据清洗

- 本项目选择从链家中爬取北京范围内租房数据
- 爬取数据范围为1-30页
- 爬取时利用多线程爬取，加快爬虫速度
- 利用xpath定位器，定位到不同等元素，并进行数据清洗，保留自己需要的成分
- 将爬取下来的数据写入到无头文件infoList.csv文件中，第一列为房源信息，第二列为房源所属区块信息

### 前端功能介绍

- 在原有基础上，更改了csv文件的接口，能够显示当前区块内所有的房源具体信息。
