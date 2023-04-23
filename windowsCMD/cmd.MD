# 刷新dns缓存
ipconfig flushdns 

# 计算文件sha256值(也可换为MD5、SHA1等）
certutil -hashfile ideaIU-2023.1.exe sha256

# PowerShell查看文件哈希值
在 PowerShell 中，使用 Get-FileHash cmdlet 计算您下载的 ISO 文件的哈希值
Get-FileHash C:\Users\用户1\Downloads\Contoso8_1_ENT.iso
