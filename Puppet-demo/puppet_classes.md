# Classes

## Class Definition and include
```rb
class webserver {
 package { 'apache2':
  ensure => installed,
 }
 service { 'apache2':
  ensure    => running,
 }
}

class {webserver:}
# or include webserver
```

## Class With Parameters

```rb
class user_account ($username){

  user { $username:
    ensure => present,
    uid    => '101',
    shell  => '/bin/bash',
    home   => "/home/$username",
  }

}

class {user_account:
    username => "homer",
}

#Or
#class {user_account:
#    username => "bart",
#}
```
