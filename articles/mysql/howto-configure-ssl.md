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
# <a name="configure-ssl-connectivity-in-your-application-to-securely-connect-to-azure-database-for-mysql"></a><span data-ttu-id="9b3bc-103">SSL-verbindingen in uw toepassing veilig verbinding kunnen maken met Azure-Database voor MySQL configureren</span><span class="sxs-lookup"><span data-stu-id="9b3bc-103">Configure SSL connectivity in your application to securely connect to Azure Database for MySQL</span></span>
<span data-ttu-id="9b3bc-104">Azure MySQL-Database ondersteunt verbindingen van uw Azure-Database voor de MySQL-server met clienttoepassingen met Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="9b3bc-105">Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in het midden'-aanvallen door het versleutelen van de gegevensstroom tussen de server en uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="9b3bc-106">Stap 1: SSL-certificaat verkrijgen</span><span class="sxs-lookup"><span data-stu-id="9b3bc-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="9b3bc-107">Download het certificaat nodig om te communiceren via SSL met uw Azure-Database voor de server uit een MySQL [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) en sla het certificaatbestand op de lokale schijf (met Deze zelfstudie hebben we gebruikt c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="9b3bc-107">Download the certificate needed to communicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save the certificate file to your local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="9b3bc-108">**Voor Microsoft Internet Explorer en Microsoft Edge:** nadat het downloaden is voltooid, wijzig de naam van het certificaat naar BaltimoreCyberTrustRoot.crt.pem.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-108">**For Microsoft Internet Explorer and Microsoft Edge:** After the download has completed, rename the certificate to BaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="9b3bc-109">Stap 2: SSL is gekoppeld</span><span class="sxs-lookup"><span data-stu-id="9b3bc-109">Step 2: Bind SSL</span></span>
### <a name="connecting-to-server-using-the-mysql-workbench-over-ssl"></a><span data-ttu-id="9b3bc-110">Verbinding maken met server met behulp van de MySQL-Workbench via SSL</span><span class="sxs-lookup"><span data-stu-id="9b3bc-110">Connecting to server using the MySQL Workbench over SSL</span></span>
<span data-ttu-id="9b3bc-111">MySQL-Workbench veilig verbinding te maken via SSL configureren.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-111">Configure MySQL Workbench to connect securely over SSL.</span></span> <span data-ttu-id="9b3bc-112">Navigeer naar de **SSL** tabblad in de MySQL Workbench op de dialoog Setup nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-112">Navigate to the **SSL** tab in the MySQL Workbench on the Setup New Connection dialogue.</span></span> <span data-ttu-id="9b3bc-113">Geef de bestandslocatie van de **BaltimoreCyberTrustRoot.crt.pem** in de **SSL CA bestand:** veld.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-113">Enter the file location of the **BaltimoreCyberTrustRoot.crt.pem** in the **SSL CA File:** field.</span></span>
<span data-ttu-id="9b3bc-114">![aangepaste tegel opslaan](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="9b3bc-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-to-server-using-the-mysql-cli-over-ssl"></a><span data-ttu-id="9b3bc-115">Verbinding maken met server met behulp van de CLI MySQL via SSL</span><span class="sxs-lookup"><span data-stu-id="9b3bc-115">Connecting to server using the MySQL CLI over SSL</span></span>
<span data-ttu-id="9b3bc-116">Met de opdrachtregelinterface MySQL, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-116">Using the MySQL command-line interface, execute the following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="9b3bc-117">Stap 3: Afdwingen van SSL-verbindingen in Azure</span><span class="sxs-lookup"><span data-stu-id="9b3bc-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="9b3bc-118">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="9b3bc-118">Using Azure portal</span></span>
<span data-ttu-id="9b3bc-119">Met de Azure portal, gaat u naar uw Azure-Database voor MySQL-server en klik op **verbindingsbeveiliging**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-119">Using the Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="9b3bc-120">Gebruik de wisselknop inschakelen of uitschakelen de **afdwingen SSL-verbinding** instelling.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-120">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="9b3bc-121">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-121">Then click **Save**.</span></span> <span data-ttu-id="9b3bc-122">Microsoft raadt aan om in te schakelen altijd **afdwingen SSL-verbinding** instellen voor een betere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-122">Microsoft recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="9b3bc-123">![Schakel ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="9b3bc-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="9b3bc-124">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="9b3bc-124">Using Azure CLI</span></span>
<span data-ttu-id="9b3bc-125">U kunt inschakelen of uitschakelen de **ssl-afdwinging** parameter met ingeschakeld of uitgeschakeld waarden respectievelijk in Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-125">You can enable or disable the **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="9b3bc-126">Stap 4: Controleren of de SSL-verbinding</span><span class="sxs-lookup"><span data-stu-id="9b3bc-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="9b3bc-127">Uitvoeren van de mysql **status** om te controleren of u verbinding hebt gemaakt met uw MySQL-server via SSL:</span><span class="sxs-lookup"><span data-stu-id="9b3bc-127">Execute the mysql **status** command to verify that you have connected to your MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="9b3bc-128">Controleer dat de verbinding aan de hand van de uitvoer is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="9b3bc-128">Confirm the connection is encrypted by reviewing the output.</span></span> <span data-ttu-id="9b3bc-129">Moet worden weergegeven: **SSL: Cipher in gebruik is AES256 SHA**</span><span class="sxs-lookup"><span data-stu-id="9b3bc-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="9b3bc-130">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="9b3bc-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="9b3bc-131">PHP</span><span class="sxs-lookup"><span data-stu-id="9b3bc-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="9b3bc-132">Python</span><span class="sxs-lookup"><span data-stu-id="9b3bc-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="9b3bc-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b3bc-133">Next steps</span></span>
<span data-ttu-id="9b3bc-134">Bekijk verschillende toepassing connectiviteitsopties na [verbindingsbibliotheken voor Azure-Database voor MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="9b3bc-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
