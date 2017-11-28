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
# <a name="configure-ssl-connectivity-in-your-application-toosecurely-connect-tooazure-database-for-mysql"></a><span data-ttu-id="ff29b-103">SSL configureren connectiviteit in uw toepassing toosecurely tooAzure Database connect voor MySQL</span><span class="sxs-lookup"><span data-stu-id="ff29b-103">Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL</span></span>
<span data-ttu-id="ff29b-104">Azure MySQL-Database ondersteunt verbindingen van uw Azure-Database voor MySQL tooclient servertoepassingen met Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="ff29b-104">Azure Database for MySQL supports connecting your Azure Database for MySQL server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="ff29b-105">Afdwingen van SSL-verbindingen tussen uw database-server en client-toepassingen beschermt tegen 'man-in Hallo middle'-aanvallen door het versleutelen van de gegevensstroom Hallo tussen Hallo-server en uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ff29b-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="step-1-obtain-ssl-certificate"></a><span data-ttu-id="ff29b-106">Stap 1: SSL-certificaat verkrijgen</span><span class="sxs-lookup"><span data-stu-id="ff29b-106">Step 1: Obtain SSL Certificate</span></span>
<span data-ttu-id="ff29b-107">Hallo-certificaat nodig toocommunicate downloaden via SSL met uw Azure-Database voor de server uit een MySQL [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) en Hallo certificaat tooyour lokale bestand opslaan station (we gebruikt in deze zelfstudie c:\ssl).</span><span class="sxs-lookup"><span data-stu-id="ff29b-107">Download hello certificate needed toocommunicate over SSL with your Azure Database for MySQL server from [https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem) and save hello certificate file tooyour local drive (with this tutorial, we used c:\ssl).</span></span>
<span data-ttu-id="ff29b-108">**Voor Microsoft Internet Explorer en Microsoft Edge:** nadat Hallo downloaden is voltooid, Hallo certificaat tooBaltimoreCyberTrustRoot.crt.pem wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ff29b-108">**For Microsoft Internet Explorer and Microsoft Edge:** After hello download has completed, rename hello certificate tooBaltimoreCyberTrustRoot.crt.pem.</span></span>

## <a name="step-2-bind-ssl"></a><span data-ttu-id="ff29b-109">Stap 2: SSL is gekoppeld</span><span class="sxs-lookup"><span data-stu-id="ff29b-109">Step 2: Bind SSL</span></span>
### <a name="connecting-tooserver-using-hello-mysql-workbench-over-ssl"></a><span data-ttu-id="ff29b-110">Verbinding maken met behulp van Hallo MySQL Workbench via SSL tooserver</span><span class="sxs-lookup"><span data-stu-id="ff29b-110">Connecting tooserver using hello MySQL Workbench over SSL</span></span>
<span data-ttu-id="ff29b-111">MySQL-Workbench tooconnect veilig via SSL configureren.</span><span class="sxs-lookup"><span data-stu-id="ff29b-111">Configure MySQL Workbench tooconnect securely over SSL.</span></span> <span data-ttu-id="ff29b-112">Navigeer toohello **SSL** tabblad in Hallo MySQL Workbench op Hallo dialoog Setup nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="ff29b-112">Navigate toohello **SSL** tab in hello MySQL Workbench on hello Setup New Connection dialogue.</span></span> <span data-ttu-id="ff29b-113">Voer de bestandslocatie Hallo Hallo **BaltimoreCyberTrustRoot.crt.pem** in Hallo **SSL CA bestand:** veld.</span><span class="sxs-lookup"><span data-stu-id="ff29b-113">Enter hello file location of hello **BaltimoreCyberTrustRoot.crt.pem** in hello **SSL CA File:** field.</span></span>
<span data-ttu-id="ff29b-114">![aangepaste tegel opslaan](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="ff29b-114">![save customized tile](./media/howto-configure-ssl/mysql-workbench-ssl.png)</span></span>

### <a name="connecting-tooserver-using-hello-mysql-cli-over-ssl"></a><span data-ttu-id="ff29b-115">Verbinding maken met behulp van Hallo MySQL CLI via SSL tooserver</span><span class="sxs-lookup"><span data-stu-id="ff29b-115">Connecting tooserver using hello MySQL CLI over SSL</span></span>
<span data-ttu-id="ff29b-116">Gebruik Hallo MySQL-opdrachtregelinterface, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ff29b-116">Using hello MySQL command-line interface, execute hello following command:</span></span>
```dos
mysql.exe -h mysqlserver4demo.mysql.database.azure.com -u Username@mysqlserver4demo -p --ssl-ca=c:\ssl\BaltimoreCyberTrustRoot.crt.pem
```

## <a name="step-3--enforcing-ssl-connections-in-azure"></a><span data-ttu-id="ff29b-117">Stap 3: Afdwingen van SSL-verbindingen in Azure</span><span class="sxs-lookup"><span data-stu-id="ff29b-117">Step 3:  Enforcing SSL connections in Azure</span></span> 
### <a name="using-azure-portal"></a><span data-ttu-id="ff29b-118">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="ff29b-118">Using Azure portal</span></span>
<span data-ttu-id="ff29b-119">Met behulp van hello Azure-portal, gaat u naar uw Azure-Database voor MySQL-server en klik op **verbindingsbeveiliging**.</span><span class="sxs-lookup"><span data-stu-id="ff29b-119">Using hello Azure portal, visit your Azure Database for MySQL server and click **Connection security**.</span></span> <span data-ttu-id="ff29b-120">Hallo aan/uit-knop tooenable in- of uitschakelen van Hallo **afdwingen SSL-verbinding** instelling.</span><span class="sxs-lookup"><span data-stu-id="ff29b-120">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="ff29b-121">Klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ff29b-121">Then click **Save**.</span></span> <span data-ttu-id="ff29b-122">Microsoft raadt u aan het inschakelen van tooalways **afdwingen SSL-verbinding** instellen voor een betere beveiliging.</span><span class="sxs-lookup"><span data-stu-id="ff29b-122">Microsoft recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>
<span data-ttu-id="ff29b-123">![Schakel ssl](./media/howto-configure-ssl/enable-ssl.png)</span><span class="sxs-lookup"><span data-stu-id="ff29b-123">![enable-ssl](./media/howto-configure-ssl/enable-ssl.png)</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="ff29b-124">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="ff29b-124">Using Azure CLI</span></span>
<span data-ttu-id="ff29b-125">U kunt inschakelen of uitschakelen van Hallo **ssl-afdwinging** parameter met ingeschakeld of uitgeschakeld waarden respectievelijk in Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ff29b-125">You can enable or disable hello **ssl-enforcement** parameter using Enabled or Disabled values respectively in Azure CLI.</span></span>
```azurecli-interactive
az mysql server update --resource-group myresource --name mysqlserver4demo --ssl-enforcement Enabled
```

## <a name="step-4-verify-ssl-connection"></a><span data-ttu-id="ff29b-126">Stap 4: Controleren of de SSL-verbinding</span><span class="sxs-lookup"><span data-stu-id="ff29b-126">Step 4: Verify SSL Connection</span></span>
<span data-ttu-id="ff29b-127">Hallo mysql uitvoeren **status** opdracht tooverify dat u tooyour MySQL-server via SSL verbinding hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="ff29b-127">Execute hello mysql **status** command tooverify that you have connected tooyour MySQL server using SSL:</span></span>
```dos
mysql> status
```
<span data-ttu-id="ff29b-128">Bevestig het Hallo-verbinding aan de hand van de uitvoer Hallo is versleuteld.</span><span class="sxs-lookup"><span data-stu-id="ff29b-128">Confirm hello connection is encrypted by reviewing hello output.</span></span> <span data-ttu-id="ff29b-129">Moet worden weergegeven: **SSL: Cipher in gebruik is AES256 SHA**</span><span class="sxs-lookup"><span data-stu-id="ff29b-129">It should show:  **SSL: Cipher in use is AES256-SHA**</span></span> 

## <a name="sample-code"></a><span data-ttu-id="ff29b-130">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="ff29b-130">Sample code</span></span>
### <a name="php"></a><span data-ttu-id="ff29b-131">PHP</span><span class="sxs-lookup"><span data-stu-id="ff29b-131">PHP</span></span>
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "/var/www/html/BaltimoreCyberTrustRoot.crt.pem", NULL, NULL) ; 
mysqli_real_connect($conn, 'myserver4demo.mysql.database.azure.com', 'myadmin@myserver4demo', 'yourpassword', 'quickstartdb', 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}
```
### <a name="python"></a><span data-ttu-id="ff29b-132">Python</span><span class="sxs-lookup"><span data-stu-id="ff29b-132">Python</span></span>
```
try:
conn = mysql.connector.connect(user='myadmin@myserver4demo',password='yourpassword',database='quickstartdb',host='myserver4demo.mysql.database.azure.com',ssl_ca='/var/www/html/BaltimoreCyberTrustRoot.crt.pem')
except mysql.connector.Error as err:
 print(err)
```

## <a name="next-steps"></a><span data-ttu-id="ff29b-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff29b-133">Next steps</span></span>
<span data-ttu-id="ff29b-134">Bekijk verschillende toepassing connectiviteitsopties na [verbindingsbibliotheken voor Azure-Database voor MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ff29b-134">Review various application connectivity options following [Connection libraries for Azure Database for MySQL](concepts-connection-libraries.md)</span></span>
