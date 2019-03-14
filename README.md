# Use Gitea as service on MacOSx

[Gitea](https://gitea.io) - Git with a cup of tea, A painless self-hosted Git service.

![](media/15525254286192.jpg)


## 1. Install

install gitea with brew.

```
brew tap go-gitea/gitea
brew install gitea
```

## 2. Create a config file of Bootstrapper

create gitea.plist file.
```shell
touch gitea.plist
vim gitea.plist
```

edit it.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>KeepAlive</key>
    <true/>
    <key>Label</key>
    <string>gitea</string>
    <key>ProgramArguments</key>
    <array>
      <string>/usr/local/bin/gitea</string>
      <string>web</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
  </dict>
</plist>
```

move file to local services configuration directory.
```shell
mv gitea.plist $HOME/Library/LaunchAgents/gitea.plist
```

and load it.
```shell
launchctl load -w $HOME/Library/LaunchAgents/gitea.plist
```

Use Gitea service
```shell
# start service
launchctl start gitea

# stop service
launchctl stop gitea
```

## 3. Config Caddyfile for Gitea

install [Caddyserver](https://caddyserver.com/)

```shell
brew install caddy
```

config a local domain for gitea.
```shell
vim /etc/hosts
# for gitea
127.0.0.1   git.test
```

exit Caddyfile
```shell
vim /usr/local/etc/Caddyfile
```

add config.
```
http://git.test {
    proxy / localhost:3000
}
```

## 4. Open gitea with Chrome

```
open http://git.test
```

## 5. Done 🎉🎉🎉🎉🎉