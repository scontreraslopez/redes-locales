# Colección de comandos útiles

En powershell, para comprobar conectividad en los casos en los que ICMP está bloqueado: 

$tcpConnection = New-Object System.Net.Sockets.TcpClient($FTPServer, $FTPPort)

