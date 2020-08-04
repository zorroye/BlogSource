---
title: CCNA第七章
tags:
  - ccna
categories:
  - Network
  - cisco
id: '202'
abbrlink: 4214236176
date: 2012-09-14 15:22:00
---

EIGRP  

> 能同时提供多种网络层协议的路由选择。  
> EIGRP通过hello包建立邻居关系。  
> 
> > 邻居关系的三个条件：  
> 
> > > 收到hello包或者ack  
> > > 相同的as号  
> > > 相同的度量  
> > > 
> > > > 度量包括：  
> > > > 
> > > > > 带宽（默认）  
> > > > > 延迟（默认）  
> > > > > 负载  
> > > > > 可靠性  
> > > > > MTU尺寸  
> > 
> > 建立邻居关系时，会发送整个路由表。之后只发送变化的部分  
> > EIGRP通过RTP来传输，RTP是先用组播更新，再和没联系到的用单播更新。16次单播后宣告失效。  
> > 组播地址：224.0.0.10  
> 
> EIGRP跳数：255  
> EIGRP有3张表：邻居表、拓扑表、路由表  
> EIGRP没有像ospf一样有区域0要求。  
> 
> > EIGRP分为内部路由(AD=90)和外部路由(AD=170)  
> 
> EIGRP和RIPv2支持不连续子网的自动汇总，所以默认时图7.1是不通的。  
> 
> > 因为172.16.10.0/24和172.16.20.0/24多汇总成172.16.0.0/16，所以路由器就把数据发回原路了。  
> >   
> 
> EIGRP相关命令  
> 
> > > (config)#router eigrp 10  
> > > (config-router)#network 172.16.0.0  
> > > (config-router)#network 10.0.0.0  
> 
> > 其他还有  
> 
> > > (config-router)#maximum-paths 6                   最大负载均衡链路支持6条  
> > > (config-router)#metric maximum-hops 255     最大跳数支持255  
> > > (config-router)#passive-interface s0/1             不发送或接收路由信息  
> > > (config-router)#no auto-summary                   不自动汇总  
> > 
> > 再发布命令  
> > 
> > > (config)#router eigrp 10  
> > > (config-router)#redistribute rip metric 10000000 20000 255 1 1500  
> > > (config)#router rip  
> > > (config-router)#redistribute eigrp 10 metric 1  
> > 
> > 验证命令  
> > 
> > > #show ip eitrp neighbors  
> > > #show ip eitrp topology  
> > > #show ip route  
> > > #show ip route eigrp                只显示eigrp项目  
> > 
> > 故障诊断命令  
> > 
> > > debug eigrp packet                  显示hello包数据  
> > > debug ip eigrp notification        网络变化(出错)时，显示变化的信息  
> > 
> > >   

OSPF  

> ospf一定要规定一个主干区域（区域0），然后其他区域必须有一个接口和主干区域链接。  
> 
> > ospf只能在代价相同的链路上实现负载均衡，而eigrp可以在不同代价的链路上实现负载均衡  
> > 路由器最好配置环回接口lo。这样就可以指定DB路由器  
> > 
> > > 配置命令：  
> > > (config)#int loopback 0  
> > > (config-if)#ip address 172.16.10.1 255.255.255.255    要保证每个路由器的环回接口多是独立网段。  

  

> 邻居和邻接  
> 
> > 邻居：只要2个路由器有连接，就是邻居关系。  
> > 
> > >   hello包发送地址：224.0.0.5  
> > 
> > 邻接：建立邻居关系后，若发DBD包(用于选DB)，则选好DB后就表明建立了邻接关系。  
> > 
> > >   建立邻接关系后，发LSA(链路状态通告)，交换路由更新数据，共享路由信息。  
> > >   备注：只有DR和BDR和Dother建立邻接关系，Dother之间不能建链接关系，只能建邻居关系。  
> > >   参考：[OSPF的邻接关系是怎么建立成功的](http://www.2cto.com/net/201208/145681.html)  
> > >             [OSPF两台路由器之间建立邻接关系过程](http://cisco.chinaitlab.com/OSPF/740073.html)
> 
>   
> OSPF命令  
> 
> > > (config)#router ospf 12         #12只是ospf的标识，跟区域没有关系，随便标多可以  
> > > (config-router)#network 192.168.10.0    0.0.0.255          area 0    
> > >                                                            子网掩码反码      设置区域0  
> > >   
> > 
> > 在发布命令  
> > 
> > > (config)#router eigrp 10  
> > > (config-router)#ip summary-address eigrp 10 192.168.10.60 255.255.255.224  
> > > (config)#router ospf 1  
> > > (config-router)#area 1 range 192.168.10.64 255.255.255.224  
> > >   
> 
> > 查看命令  
> > 
> > > show ip ospf                          ospf相关信息  
> > > show ip ospf interface f0/0    某个接口的ospf信息  
> > > show ip ospf database          查看路由器各个接口的ID和相邻路由器的ID  
> > > show ip ospf neighbor           查看邻居和邻接信息，这样DR和BDR也会显示出来  
> > 
> > 调试命令  
> > 
> > > debug ip ospf packet              显示hello包的收发  
> > > debug ip ospf hello                 显示hello包的收发，比上面的详细  
> > > debug ip ospf adj                    用于查看选举DR、BDR过程  
> 
>   
> 
> > DR的选举  
> > 
> > > DR的选举主要看优先级和IP的大小  
> > > 优先级：  
> > > 
> > > > 默认为1，越大就越能当DR，0就只能当Dother  
> > > > (config-if)#ip ospf priority 0  
> > > 
> > > IP的大小可以通过lo来设置  
> > >   

补充及实验：待续