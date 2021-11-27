# 常用指令

1. one.sh **-b** 2 ~.txt: 可以使用 b 来直接生成报告，无需 gui, 2 表示两种情况。
2. one.sh -b 1:6 ~.txt :每个节点跑一次，6 \* 1
3. one.sh -b 1:60 ~.txt 每个节点跑 10 次 6 \* 10

# 参数解释
## WIFI , bluetooth Interface
### WiFi Interface
1. // 应该还是SimpleBroadcastInterface , 速度和范围要和蓝牙区别开（蓝牙6m）
wifiInterface.type = SimpleBroadcastInterface
wifiInterface.transmitSpeed = 7.5M
wifiInterface.transmitRange = 50

2. //调用时使用 ,直接加姓名
Group.interface1 = wifiInterface

## group

1. Scenario.name = [\name1;\name2;\name3;\name4;\name5\] : ;\,最后无“；"
2. Scenario.endTime = 36000
3. Scenario.nrofHostGroups =3
   // 3 node groups
4. Group.router = [\
                 SprayAndFocusRouter;\
                 SprayAndFocusRouter;\
                 SprayAndFocusRouter;\
                 SprayAndFocusRouter;\
                 ProphetRouter;\
                 ProphetRouter;\
                 ProphetRouter;\
                 ProphetRouter\
                ]
   //可能可以同时跑两个协议
   //有严格的格式限制  ;\ ;\
5. Group.bufferSize = [5M;10M;20M]
   // buffer Size

6. // 固定节点时记得添加节点位置。
   Group1.movementModel = **StationaryMovement **
   Group1.nodeLocation = 2000, 2000 

   Group2.movementModel = ShortestPathMapBasedMovement

   Group1.groupID = hq
   Group1.nrofHosts = 1
   Group1.movementModel = StationaryMovement
   Group1.nodeLocation = 2000, 2000
   // 固定节点

7. Group2.nrofHosts = 10
   //设置每个组的节点个数
   //可以单独设置
8. Group2.okMaps = 1
   //在地图上走
9. Group2.speed = 8.9, 13.4
   // 速度的范围

## Event

1. Event1.hosts 0,5
   //range of source and destination address
2. Event1.hosts = 1,3,4,5,6 ： destnation 接收的序号
   A. =[1,3,4;7,8,9]: one. bat -b 2 defaults.txt ,first report 1,3,4 will be random ; 7,8,9 report will be random used
   B. 如果只设置了 hosts，de 和 so 为随机。
   C. 如果都设置，那么在集合中随机选择。

3. Event1.hosts 6,10 ： destnation 接收的序号
4. Report.reportDir = [reports/1 ; reports/2 ; reports/3]
5. Events.prefix = 0
   // ?

## Reports

1. Report.nrofRepeots =1
   //?
2. Report.reportDir= reports/demo/
   // 报告位置
3. Report.reprort1 = MessageStatsReport
   //MessageStatsReport , 报告类型

## Serveral Reports to generate

1. Report.nrofReports = 8 : 生成报告数量

Report.report8 = InterContactTimesReport
Report.report7 = PriorityMessageStatsReport
Report.report1 = CongestionCountsReport
Report.report2 = CongestionTimesReport
Report.report3 = CongestionLevelsReport
Report.report4 = ContactTimesReport
Report.report5 = TotalContactTimeReport
Report.report6 = EncountersVSUniqueEncountersReport

MessageStatsReport

## Network interface

1. tansmitSpeed:(bytes per second)
2. tansmitRange:(meters)
3. btInterface.type = simle..
   //2M = 250k
   btInterface.transmitSpeed=250k
   btInterface.transmitRange=20

## Node groups and common settings

1. Scenario.nrofHostGroups = 6
2. Group.bufferSize= [5M;25M;50M]

## Map

### Movement model settings
MovementModel.worldSize = 4500, 3400
MovementModel.rngSeed = [1;2;0;4;5;2]

### Map based movement settings
MapBasedMovement.nrofMapFiles = 3
MapBasedMovement.mapFile1 = data/roads.wkt
MapBasedMovement.mapFile2 = data/main_roads.wkt
MapBasedMovement.mapFile3 = data/pedestrian_paths.wkt

### Optimisation Settings
Optimization.cellSizeMult = 1
Optimization.randomizeUpdateOrder = true

# Note

1. 随机设置 hosts 与 tohosts 的参数
