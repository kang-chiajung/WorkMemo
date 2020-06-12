# MQ 
* 測試URL
  * [MQ UAT](https://staffuat.taiwanlife.com/MQTs/MQTs101.asp?trgcode=300&pgmname=INT340C&inputparm=0000495540403086%2CAJSD2184) staffuat.taiwanlife.com

  * [MQ Prod](https://staff.taiwanlife.com/MQTs/MQTs101.asp?trgcode=300&pgmname=INT340C&inputparm=0000495540403086,CAJSD2184) staff.taiwanlife.com

  * [MQ UAT](http://10.1.244.54/MQTs/MQTs101.asp?trgcode=300&pgmname=INT340C&inputparm=0000495540403086,CAJSD2184) 10.1.244.54 New

  * [MQ Prod](http://10.174.5.118/MQTs/MQTs101.asp?trgcode=300&pgmname=INT340C&inputparm=0000495540403086,CAJSD2184) 10.174.5.118

* 環境變數
  * UAT
    * 變數名稱: _MQSERVER_
    * 變數值: _SYSTEM.ADMIN.SVRCONN/TCP/10.174.4.1_

  * PRD
    * 變數名稱: _MQSERVER_
    * 變數值: _SYSTEM.ADMIN.SVRCONN/TCP/10.174.3.18_

* 防火牆規則 
   * 10.174.4.1(MISTEST1) Port:1414,1415
   * 10.174.3.18 Port:1414,1415

# ATM

## 環境

* DEV
	* DEVW16019(10.1.248.24)    
   
* UAT
   * AP：mistest1 (10.174.4.1 | 10.174.4.20(主要))
   * Url：http://customeruat.ctbclife.com/svcatm/CTLATMService.asmx
   * DB
      >  mistest1 10.174.4.1
      >  mistest1 10.174.4.1
      >  mistest1 10.174.4.1
        
   * ESB 
      >  175.184.247.92      
      >  175,184.247.93
   * MMAS
     > 175.184.247.72:24114
   * 憑證中心
     > 10.174.4.4(mistest3)
* PROD
   * 伺服器:WEBSVR4
   * 伺服器ip:10.174.3.60
   * url:https://customer.ctbclife.com/svcatm/CTLATMService.asmx
   * DB:missvr3(10.174.3.156)
   * 憑證中心
     > missvr29(10.174.3.34)
 * 其它  
 # 立即繳系統
## 環境

* DEV
   * 伺服器:DEVW16019
   
* UAT
   * 伺服器:10.1.249.48(UATW16044)
   * url:https://uat.taiwanlife.com/
   * 資料庫:UATW16008
   * 資料庫ip:10.1.249.42
   * 測試帳號
      * R222412421    WS*****
      * N220123080    12345678a  
* PROD
   * 伺服器:10.1.2.207(HQ0W16100)
   * url:https://www.taiwanlife.com/ 
   * 資料庫:HQ0W16025
   * 資料庫ip:10.1.101.53


## 移機Memo
1. HOST:UATW16075(10.1.244.55)
 申請內部IP需在244網段
2. 於該主機建置IIS站台
 站主機上會有兩個站台
	1. atmsvrdev.taiwanlife.com(SSL)
	2. 新申請之ip(內部網用)

1. 於AP主機：DEVW16004，安裝IBM Access for Windows
2. 於AP主機：UATW16029，安裝IBM Access for Windows
3. 於AP主機：HQ0W16162，安裝IBM Access for Windows
4. 於AP主機上安裝BinaryTran加解密程式(Interop.BinaryTran.dll )


# 員工網
Driver={SQL Server};Server=olap;uid=webdefault;
pwd=webdefault;database=metlife;
*  UAT UATW16028(4.188) 
*  Prod WEBSVR3

# TLS 1.2昇級

申請另一組內部ip供HQ0W16162(10.174.5.173)使用，配發IP：10.174.5.118
申請另一組內部ip供UATW16075(10.1.244.55)使用，配發IP：10.1.244.54
申請另一組內部ip供DEVW16019(10.1.248.24)使用，配發IP：10.1.248.56

* PROD
   * 10.174.5.173|118 
   * Waf IP： 172.16.100.165 
   * Public IP：218.32.204.90
* UAT 
   * 10.1.244.55|54 
   * Waf IP：172.16.102.165 
   * Public IP：218.32.204.91
* DEV 
   * 10.1.248.24|56 


## [MMAS BATCH]
* UAT	MISTEST1
* PROD	MISSVR9

## [其它]

1. 移機memo

D:\Document\My Request\dotNet系統升級&主機轉移
Step 1.Clone主機
	主機來源：UATW16028(4.188)執行需關機進行，進行前請告知康家榮、俊淵
	
Step 2.關閉準備覆蓋的主機
     UATW16075(10.1.244.55)
	 
Step 3 Clone暫存主機
	待IT內部測試沒問題後再執行Step4
	
Step 4 覆蓋目標主機
	將Clone出來的主機覆蓋至UATW16075
	覆蓋後以下需還原設置
		IP:10.1.244.55*,10.1.244.54
		Pulice IP：218.32.204.91
		WAF VS IP：172.16.100.165
		Host Name：UATW16075
		其它：機碼等…
		
*ATMSVR站台是2.0的
 把加解密元件移掉


中信銀atm 立即繳 訪談：2020/7/1	uat:2020/11/16

# Memo

## 新主機
* HQ0W16161(10.174.5.172)		IBON
* HQ0W16162(10.174.5.173|118)		中信ATM
* UATW16075(10.1.244.55)		IBON,中信ATM,立即繳
* DEVW16019(10.1.248.24)       中信ATM DEV

## 指令
Net Use
``` cmd 	
	net use z: \\10.174.3.12\website A12345!! /user:ap_staff
	net use y: \\10.174.3.14\website A12345!! /user:ap_staff
	net use x: \\10.174.4.1\website A12345!! /user:ap_staff
   net use w: \\10.174.4.187\website
   net use w: \\10.1.244.55\webSite
```
``` sql
ATMSvc_SystemRule] set  [SysMaintainBDate]=convert(datetime,'2020-5-22 09:00.00'),[SysMaintainEDate]=convert(datetime,'2020-5-22 12:00.00') ,[SysMaintainEnable]='Y',[DayMaintainEnable]='N'
```  	
## 常用員編

* 蔡承昌：003646
* 查員編 [IT服務網](http://staff.taiwanlife.com/ad/it/service.asp?t_type=4#)
http://webapp2uat.ctbclife.com:8080/CtcbSign/SignServlet2"
[1]:https://markdown.tw/

> 註:5/22~5/24 因LSP異常故筆數僅22當日有2筆 

## 常用路徑
\\hq0w16063\department\資訊處\資訊三部\資訊三部公用區\15.健康指標及MBO\02.MBO\2020年MBO\二科\2020MBO執行時程規劃_二科四組.xlsx


