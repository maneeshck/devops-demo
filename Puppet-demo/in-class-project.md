# Generate addressbook.war
``` bash
apt-get install maven
git clone
cd addressbook
mvn package
```

# Install tomcat module
``` bash
cd  /etc/puppetlabs/code/environments/production/modules
puppet module install puppetlabs-tomcat
cp /root/addressbook/addressbook_main/target/addressbook.war /etc/puppetlabs/code/environments/production/modules/tomcat/files

```

# setup instance

``` rb
tomcat::install { '/opt/tomcat9':
  source_url => 'https://www.apache.org/dist/tomcat/tomcat-9/v9.0.44/bin/apache-tomcat-9.0.44.tar.gz'
}
tomcat::instance { 'default':
  catalina_home => '/opt/tomcat9',
}
```

# deploy war file
```rb
tomcat::war { 'sample.war':
  catalina_base => '/opt/tomcat9',
  war_source    => "puppet:///modules/tomcat/addressbook.war",
}
```
