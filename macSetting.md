## 截屏 
修改截屏命令<br/>
``` shell
修改截图文件保存路径
defaults write com.apple.screencapture location /Users/lvan/Desktop/ScreenShots

修改截图文件格式
defaults write com.apple.screencapture type jpg;killall SystemUIServer
```

## 允许所有来源 
``` shell
sudo spctl --master-disable
```