#### To upload the file inside the folder "assets2" to S3 bucket :

````
[root@ip-172-31-44-112 ~]# aws s3 cp assets2 s3://s3uploadbucket1 --recursive 
upload: assets2/temp2.txt to s3://s3uploadbucket1/temp2.txt
````

#### To upload the full folder "assets2" in to the S3 bucket :
````
[root@ip-172-31-44-112 ~]# aws s3 cp assets s3://s3uploadbucket1/assets/ --recursive
upload: assets/temp.log to s3://s3uploadbucket1/assets/temp.log

[root@ip-172-31-44-112 ~]# aws s3 ls s3://s3uploadbucket1
                           PRE assets/
2019-11-24 15:30:09          0 temp2.txt
````
#### Deleting a particular object / file in the S3 bucket :
````
root@ip-172-31-44-112 ~]# aws s3 rm s3://s3uploadbucket1/assets/temp.log
delete: s3://s3uploadbucket1/assets/temp.log
````
#### Filter the uploaded files based on certain critera (exclude certain files). It will be very helpful if you have mixed set of files in your dirctory which you wish to upload. If we don't want to upload the .log file
```
[root@ip-172-31-44-112 ~]# aws s3 cp assets3 s3://s3uploadbucket1/assets3/ --recursive --exclude *.log 
upload: assets3/temp.jpg to s3://s3uploadbucket1/assets3/temp.jpg
upload: assets3/temp.txt to s3://s3uploadbucket1/assets3/temp.txt
```
#### Include all the temp* files but exclude the temp.log file :
```
[root@ip-172-31-44-112 ~]# aws s3 cp assets3 s3://s3uploadbucket1/assets3/ --recursive --include temp* --exclude *.log 
upload: assets3/temp.jpg to s3://s3uploadbucket1/assets3/temp.jpg
upload: assets3/temp.txt to s3://s3uploadbucket1/assets3/temp.txt
```
#### Sync local folder with s3 :
```
[root@ip-172-31-44-112 scripts]# aws s3 sync .  s3://s3uploadbucket1/scripts/
upload: ./game4.txt to s3://s3uploadbucket1/scripts/game4.txt
upload: ./game5.ps1 to s3://s3uploadbucket1/scripts/game5.ps1
upload: ./game.txt to s3://s3uploadbucket1/scripts/game.txt
upload: ./game6.ps1 to s3://s3uploadbucket1/scripts/game6.ps1
upload: ./game.ps1 to s3://s3uploadbucket1/scripts/game.ps1
```
#### I have now deleted the file game6.ps1 on the scripts folder in my local machine. Sync local folder with s3 with deletion :
````
[root@ip-172-31-44-112 scripts]# aws s3 sync .  s3://s3uploadbucket1/scripts/ --delete
delete: s3://s3uploadbucket1/scripts/game6.ps1
````
#### You can see that the file is also deleted in the S3 bucket to keept it in sync
 
 #### To sync S3 bucket with local folder :
 ```
 [root@ip-172-31-44-112 scripts4]# aws s3 sync s3://s3uploadbucket1/asset .
download: s3://s3uploadbucket1/asset/test1.txt to ./test1.txt   
```
#### To sync S3 bucket with local folder with delete :
```
[root@ip-172-31-44-112 scripts4]# aws s3 sync s3://s3uploadbucket1/asset . --delete
delete: ./game.jpg
delete: ./game.ps1                                            
delete: ./game.ps2                                            
delete: ./game.ps3                                            
delete: ./game.txt                                            
delete: ./test1.txt  
```


