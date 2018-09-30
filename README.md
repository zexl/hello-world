# hello-world
#!/usr/bin/env python 
# -*- coding:utf-8 -*-

import fileinput

Dir="/home/yw_opert/_zzx/ceph/"
Filename="new_image_20180918.txt"

pool={"GZNXG0100":1, "GZNXG0101":2, "GZNXG0102":3, "GZNXG0103":4, "GZNXG0104":5, "GZNXG0105":6, "GZNXG0106":7, "GZNXG0107":8}

insert="insert into rf_image " \
       "(image_id,disk_id,image_name,bind_status,fault_status,status,enable_status,pool_id,creater,create_time)"

file = open(Dir+Filename,'r')
for (num,value) in enumerate(file):
    imageid=num+1
    line = value.strip('\n').split('/')
    poolid=pool[line[0]]
    imagename=line[1]
    #insert into rf_image
    # (image_id,disk_id,image_name,bind_status,fault_status,status,enable_status,pool_id,creater,create_time)
    #  values('1','1','GZNXG0100000001','0','0','1','1','1','zzx',now());
    print(insert+"values(nextval('seq_rf_image')"+",'1','"+imagename+"','0','0','1','1','"+str(poolid)+"','zzx',now());")
file.close()
