## 装新ubuntu ##
1. DHCP-->Manual
2. sudo apt-get install openssh-server
3. sudo ufw disabled/enabled
	1. sudo ufw status 
4. sudo apt-get install vim/git
5. sh Anaconda-xxxx.sh
6. source ~/.bashrc
7. conda list
	1. pip install --upgrade pip
8. pip install xgboost
9. sudo apt-get install cmake/gcc/g++  (--version)
10. sudo git clone https://github.com/aksnzhy/xlearn.git
11. head/tail -n 10 /etc/profile
12. wc -l train.txt
13. sudo apt-get install mysql-server
 apt-get isntall mysql-client
 sudo apt-get install libmysqlclient-dev
mysql -u root -p (root)
14. 复制：1,2 co 3(1&2行复制到2之后)
(n)yy -> p
15. scp xxx-xxx.xml ts@192.168.0.1:/home/ts
16. hosts文件生效
16.1 sudo /etc/init.d/networking restart
16.2 sudo /etc/init.d/dns-clean start
17. wc -lwc user_data
18. cat ad_operation.dat |head -n 30 | tail -n -20 前20行的后10行，即10-30
19. cat ad_operation.dat |tail -n +10 | head -n 20 10行开始显示20行，即10-30
20. sed -n '10,30p' user_data 直接查看10-30行