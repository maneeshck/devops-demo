# Puppet resources

## Resource
1. File
``` rb
file { 'helloworld':
  path    => '/tmp/helloworld.conf',
  ensure  => file,
  content => "Hello World",
}
```
2. package
``` rb
package { 'apache2':
  ensure => installed,
}
```
3. relationships
``` rb
package { 'apache2':
  ensure => installed,
  before => File['helloworld'],
}
service { 'apache2':
  ensure    => running,
  subscribe => Package['apache2'],
}
```

4. Notify
``` rb
notify { 'Debug Message':
  message  => "hello",
}
```

## Classes
webserver.pp
``` rb
class webserver {
 package { 'apache2':
  ensure => installed,
 }
 service { 'apache2':
  ensure    => running,
 }
}
```

In site.pp

```include webserver```
