---
title: aaaBuild een Java- en MySQL web-app in Azure
description: Meer informatie over hoe tooget een Java-app die is verbonden toohello Azure MySQL database-service in Azure App service werkt.
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="41db1-103">Een Java- en MySQL web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="41db1-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="41db1-104">Deze zelfstudie leert u hoe toocreate een Java web-app in Azure en verbindt u deze tooa MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="41db1-104">This tutorial shows you how toocreate a Java web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="41db1-105">Wanneer u klaar bent, hebt u een [Spring Boot](https://projects.spring.io/spring-boot/) toepassing opslaan van gegevens in [Azure Database voor MySQL](https://docs.microsoft.com/azure/mysql/overview) uitgevoerd op [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="41db1-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Java-app uitgevoerd in Azure App service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="41db1-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="41db1-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="41db1-108">Een MySQL-database maken in Azure</span><span class="sxs-lookup"><span data-stu-id="41db1-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="41db1-109">Verbinding maken met een voorbeeld-app toohello database</span><span class="sxs-lookup"><span data-stu-id="41db1-109">Connect a sample app toohello database</span></span>
> * <span data-ttu-id="41db1-110">Hallo app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="41db1-110">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="41db1-111">Bijwerken en het Hallo-app implementeren</span><span class="sxs-lookup"><span data-stu-id="41db1-111">Update and redeploy hello app</span></span>
> * <span data-ttu-id="41db1-112">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="41db1-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="41db1-113">Hallo app controleren in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="41db1-113">Monitor hello app in hello Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="41db1-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="41db1-114">Prerequisites</span></span>

1. [<span data-ttu-id="41db1-115">Download en installeer Git</span><span class="sxs-lookup"><span data-stu-id="41db1-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="41db1-116">Download en installeer Hallo JDK van Java-7 of hoger</span><span class="sxs-lookup"><span data-stu-id="41db1-116">Download and install hello Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="41db1-117">Downloaden, installeren en starten van MySQL</span><span class="sxs-lookup"><span data-stu-id="41db1-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="41db1-118">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="41db1-118">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="41db1-119">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="41db1-119">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="41db1-120">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="41db1-120">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="41db1-121">Lokale MySQL voorbereiden</span><span class="sxs-lookup"><span data-stu-id="41db1-121">Prepare local MySQL</span></span> 

<span data-ttu-id="41db1-122">In deze stap maakt u een database in een lokale MySQL-server voor gebruik in testen Hallo app lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="41db1-122">In this step, you create a database in a local MySQL server for use in testing hello app locally on your machine.</span></span>

### <a name="connect-toomysql-server"></a><span data-ttu-id="41db1-123">TooMySQL server verbinden</span><span class="sxs-lookup"><span data-stu-id="41db1-123">Connect tooMySQL server</span></span>

<span data-ttu-id="41db1-124">In een terminalvenster verbinding tooyour lokale MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="41db1-124">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="41db1-125">U kunt deze toorun terminalvenster alle Hallo-opdrachten gebruiken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="41db1-125">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="41db1-126">Als u wordt gevraagd om een wachtwoord, hello wachtwoord invoeren voor Hallo `root` account.</span><span class="sxs-lookup"><span data-stu-id="41db1-126">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="41db1-127">Als je het wachtwoord van je root-account, Zie [MySQL: hoe tooReset hoofdwachtwoord Hallo](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="41db1-127">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="41db1-128">Als uw opdracht is uitgevoerd, wordt al uw MySQL-server uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="41db1-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="41db1-129">Als dit niet het geval is, zorg ervoor dat de lokale MySQL-server is gestart met de volgende Hallo [MySQL na de installatie stappen](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="41db1-129">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="41db1-130">Een database maken</span><span class="sxs-lookup"><span data-stu-id="41db1-130">Create a database</span></span> 

<span data-ttu-id="41db1-131">In Hallo `mysql` vragen, maakt u een database en een tabel voor Hallo taakitems.</span><span class="sxs-lookup"><span data-stu-id="41db1-131">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="41db1-132">Uw serververbinding sluiten door te typen `quit`.</span><span class="sxs-lookup"><span data-stu-id="41db1-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a><span data-ttu-id="41db1-133">Maken en Hallo voorbeeld-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="41db1-133">Create and run hello sample app</span></span> 

<span data-ttu-id="41db1-134">In deze stap voorbeeldapp Spring opstarten klonen, toouse Hallo lokale MySQL-database configureren en uitvoeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="41db1-134">In this step, you clone sample Spring boot app, configure it toouse hello local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="41db1-135">Kloon Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="41db1-135">Clone hello sample</span></span>

<span data-ttu-id="41db1-136">Navigeer in terminalvenster hello, tooa directory- en kloon Hallo voorbeeld opslagplaats werkt.</span><span class="sxs-lookup"><span data-stu-id="41db1-136">In hello terminal window, navigate tooa working directory and clone hello sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a><span data-ttu-id="41db1-137">Hallo app toouse Hallo MySQL-database configureren</span><span class="sxs-lookup"><span data-stu-id="41db1-137">Configure hello app toouse hello MySQL database</span></span>

<span data-ttu-id="41db1-138">Update Hallo `spring.datasource.password` en de waarde *spring-boot-mysql-todo/src/main/resources/application.properties* Hello dezelfde hoofdwachtwoord tooopen Hallo MySQL prompt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="41db1-138">Update hello `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with hello same root password used tooopen hello MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a><span data-ttu-id="41db1-139">Bouwen en uitvoeren van Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="41db1-139">Build and run hello sample</span></span>

<span data-ttu-id="41db1-140">Bouwen en uitvoeren met Hallo Maven wrapper die is opgenomen in de opslagplaats Hallo Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="41db1-140">Build and run hello sample using hello Maven wrapper included in hello repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="41db1-141">Open uw browser toohttp://localhost:8080 toosee in de steekproef Hallo in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="41db1-141">Open your browser toohttp://localhost:8080 toosee in hello sample in action.</span></span> <span data-ttu-id="41db1-142">Als u een lijst met taken toohello toevoegt, gebruik Hallo volgende SQL-in Hallo MySQL vragen tooview Hallo opgeslagen gegevens in MySQL opdrachten.</span><span class="sxs-lookup"><span data-stu-id="41db1-142">As you add tasks toohello list,  use hello following SQL commands in hello MySQL prompt tooview hello data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="41db1-143">Hallo toepassing stoppen roept `Ctrl` + `C` in Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="41db1-143">Stop hello application by hitting `Ctrl`+`C` in hello terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="41db1-144">Een Azure-MySQL-database maken</span><span class="sxs-lookup"><span data-stu-id="41db1-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="41db1-145">In deze stap maakt u een [Azure Database voor MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) exemplaar met gebruikmaking van Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="41db1-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using hello [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="41db1-146">U Hallo voorbeeld toepassing toouse deze database later op in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="41db1-146">You configure hello sample application toouse this database later on in hello tutorial.</span></span>

<span data-ttu-id="41db1-147">Gebruik hello Azure CLI 2.0 in een terminalvenster toocreate Hallo bronnen nodig toohost uw Java-toepassing in Azure App service.</span><span class="sxs-lookup"><span data-stu-id="41db1-147">Use hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost your Java application in Azure appservice.</span></span> <span data-ttu-id="41db1-148">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="41db1-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="41db1-149">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="41db1-149">Create a resource group</span></span>

<span data-ttu-id="41db1-150">Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) Hello [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="41db1-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="41db1-151">Een Azure-resourcegroep is een logische container waar verwante resources, zoals web-apps, databases en storage-accounts worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="41db1-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="41db1-152">Hallo volgende voorbeeld wordt een resourcegroep in Hallo Noord-Europa regio:</span><span class="sxs-lookup"><span data-stu-id="41db1-152">hello following example creates a resource group in hello North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="41db1-153">toosee hello mogelijke waarden kunt u gebruiken voor `--location`, gebruik Hallo [az appservice lijst-locaties](/cli/azure/appservice#list-locations) opdracht.</span><span class="sxs-lookup"><span data-stu-id="41db1-153">toosee hello possible values you can use for `--location`, use hello [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="41db1-154">Een MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="41db1-154">Create a MySQL server</span></span>

<span data-ttu-id="41db1-155">Maken van een server in Azure-Database voor MySQL (Preview) Hello [az mysql-server maken](/cli/azure/mysql/server#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="41db1-155">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="41db1-156">Vervangen door uw eigen unieke MySQL servernaam op waar u Hallo zien `<mysql_server_name>` tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="41db1-156">Substitute your own unique MySQL server name where you see hello `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="41db1-157">Deze naam maakt deel uit van de hostnaam van uw MySQL-server, `<mysql_server_name>.mysql.database.azure.com`, dus moet toobe globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="41db1-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs toobe globally unique.</span></span> <span data-ttu-id="41db1-158">Ook vervangen `<admin_user>` en `<admin_password>` met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="41db1-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="41db1-159">Wanneer Hallo MySQL-server is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="41db1-159">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="41db1-160">Een firewall configureren</span><span class="sxs-lookup"><span data-stu-id="41db1-160">Configure server firewall</span></span>

<span data-ttu-id="41db1-161">Een firewallregel maken voor uw MySQL server tooallow client verbindingen via Hallo [az mysql server-firewallregel maken](/cli/azure/mysql/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="41db1-161">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="41db1-162">Azure-Database voor MySQL (Preview) kunnen niet automatisch momenteel verbindingen van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="41db1-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="41db1-163">Zoals IP-adressen in Azure dynamisch toegewezen worden, is het beter tooenable alle IP-adressen voor nu.</span><span class="sxs-lookup"><span data-stu-id="41db1-163">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses for now.</span></span> <span data-ttu-id="41db1-164">Wanneer Hallo service de preview blijft, kunt u betere methoden voor het beveiligen van uw database wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="41db1-164">As hello service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-hello-azure-mysql-database"></a><span data-ttu-id="41db1-165">Hello Azure MySQL-database configureren</span><span class="sxs-lookup"><span data-stu-id="41db1-165">Configure hello Azure MySQL database</span></span>

<span data-ttu-id="41db1-166">In terminalvenster Hallo op uw computer verbinding met toohello MySQL-server in Azure.</span><span class="sxs-lookup"><span data-stu-id="41db1-166">In hello terminal window on your computer, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="41db1-167">Hallo-waarde die u eerder hebt opgegeven voor `<admin_user>` en `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="41db1-167">Use hello value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="41db1-168">Een database maken</span><span class="sxs-lookup"><span data-stu-id="41db1-168">Create a database</span></span> 

<span data-ttu-id="41db1-169">In Hallo `mysql` vragen, maakt u een database en een tabel voor Hallo taakitems.</span><span class="sxs-lookup"><span data-stu-id="41db1-169">In hello `mysql` prompt, create a database and a table for hello to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="41db1-170">Een gebruiker met machtigingen maken</span><span class="sxs-lookup"><span data-stu-id="41db1-170">Create a user with permissions</span></span>

<span data-ttu-id="41db1-171">Een databasegebruiker maken en hieraan alle bevoegdheden in Hallo `tododb` database.</span><span class="sxs-lookup"><span data-stu-id="41db1-171">Create a database user and give it all privileges in hello `tododb` database.</span></span> <span data-ttu-id="41db1-172">Vervang de tijdelijke aanduidingen Hallo `<Javaapp_user>` en `<Javaapp_password>` met uw eigen unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="41db1-172">Replace hello placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

<span data-ttu-id="41db1-173">Uw serververbinding sluiten door te typen `quit`.</span><span class="sxs-lookup"><span data-stu-id="41db1-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a><span data-ttu-id="41db1-174">Hallo voorbeeld tooAzure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="41db1-174">Deploy hello sample tooAzure App Service</span></span>

<span data-ttu-id="41db1-175">Maken van een Azure App Service-abonnement met Hallo **vrije** prijscategorie Hallo met [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="41db1-175">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="41db1-176">Hallo appservice-abonnement definieert Hallo fysieke resources gebruikt toohost uw apps.</span><span class="sxs-lookup"><span data-stu-id="41db1-176">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="41db1-177">Alle toepassingen die toegewezen tooan appservice-abonnement kunt u deze resources, zodat u toosave kosten bij het hosten van meerdere apps delen.</span><span class="sxs-lookup"><span data-stu-id="41db1-177">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="41db1-178">Wanneer Hallo plan klaar is, uitvoer hello die Azure CLI ongeveer dezelfde wordt toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="41db1-178">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="41db1-179">Een Azure-Web-app maken</span><span class="sxs-lookup"><span data-stu-id="41db1-179">Create an Azure Web app</span></span>

 <span data-ttu-id="41db1-180">Gebruik Hallo [az webapp maken](/cli/azure/appservice/web#create) CLI opdracht toocreate de definitie van een web-app in Hallo `myAppServicePlan` App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="41db1-180">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="41db1-181">Hallo web app definitie voorziet in uw toepassing met een URL-tooaccess en verschillende opties toodeploy uw code tooAzure configureert.</span><span class="sxs-lookup"><span data-stu-id="41db1-181">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="41db1-182">Vervang Hallo `<app_name>` aanduiding voor items met uw eigen unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="41db1-182">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="41db1-183">Deze unieke naam is onderdeel van de standaarddomeinnaam Hallo voor Hallo-web-app Hallo naam moet toobe uniek zijn in alle apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="41db1-183">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="41db1-184">U kunt een aangepast domein de naam van vermelding toohello web-app kunt toewijzen, voordat u deze tooyour gebruikers weergeven.</span><span class="sxs-lookup"><span data-stu-id="41db1-184">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="41db1-185">Wanneer de definitie van Hallo web apps klaar is, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="41db1-185">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="41db1-186">Java configureren</span><span class="sxs-lookup"><span data-stu-id="41db1-186">Configure Java</span></span> 

<span data-ttu-id="41db1-187">Hallo Java runtime-configuratie die uw app Hello moet instellen [az appservice web config update](/cli/azure/appservice/web/config#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="41db1-187">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="41db1-188">Hallo volgende opdracht configureert u Hallo web app toorun op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="41db1-188">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a><span data-ttu-id="41db1-189">Hallo app toouse hello Azure SQL database configureren</span><span class="sxs-lookup"><span data-stu-id="41db1-189">Configure hello app toouse hello Azure SQL database</span></span>

<span data-ttu-id="41db1-190">Voordat u de voorbeeld-app hello, stelt u toepassingsinstellingen op Hallo web app toouse hello Azure MySQL-database die in Azure worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="41db1-190">Before running hello sample app, set application settings on hello web app toouse hello Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="41db1-191">Deze eigenschappen zijn blootgestelde toohello webtoepassing als omgevingsvariabelen en Hallo onderdrukkingswaarden in Hallo application.properties binnen Hallo verpakte web-app ingesteld.</span><span class="sxs-lookup"><span data-stu-id="41db1-191">These properties are exposed toohello web application as environment variables and override hello values set in hello application.properties inside hello packaged web app.</span></span> 

<span data-ttu-id="41db1-192">Toepassingsinstellingen met [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in Hallo CLI:</span><span class="sxs-lookup"><span data-stu-id="41db1-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in hello CLI:</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="41db1-193">FTP-implementatiereferenties ophalen</span><span class="sxs-lookup"><span data-stu-id="41db1-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="41db1-194">U kunt uw toepassing tooAzure appservice op verschillende manieren, met inbegrip van de FTP-, lokale Git, GitHub, Visual Studio Team Services en BitBucket implementeren.</span><span class="sxs-lookup"><span data-stu-id="41db1-194">You can deploy your application tooAzure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="41db1-195">FTP-toodeploy Hallo voor dit voorbeeld. WAR-bestand is gebouwd eerder op uw lokale machine tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="41db1-195">For this example, FTP toodeploy hello .WAR file built previously on your local machine tooAzure App Service.</span></span>

<span data-ttu-id="41db1-196">toodetermine wat toopass langs in een FTP-opdracht toohello Web-App gebruikt de referenties [implementatie in az appservice web-lijst-publicatie-profielen](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) opdracht:</span><span class="sxs-lookup"><span data-stu-id="41db1-196">toodetermine what credentials toopass along in an ftp command toohello Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a><span data-ttu-id="41db1-197">Met FTP Hallo-app uploaden</span><span class="sxs-lookup"><span data-stu-id="41db1-197">Upload hello app using FTP</span></span>

<span data-ttu-id="41db1-198">Gebruik uw favoriete toodeploy Hallo voor FTP-hulpprogramma. WAR-bestand toohello */site/wwwroot/webapps* map op het Hallo-serveradres die afkomstig zijn uit Hallo `URL` veld in de vorige opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="41db1-198">Use your favorite FTP tool toodeploy hello .WAR file toohello */site/wwwroot/webapps* folder on hello server address taken from hello `URL` field in hello previous command.</span></span> <span data-ttu-id="41db1-199">Hallo bestaande (ROOT) standaardmap toepassingen verwijderen en vervang bestaande ROOT.war Hello Hallo. Ingebouwd in Hallo eerder in de zelfstudie Hallo WAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="41db1-199">Remove hello existing default (ROOT) application directory and replace hello existing ROOT.war with hello .WAR file built in hello earlier in hello tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a><span data-ttu-id="41db1-200">Test Hallo web-app</span><span class="sxs-lookup"><span data-stu-id="41db1-200">Test hello web app</span></span>

<span data-ttu-id="41db1-201">Te bladeren`http://<app_name>.azurewebsites.net/` en enkele taken toohello lijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="41db1-201">Browse too`http://<app_name>.azurewebsites.net/` and add a few tasks toohello list.</span></span> 

![Java-app uitgevoerd in Azure App service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="41db1-203">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="41db1-203">**Congratulations!**</span></span> <span data-ttu-id="41db1-204">U uitvoert een Java-gegevensgestuurde app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="41db1-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="41db1-205">Update Hallo app en de implementatie opnieuw uit</span><span class="sxs-lookup"><span data-stu-id="41db1-205">Update hello app and redeploy</span></span>

<span data-ttu-id="41db1-206">Werk Hallo toepassing tooinclude een extra kolom in de takenlijst Hallo voor welke dag Hallo-item is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="41db1-206">Update hello application tooinclude an additional column in hello todo list for what day hello item was created.</span></span> <span data-ttu-id="41db1-207">Spring opstarten verwerkt bijwerken Hallo-databaseschema voor u als wijzigingen in het gegevensmodel Hallo zonder uw bestaande databaserecords zelf te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="41db1-207">Spring Boot handles updating hello database schema for you as hello data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="41db1-208">Open op uw lokale systeem *src/main/java/com/example/fabrikam/TodoItem.java* en voeg de volgende Hallo importeert toohello klasse:</span><span class="sxs-lookup"><span data-stu-id="41db1-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add hello following imports toohello class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="41db1-209">Voeg een `String` eigenschap `timeCreated` te*src/main/java/com/example/fabrikam/TodoItem.java*, deze met een tijdstempel bij het maken van een object te initialiseren.</span><span class="sxs-lookup"><span data-stu-id="41db1-209">Add a `String` property `timeCreated` too*src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="41db1-210">Toevoegen van getters/setters voor nieuwe Hallo `timeCreated` eigenschap tijdens het bewerken van dit bestand.</span><span class="sxs-lookup"><span data-stu-id="41db1-210">Add getters/setters for hello new `timeCreated` property while you are editing this file.</span></span>

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. <span data-ttu-id="41db1-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* met een regel in Hallo `updateTodo` methode tooset Hallo tijdstempel:</span><span class="sxs-lookup"><span data-stu-id="41db1-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in hello `updateTodo` method tooset hello timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="41db1-212">Ondersteuning voor het nieuwe veld Hallo in Hallo Thymeleaf sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="41db1-212">Add support for hello new field in hello Thymeleaf template.</span></span> <span data-ttu-id="41db1-213">Update *src/main/resources/templates/index.html* met een nieuwe tabel-header voor Hallo tijdstempel, en een nieuwe toodisplay Hallo veldwaarde van Hallo tijdstempel in elke tabel gegevensrij.</span><span class="sxs-lookup"><span data-stu-id="41db1-213">Update *src/main/resources/templates/index.html* with a new table header for hello timestamp, and a new field toodisplay hello value of hello timestamp in each table data row.</span></span>

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. <span data-ttu-id="41db1-214">Hallo-toepassing bouwen:</span><span class="sxs-lookup"><span data-stu-id="41db1-214">Rebuild hello application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="41db1-215">FTP-hello bijgewerkt. WAR als voorheen kunt verwijderen van bestaande Hallo *site/wwwroot/webapps/ROOT* directory en *ROOT.war*, en vervolgens uploaden Hallo bijgewerkt. WAR-bestand als ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="41db1-215">FTP hello updated .WAR as before, removing hello existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading hello updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="41db1-216">Wanneer u Hallo-app vernieuwen een **Aanmaaktijd** kolom nu zichtbaar is.</span><span class="sxs-lookup"><span data-stu-id="41db1-216">When you refresh hello app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="41db1-217">Wanneer u een nieuwe taak toevoegt, wordt app Hallo Hallo tijdstempel automatisch gevuld.</span><span class="sxs-lookup"><span data-stu-id="41db1-217">When you add a new task, hello app will populate hello timestamp automatically.</span></span> <span data-ttu-id="41db1-218">Uw bestaande taken blijven ongewijzigd en werken met Hallo app Hoewel Hallo onderliggende gegevensmodel is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="41db1-218">Your existing tasks remain unchanged and work with hello app even though hello underlying data model has changed.</span></span> 

![Java-app bijgewerkt met een nieuwe kolom](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="41db1-220">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="41db1-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="41db1-221">Als uw Java-toepassing in Azure App Service wordt uitgevoerd, kunt u de console Hallo opvragen logboeken doorgesluisd rechtstreeks tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="41db1-221">While your Java application runs in Azure App Service, you can get hello console logs piped directly tooyour terminal.</span></span> <span data-ttu-id="41db1-222">Op die manier kunt u Hallo dezelfde diagnostische ontvangt toohelp foutopsporing van toepassingsfouten.</span><span class="sxs-lookup"><span data-stu-id="41db1-222">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="41db1-223">toostart logboek streaming gebruik Hallo [az webapp logboek tail](/cli/azure/appservice/web/log#tail) opdracht.</span><span class="sxs-lookup"><span data-stu-id="41db1-223">toostart log streaming, use hello [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="41db1-224">Uw Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="41db1-224">Manage your Azure web app</span></span>

<span data-ttu-id="41db1-225">Ga toohello Azure portal toosee Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="41db1-225">Go toohello Azure portal toosee hello web app you created.</span></span>

<span data-ttu-id="41db1-226">toodo dit te melden[https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="41db1-226">toodo this, sign in too[https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="41db1-227">In het linkermenu hello, klikt u op **App Service**, klikt u op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="41db1-227">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="41db1-229">Standaard ziet u uw web-app-blade Hallo **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="41db1-229">By default, your web app's blade shows hello **Overview** page.</span></span> <span data-ttu-id="41db1-230">Deze pagina geeft u een overzicht van hoe uw app presteert.</span><span class="sxs-lookup"><span data-stu-id="41db1-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="41db1-231">U kunt hier ook beheertaken zoals stoppen, starten, opnieuw opstarten en verwijderen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="41db1-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="41db1-232">Hallo tabbladen aan de linkerkant Hallo van Hallo blade bevatten Hallo verschillende configuratiepagina's die u kunt openen.</span><span class="sxs-lookup"><span data-stu-id="41db1-232">hello tabs on hello left side of hello blade show hello different configuration pages you can open.</span></span>

![App Service-blade in Azure Portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="41db1-234">Deze tabbladen Hallo blade bevatten Hallo vele handige functies u tooyour web-app kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="41db1-234">These tabs in hello blade show hello many great features you can add tooyour web app.</span></span> <span data-ttu-id="41db1-235">Hallo na lijst hebt u slechts een paar van Hallo mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="41db1-235">hello following list gives you just a few of hello possibilities:</span></span>
* <span data-ttu-id="41db1-236">Een aangepaste DNS-naam toewijzen</span><span class="sxs-lookup"><span data-stu-id="41db1-236">Map a custom DNS name</span></span>
* <span data-ttu-id="41db1-237">Een aangepast SSL-certificaat binden</span><span class="sxs-lookup"><span data-stu-id="41db1-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="41db1-238">Continue implementatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="41db1-238">Configure continuous deployment</span></span>
* <span data-ttu-id="41db1-239">Omhoog en omlaag schalen</span><span class="sxs-lookup"><span data-stu-id="41db1-239">Scale up and out</span></span>
* <span data-ttu-id="41db1-240">Gebruikersverificatie toevoegen</span><span class="sxs-lookup"><span data-stu-id="41db1-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="41db1-241">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="41db1-241">Clean up resources</span></span>

<span data-ttu-id="41db1-242">Als u deze resources niet voor een andere zelfstudie hoeft (Zie [Vervolgstappen](#next)), kunt u ze verwijderen door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="41db1-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running hello following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="41db1-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="41db1-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="41db1-244">Een MySQL-database maken in Azure</span><span class="sxs-lookup"><span data-stu-id="41db1-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="41db1-245">Verbinding maken met een steekproef Java app toohello MySQL</span><span class="sxs-lookup"><span data-stu-id="41db1-245">Connect a sample Java app toohello MySQL</span></span>
> * <span data-ttu-id="41db1-246">Hallo app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="41db1-246">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="41db1-247">Bijwerken en het Hallo-app implementeren</span><span class="sxs-lookup"><span data-stu-id="41db1-247">Update and redeploy hello app</span></span>
> * <span data-ttu-id="41db1-248">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="41db1-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="41db1-249">Hallo-app in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="41db1-249">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="41db1-250">De volgende zelfstudie toolearn toohello gaan hoe een aangepaste DNS-server toomap toohello app name.</span><span class="sxs-lookup"><span data-stu-id="41db1-250">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="41db1-251">Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="41db1-251">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
