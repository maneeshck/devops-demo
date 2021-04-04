# variables
``` rb
$content = "This content is defined in a variable"
file {'/tmp/fileContainingVariableText':
  ensure  => file,
  content => ${content},
}
```
# Factor variables:
``` rb
notify { 'OS Family':
 message => $facts['os']['family']
}

```
