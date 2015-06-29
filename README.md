# redact

rendering config files from templates

keeping sensible infomation, like passwords, out of config files, so they can
be keeped in version control system

install using pip
```sh
pip install redact
```

## usage

given a template `~/.muttrc.tpl`

```
passwd: #{mutt.passwd}
address: #{mutt.email}
```

render `~/.muttrc` interactively with redact

```
redact ~/.muttrc.tpl
mutt.password
> secret
mutt.email
> contact@redact.com
~/.muttrc updated
```

keep track of template file locations and save/load variables

```
redact -t ~/.redact -s ~/.secret ~/.muttrc.tpl
```

render a list of templates

```
redact -t ~/.redact -s ~/.secret
```
