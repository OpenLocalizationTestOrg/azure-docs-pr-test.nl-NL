---
title: Configureren van SSL-verbindingen veilig verbinding kunnen maken met Azure-Database voor MySQL | Microsoft Docs
description: Instructies voor het correcte configuratie van Azure-Database voor MySQL en de bijbehorende toepassingen juist gebruik van SSL-verbindingen
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 77e1b6266a2cf47949fa06358ec003f6b6b38065
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ssl-connectivity-in-your-application-to-securely-connect-to-azure-database-for-mysql"></a>SSL-verbindingen in uw toepassing veilig verbinding kunnen maken met Azure-Database voor MySQL configureren
Azure MySQL-Database ondersteunt verbindingen van uw Azure-Database voor de MySQL-server met clienttoepassingen met Secure Sockets Layer (SSL). Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in het midden'-aanvallen door het versleutelen van de gegevensstroom tussen de server en uw toepassing.

## <a name="step-1-obtain-ssl-certificate"></a>Stap 1: SSL-certificaat verkrijgen
Download het certificaat nodig om te communiceren via SSL met uw Azure-Database voor de server uit een MySQL [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) en sla het certificaatbestand op de lokale schijf (met Deze zelfstudie hebben we gebruikt c:\ssl).
**Voor Microsoft Internet Explorer en Microsoft Edge:** nadat het downloaden is voltooid, wijzig de naam van het certificaat naar BaltimoreCyberTrustRoot.crt.pem.

## <a name="step-2-bind-ssl"></a>Stap 2: SSL is gekoppeld
### <a name="connecting-to-server-using-the-mysql-workbench-over-ssl"></a>Verbinding maken met server met behulp van de MySQL-Workbench via SSL
MySQL-Workbench veilig verbinding te maken via SSL configureren. Navigeer naar de **SSL** tabblad in de MySQL Workbench op de dialoog Setup nieuwe verbinding. Geef de bestandslocatie van de **BaltimoreCyberTrustRoot.crt.pem** in de **SSL CA bestand:** veld.
![aangepaste tegel opslaan](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-to-server-using-the-mysql-cli-over-ssl"></a>Verbinding maken met server met behulp van de CLI MySQL via SSL
Met de opdrachtregelinterface MySQL, voer de volgende opdracht:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>Stap 3: Afdwingen van SSL-verbindingen in Azure 
### <a name="using-azure-portal"></a>Azure Portal gebruiken
Met de Azure portal, gaat u naar uw Azure-Database voor MySQL-server en klik op **verbindingsbeveiliging**. Gebruik de wisselknop inschakelen of uitschakelen de **afdwingen SSL-verbinding** instelling. Klik vervolgens op **Opslaan**. Microsoft raadt aan om in te schakelen altijd **afdwingen SSL-verbinding** instellen voor een betere beveiliging.
![Schakel ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Azure CLI gebruiken
U kunt inschakelen of uitschakelen de **ssl-afdwinging** parameter met ingeschakeld of uitgeschakeld waarden respectievelijk in Azure CLI.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Stap 4: Controleren of de SSL-verbinding
Uitvoeren van de mysql **status** om te controleren of u verbinding hebt gemaakt met uw MySQL-server via SSL:
```dos
mysql> status
```
Controleer dat de verbinding aan de hand van de uitvoer is versleuteld. Moet worden weergegeven: **SSL: Cipher in gebruik is AES256 SHA** 

## <a name="sample-code"></a>Voorbeeldcode
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a>Python
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a>Volgende stappen
Bekijk verschillende toepassing connectiviteitsopties na [verbindingsbibliotheken voor Azure-Database voor MySQL](concepts-connection-libraries.md)
