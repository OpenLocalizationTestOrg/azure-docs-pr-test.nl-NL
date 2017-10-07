---
title: aaaConfigure SSL connectiviteit toosecurely tooAzure Database connect voor MySQL | Microsoft Docs
description: Instructies voor hoe tooproperly Azure-Database configureren voor MySQL en bijbehorende toepassingen toocorrectly SSL-verbindingen gebruiken
services: mysql
author: seanli1988
ms.author: seanli
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 07/28/2017
ms.openlocfilehash: 8c37c19d4c101abfb730f429a19441e94e52fc85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a>SSL configureren connectiviteit in uw toepassing toosecurely tooAzure Database connect voor MySQL
Azure MySQL-Database ondersteunt verbindingen van uw Azure-Database voor MySQL tooclient servertoepassingen met Secure Sockets Layer (SSL). Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in Hallo middle'-aanvallen door het versleutelen van de gegevensstroom Hallo tussen Hallo-server en uw toepassing.

## <a name="step-1-obtain-ssl-certificate"></a>Stap 1: SSL-certificaat verkrijgen
Hallo-certificaat nodig toocommunicate downloaden via SSL met uw Azure-Database voor de server uit een MySQL [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) en Hallo certificaat tooyour lokale bestand opslaan station (we gebruikt in deze zelfstudie c:\ssl).
**Voor Microsoft Internet Explorer en Microsoft Edge:** nadat Hallo downloaden is voltooid, Hallo certificaat tooBaltimoreCyberTrustRoot.crt.pem wijzigen.

## <a name="step-2-bind-ssl"></a>Stap 2: SSL is gekoppeld
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a>Verbinding maken met behulp van Hallo MySQL Workbench via SSL tooserver
MySQL-Workbench tooconnect veilig via SSL configureren. Navigeer toohello **SSL** tabblad in Hallo MySQL Workbench op Hallo dialoog Setup nieuwe verbinding. Voer de bestandslocatie Hallo Hallo **BaltimoreCyberTrustRoot.crt.pem** in Hallo **SSL CA bestand:** veld.
![aangepaste tegel opslaan](./media/howto-configure-ssl/mysql-workbench-ssl.png)

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a>Verbinding maken met behulp van Hallo MySQL CLI via SSL tooserver
Gebruik Hallo MySQL-opdrachtregelinterface, Hallo volgende opdracht uitvoeren:
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a>Stap 3: Afdwingen van SSL-verbindingen in Azure 
### <a name="using-azure-portal"></a>Azure Portal gebruiken
Met behulp van hello Azure-portal, gaat u naar uw Azure-Database voor MySQL-server en klik op **verbindingsbeveiliging**. Hallo aan/uit-knop tooenable in- of uitschakelen van Hallo **afdwingen SSL-verbinding** instelling. Klik vervolgens op **Opslaan**. Microsoft raadt u aan het inschakelen van tooalways **afdwingen SSL-verbinding** instellen voor een betere beveiliging.
![Schakel ssl](./media/howto-configure-ssl/enable-ssl.png)

### <a name="using-azure-cli"></a>Azure CLI gebruiken
U kunt inschakelen of uitschakelen van Hallo **ssl-afdwinging** parameter met ingeschakeld of uitgeschakeld waarden respectievelijk in Azure CLI.
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a>Stap 4: Controleren of de SSL-verbinding
Hallo mysql uitvoeren **status** opdracht tooverify dat u tooyour MySQL-server via SSL verbinding hebt gemaakt:
```dos
mysql> status
```
Bevestig het Hallo-verbinding aan de hand van de uitvoer Hallo is versleuteld. Moet worden weergegeven: **SSL: Cipher in gebruik is AES256 SHA** 

## <a name="sample-code"></a>Voorbeeldcode
### <a name="php"></a>PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
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
