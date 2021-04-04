# Enable jenkins to run sudo commands without password

Add below lines to sudoers file

`$ sudo visudo`

```
ALL     ALL=(ALL:ALL) ALL

jenkins ALL = NOPASSWD: /usr/bin/docker
```




# Jenkins Freestyle job to create docker iamge
* Execute shell :
``` mvn package
    cp <path_to_generated_addressbook.war_From above command> .
    echo "FROM tomcat" > Dockerfile
    ADD "addressbook.war /usr/local/tomcat/webapps/addresssbook.war" >> Dockerfile
    docker build -t addressbook:${BUILD_NUMBER} .
 ```
