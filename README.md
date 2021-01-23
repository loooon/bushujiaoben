# bushujiaoben
常用脚本
1.java程序部署脚本
> 后台运行：nohup java -jar demo-0.0.1-SNAPSHOT.jar  > log.file  2>&1 &

---
···
start.sh
#!/bin/bash 
 
export CALLCENTER=word-0.0.1-SNAPSHOT.jar
 
export CALLCENTER_port=8888
 
export dir=/root
 
## BEGIN--CALLCENTER-----------------------------------------------------------------------------------------------------------------
P_ID=`ps -ef | grep -w $CALLCENTER_port | grep -v "grep" | awk '{print $2}'`
if [ "$P_ID" == "" ]; then
	echo "===CALLCENTER process not exists or stop success"
else
	kill -9 $P_ID
	echo "CALLCENTER killed success"
fi
 
echo "===CALLCENTER stop success==="
## 启动CALLCENTER
echo "--------CALLCENTER start--------------"
 
nohup java -jar $dir/$CALLCENTER   > $dir/nohup.out 2>&1 &
tail -f $dir/nohup.out
···
---

stop.sh
···
#!/bin/bash

 
export CALLCENTER=word-0.0.1-SNAPSHOT.jar
 
export CALLCENTER_port=8888
 
export dir=/root
 
## BEGIN--CALLCENTER-----------------------------------------------------------------------------------------------------------------
P_ID=`ps -ef | grep -w $CALLCENTER_port | grep -v "grep" | awk '{print $2}'`
if [ "$P_ID" == "" ]; then
	echo "===CALLCENTER process not exists or stop success"
else
	kill -9 $P_ID
	echo "CALLCENTER killed success"
fi
···
