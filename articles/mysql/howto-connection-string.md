---
title: aaaConnect toepassingen tooAzure Database voor MySQL | Microsoft Docs
description: Dit document bevat verbindingsreeksen Hallo momenteel niet ondersteund voor toepassingen tooconnect met Azure Database MySQL, met inbegrip van ADO.NET (C#), JDBC, Node.js, ODBC-, PHP, Python en Ruby.
services: mysql
author: mswutao
ms.author: wuta
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 06/12/2017
ms.openlocfilehash: bbcb2c0ddb4f8e5c225ebef53781e073f5c7b1a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-applications-tooazure-database-for-mysql"></a>Hoe tooconnect toepassingen tooAzure voor MySQL-Database
Dit document worden Hallo tekenreeks verbindingstypen die worden ondersteund door Azure Database voor MySQL, samen met sjablonen en voorbeelden. Mogelijk hebt u verschillende parameters en andere instellingen in de verbindingsreeks.

- tooobtain hello certificaat, Zie [hoe tooconfigure SSL](./howto-configure-ssl.md).
- {your_host} = <servername>. mysql.database.azure.com
- {your_user}@{servername} = userID indeling voor verificatie correct.  NET Hallo userID zal gebruikt Hallo verificatie toofail.

## <a name="adonet"></a>ADO.NET
```ado.net
Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password};[SslMode=Required;]
```

In dit voorbeeld Hallo-servernaam is `myserver4demo`, de databasenaam van de is `wpdb`, de gebruikersnaam is `WPAdmin`, en het wachtwoord is `mypassword!2`. Vervolgens moet Hallo-verbindingsreeks:

```ado.net
Server= "myserver4demo.mysql.database.azure.com"; Port=3306; Database= "wpdb"; Uid= "WPAdmin@myserver4demo"; Pwd="mypassword!2"; SslMode=Required;
```

## <a name="jdbc"></a>JDBC
```jdbc
String url ="jdbc:mysql://%s:%s/%s[?verifyServerCertificate=true&useSSL=true&requireSSL=true]",{your_host},{your_port},{your_database}"; myDbConn = DriverManager.getConnection(url, {username@servername}, {your_password}";
```

## <a name="nodejs"></a>Node.js
```node.js
var conn = mysql.createConnection({host: {your_host}, user: {username@servername}, password: {your_password}, database: {your_database}, Port: {your_port}[, ssl:{ca:fs.readFileSync({ca-cert filename})}}]);
```

## <a name="odbc"></a>ODBC
```odbc
DRIVER={MySQL ODBC 5.3 UNICODE Driver};Server={your_host};Port={your_port};Database={your_database};Uid={username@servername};Pwd={your_password}; [sslca={ca-cert filename}; sslverify=1; Option=3;]
```

## <a name="php"></a>PHP
```php
$con=mysqli_init(); [mysqli_ssl_set($con, NULL, NULL, {ca-cert filename}, NULL, NULL);] mysqli_real_connect($con, {your_host}, {username@servername}, {your_password}, {your_database}, {your_port});
```

## <a name="python"></a>Python
```python
cnx = mysql.connector.connect(user={username@servername}, password={your_password}, host={your_host}, port={your_port}, database={your_database}[, ssl_ca={ca-cert filename}, ssl_verify_cert=true])
```

## <a name="ruby"></a>Ruby
```ruby
client = Mysql2::Client.new(username: {username@servername}, password: {your_password}, database: {your_database}, host: {your_host}, port: {your_port}[, sslca:{ca-cert filename}, sslverify:false, sslcipher:'AES256-SHA'])
```

## <a name="get-hello-connection-string-details-from-hello-azure-portal"></a>Hallo verbinding tekenreeks details ophalen van hello Azure-portal
In Hallo [Azure-portal](https://portal.azure.com), gaat u tooyour Azure Database voor de MySQL-server en klik op **verbindingsreeksen** tooget lijst met de tekenreeks voor uw exemplaar: ![Hallo verbinding tekenreeksen deelvenster in Hallo Azure-portal](./media/howto-connection-strings/connection-strings-on-portal.png)

Hallo-tekenreeks bevat informatie zoals Hallo stuurprogramma, server en andere databaseparameters. Deze voorbeelden wijzigen met behulp van uw eigen parameters, zoals de databasenaam van de en wachtwoord. Vervolgens kunt u deze tekenreeks tooconnect toohello server van uw code en toepassingen.

## <a name="next-steps"></a>Volgende stappen
- Zie voor meer informatie over verbindingsbibliotheken [concepten - verbindingsbibliotheken](./concepts-connection-libraries.md).
