## ad_static_feature ##
72w条记录，7个属性
 |ad_id | timestamp | account_id | product_id | product_type | profess_id | size 
|-----|-----|-----|-----|-----|-----|
|1 |2 | 3| 4 | 5 | 6 | 7 |

读文件，转成csv格式
    #out转csv文件
	import numpy as np
	import pandas as pd
	out_data = list()
	file = open("G:\\tiansir\\dataset\\txCTR\\testA\\ad_static_feature.out",'r')
	for line in file:
	    tmp_line = line.replace(',','_')
	    tmp_line = tmp_line.replace('\t\n','\n')
	    out_data.append(tmp_line.replace('\t',','))
	#    out_data.append(line)
	print(out_data[:3])
	file.close()
	print('SUCCEED')

	file = open("G:\\tiansir\\dataset\\txCTR\\testA\\ad_static_feature.csv",'w')
	for row in out_data:
	    file.write(row)
	file.close()
	print('SUCCEED')