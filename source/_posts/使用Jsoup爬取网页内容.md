---
layout: post
title:  使用Jsoup爬取网页内容
date:   2017-12-18 00:00:00 +0800
categories: 技术
tags:
  - Jsoup
---

### 一、Jsoup相关资料
- [Jsoup官网](https://jsoup.org/)
- [中文使用文档](http://www.open-open.com/jsoup/)


### 二、使用方法
1. 心得
    * Jsoup适合用来解析静态网页(目前我也只用来解析静态网页)，稍微懂一些Java基本就能无障碍使用Jsoup来解析网页。
    * Jsoup的API简单易于理解，上手快，学习成本低。
    * 如果大家有好的办法或者工具可以与Jsoup结合起来解析动态网页，请一定要告诉我！

2. Jsoup其实就是把网页读取为一个HTML文档，然后根据文档内的标签来解析数据。
    * 首先需要读取这个文档：
    ```
            String url = "http://ccc.spdb.com.cn/miniSite/Platamex2017/1_4_list.shtml";
            Document document = Jsoup.connect(url).get();
    ```
    * 使用DOM方法来遍历一个文档
    > http://www.open-open.com/jsoup/dom-navigation.htm
    ```
       Element ele = document.getElementById("content");
            Elements elements = ele.getElementsByClass("addlist");
            for (Element element : elements) {
                Element province = element.select("h3").first();
                Elements tbody = element.selectFirst("table").selectFirst("tbody").select("tr");
                for (int i = 1; i < tbody.size(); i++) {
                    AreaCode areaCode = new AreaCode();
                    areaCode.province = province.text();
                    Elements tds = tbody.get(i).select("td");
                    areaCode.code = tds.get(0).text();
                    areaCode.city = tds.get(1).text();
                    System.out.println("-----" + areaCode.toString());
                }
            }
    ```
    * 使用选择器语法来查找元素
    > 这个翻译里面介绍的非常详细，我就不画蛇添足了
    > http://www.open-open.com/jsoup/selector-syntax.htm

3. 代码
    * 下面一段是我用来解析一个网页，用来给前阵子写的微信小程序获取数据。
    * 全部代码已经上传到[github]（https://github.com/chenwansong/JsopDemo）
    ```
       public static void main(String[] args) throws IOException {

            String url = "http://ccc.spdb.com.cn/miniSite/Platamex2017/1_4_list.shtml";
            Document document = Jsoup.connect(url).get();


            Element body = document.body();
            Element tbody = body.selectFirst("tbody");
            Elements tr = tbody.select("tr");

            for (int i = 2; i < tr.size(); i++) {

                SpdbHotelBean spdbHotelBean = new SpdbHotelBean();
                Elements tds = tr.get(i).select("td");

                spdbHotelBean.country = tds.get(0).text();
                spdbHotelBean.city = tds.get(1).text();
                spdbHotelBean.hotelNameCN = tds.get(2).text();
                spdbHotelBean.hotelNameEN = tds.get(3).text();
                spdbHotelBean.type = tds.get(4).text();
                spdbHotelBean.breakfast = tds.get(5).text();
                spdbHotelBean.address = tds.get(6).text();
                spdbHotelBean.closeDay = tds.get(7).text();

                System.out.println("-----" + spdbHotelBean.hotelNameCN);

            }
        }
    ```