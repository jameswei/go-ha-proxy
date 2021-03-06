# Introduction:
  This go-ha-proxy is simple reverse proxy using Golang.
  
## Version:

version:0.0.2

1.support TCP proxy and you can use round-robin or source mode to HA.

2.health mode supported.

3.monitor server supported.

    http://localip:8080
     
4.command line params supported.

    ./GoHAProxy -help

5.auto reload config file.When file changed.GoHAProxy will auto reloaded.

6.balance type:RoundRobin,Source,Weight,LeastConn

    RoundRobin:auto RR
    
    Source:use source ip to balance service.
    
    Weight:Use weight setting to balance.
    
    LeastConn:Search least conn server to balance server.

  
## Install:
```sh
  go get github.com/matishsiao/GoHAProxy
  go test
  go build
```

## Configuration format:

configs in config.json

ProxyList:

      Proxy:

      Src:source ip or domain.

      SrcPort:source port.

      Mode:tcp,health

      Type:RoundRobin,Source,Weight,LeastConn
   
      KeepAlive:1 second (keep alive server connection.Set zero will allways keep alive.)

      CheckTime:1 second (check health,default value:5 seconds.)

      DstList:Destination server list
      
         DstNode:

         Name:server name

         Dst:server ip or domain
 
         DstPort:destination port

         Weight:not use(when Weight HA mode done,will use this arg)

         Check:true or false(check node server health.If you set false,the GoHAProxy will set this server allways health.)

## Configuration example:
		{"Configs": 
		    {       
		       "ProxyList":
		       [
		               {
		                       "Src": "",
		                       "SrcPort": "9000",
		                       "Mode":"tcp",
		                       "Type":"RoundRobin",
		                       "KeepAlive":60,
		                       "CheckTime":1,                       
		                       "DstList": 
		                       [
			                       {
			                       	 "Name":"MatisVM",
			                         "Dst":"10.7.9.59",
			                         "DstPort": "80",
			                         "Weight":1,
			                         "Check":true
			                       },
			                       {
			                         "Name":"Outsite",
			                         "Dst":"www.yahoo.com",
			                         "DstPort": "80",
			                         "Weight":2,
			                         "Check":true
			                       },
			                       {
			                       	 "Name":"DemoVM",
			                         "Dst":"10.7.9.53",
			                         "DstPort": "80",
			                         "Weight":3,
			                         "Check":true
			                       }
		                       ]
		               },
		               {
		                       "Src": "",
		                       "SrcPort": "9001",
		                       "Mode":"tcp",
		                       "Type":"Source",
		                       "KeepAlive":60,
		                       "CheckTime":1,                       
		                       "DstList": 
		                       [
			                       {
			                       	 "Name":"MatisVM",
			                         "Dst":"10.7.9.59",
			                         "DstPort": "80",
			                         "Weight":1,
			                         "Check":true
			                       },
			                       {
			                         "Name":"Outsite",
			                         "Dst":"www.yahoo.com",
			                         "DstPort": "80",
			                         "Weight":2,
			                         "Check":true
			                       },
			                       {
			                       	 "Name":"DemoVM",
			                         "Dst":"10.7.9.53",
			                         "DstPort": "80",
			                         "Weight":3,
			                         "Check":true
			                       }
		                       ]
		               }
		       ]
		    }
		}


##License and Copyright
This software is Copyright 2012-2014 Matis Hsiao.
