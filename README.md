# redact

rendering config files from templates

keeping sensible infomation, like passwords, out of config files, so they can
be keeped in version control system

install using pip
```sh
pip install redact
```

## usage

`~/.muttrc.tpl`
```
passwd: #{passwd}
address: #{email}
```

`.gitconfig.tpl`
```
email = #{email}
```

`/var/www/config.php.tpl`
```php
$config['database']['user'] = "#{user}";
$config['database']['passwd'] = "#{passwd}";
$config['email']['sender'] = "#{email}";
```

passwords.yaml
```yaml
email: "foo@foo.com"
~/.muttrc:
    passwd: secret-passwd-for-email
~/.gitconfig:
/var/www/config.php:
    user: username-for-db
    passwd: secret-passwd-for-db
    email: admin@mydomain.com
```

run
```sh
$ redact passwords.yaml
```

will generate(overwrite)
`~/.gitconfig`, `~/.muttrc` and `/var/www/config.php`

specify a different extension other than the default `tpl`
```sh
$ redact --extension template passwords.yaml
```

selectively redact(TBD)
```sh
$ redact --sel gitconfig
$ redact --skip muttrc
```

using pipe
```sh
$ ssh remote-machine "cat ~/passwords.yaml" | redact
```
