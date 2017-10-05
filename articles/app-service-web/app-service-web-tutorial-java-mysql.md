---
title: Een Java- en MySQL web-app in Azure bouwen
description: Informatie over het ophalen van een Java-app die is verbonden met de Azure MySQL-database-service in Azure App service werkt.
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
ms.openlocfilehash: eb2d59939c4e4486bb14bb143a4a18f9bc1478e1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a><span data-ttu-id="4b9e4-103">Een Java- en MySQL web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-103">Build a Java and MySQL web app in Azure</span></span>

<span data-ttu-id="4b9e4-104">Deze zelfstudie laat zien hoe u een Java-web-app in Azure maken en te verbinden met een MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-104">This tutorial shows you how to create a Java web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="4b9e4-105">Wanneer u klaar bent, hebt u een [Spring Boot](https://projects.spring.io/spring-boot/) toepassing opslaan van gegevens in [Azure Database voor MySQL](https://docs.microsoft.com/azure/mysql/overview) uitgevoerd op [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="4b9e4-105">When you are finished, you will have a [Spring Boot](https://projects.spring.io/spring-boot/) application storing data in [Azure Database for MySQL](https://docs.microsoft.com/azure/mysql/overview) running on [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).</span></span>

![Java-app uitgevoerd in Azure App service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="4b9e4-107">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b9e4-108">Een MySQL-database maken in Azure</span><span class="sxs-lookup"><span data-stu-id="4b9e4-108">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="4b9e4-109">Een voorbeeld-app verbinden met de database</span><span class="sxs-lookup"><span data-stu-id="4b9e4-109">Connect a sample app to the database</span></span>
> * <span data-ttu-id="4b9e4-110">De app implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="4b9e4-110">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4b9e4-111">De app bijwerken en opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-111">Update and redeploy the app</span></span>
> * <span data-ttu-id="4b9e4-112">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="4b9e4-112">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="4b9e4-113">De app in de Azure portal controleren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-113">Monitor the app in the Azure portal</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4b9e4-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4b9e4-114">Prerequisites</span></span>

1. [<span data-ttu-id="4b9e4-115">Download en installeer Git</span><span class="sxs-lookup"><span data-stu-id="4b9e4-115">Download and install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="4b9e4-116">Download en installeer de JDK die Java 7 of hoger</span><span class="sxs-lookup"><span data-stu-id="4b9e4-116">Download and install the Java 7 JDK or above</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [<span data-ttu-id="4b9e4-117">Downloaden, installeren en starten van MySQL</span><span class="sxs-lookup"><span data-stu-id="4b9e4-117">Download, install, and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4b9e4-118">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-118">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4b9e4-119">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-119">Run `az --version` to find the version.</span></span> <span data-ttu-id="4b9e4-120">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4b9e4-120">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-local-mysql"></a><span data-ttu-id="4b9e4-121">Lokale MySQL voorbereiden</span><span class="sxs-lookup"><span data-stu-id="4b9e4-121">Prepare local MySQL</span></span> 

<span data-ttu-id="4b9e4-122">In deze stap maakt u een database in een lokale MySQL-server voor gebruik in de app lokaal op uw computer te testen.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-122">In this step, you create a database in a local MySQL server for use in testing the app locally on your machine.</span></span>

### <a name="connect-to-mysql-server"></a><span data-ttu-id="4b9e4-123">Verbinding maken met de MySQL-server</span><span class="sxs-lookup"><span data-stu-id="4b9e4-123">Connect to MySQL server</span></span>

<span data-ttu-id="4b9e4-124">In een terminalvenster verbinding maken met uw lokale MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-124">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="4b9e4-125">Alle opdrachten kunt uitvoeren in deze zelfstudie kunt u deze terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-125">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="4b9e4-126">Als u wordt gevraagd om een wachtwoord, voert u het wachtwoord voor de `root` account.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-126">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="4b9e4-127">Als je het wachtwoord van je root-account, Zie [MySQL: het opnieuw instellen van het hoofdwachtwoord](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="4b9e4-127">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="4b9e4-128">Als uw opdracht is uitgevoerd, wordt al uw MySQL-server uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-128">If your command runs successfully, then your MySQL server is already running.</span></span> <span data-ttu-id="4b9e4-129">Als dit niet het geval is, zorg ervoor dat de lokale MySQL-server is gestart door de [MySQL na de installatie stappen](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="4b9e4-129">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database"></a><span data-ttu-id="4b9e4-130">Een database maken</span><span class="sxs-lookup"><span data-stu-id="4b9e4-130">Create a database</span></span> 

<span data-ttu-id="4b9e4-131">In de `mysql` vragen, maakt u een database en een tabel voor de taakitems.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-131">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

<span data-ttu-id="4b9e4-132">Uw serververbinding sluiten door te typen `quit`.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-132">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="create-and-run-the-sample-app"></a><span data-ttu-id="4b9e4-133">Maken en uitvoeren van de voorbeeld-app</span><span class="sxs-lookup"><span data-stu-id="4b9e4-133">Create and run the sample app</span></span> 

<span data-ttu-id="4b9e4-134">In deze stap voorbeeldapp Spring opstarten klonen, configureert voor het gebruik van de lokale MySQL-database en uitvoeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-134">In this step, you clone sample Spring boot app, configure it to use the local MySQL database, and run it on your computer.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="4b9e4-135">Klonen van de steekproef</span><span class="sxs-lookup"><span data-stu-id="4b9e4-135">Clone the sample</span></span>

<span data-ttu-id="4b9e4-136">Navigeer naar een werkmap in een terminalvenster en kloon de opslagplaats voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-136">In the terminal window, navigate to a working directory and clone the sample repository.</span></span> 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-the-app-to-use-the-mysql-database"></a><span data-ttu-id="4b9e4-137">De app voor het gebruik van de MySQL-database configureren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-137">Configure the app to use the MySQL database</span></span>

<span data-ttu-id="4b9e4-138">Update de `spring.datasource.password` en de waarde *spring-boot-mysql-todo/src/main/resources/application.properties* met hetzelfde root-wachtwoord gebruikt om de MySQL-prompt te openen:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-138">Update the `spring.datasource.password` and  value in *spring-boot-mysql-todo/src/main/resources/application.properties* with the same root password used to open the MySQL prompt:</span></span>

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-the-sample"></a><span data-ttu-id="4b9e4-139">Bouwen en uitvoeren van de steekproef</span><span class="sxs-lookup"><span data-stu-id="4b9e4-139">Build and run the sample</span></span>

<span data-ttu-id="4b9e4-140">Bouwen en uitvoeren van het voorbeeld met de Maven-wrapper die is opgenomen in de opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-140">Build and run the sample using the Maven wrapper included in the repo:</span></span>

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

<span data-ttu-id="4b9e4-141">Open uw browser naar http://localhost: 8080 om te zien in het voorbeeld in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-141">Open your browser to http://localhost:8080 to see in the sample in action.</span></span> <span data-ttu-id="4b9e4-142">Zoals u taken aan de lijst toevoegen, gebruikt u de volgende SQL-opdrachten in de MySQL-prompt om de gegevens die zijn opgeslagen in de MySQL weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-142">As you add tasks to the list,  use the following SQL commands in the MySQL prompt to view the data stored in MySQL.</span></span>

```SQL
use testdb;
select * from todo_item;
```

<span data-ttu-id="4b9e4-143">Stop de toepassing te raken `Ctrl` + `C` in de terminal.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-143">Stop the application by hitting `Ctrl`+`C` in the terminal.</span></span> 

## <a name="create-an-azure-mysql-database"></a><span data-ttu-id="4b9e4-144">Een Azure-MySQL-database maken</span><span class="sxs-lookup"><span data-stu-id="4b9e4-144">Create an Azure MySQL database</span></span>

<span data-ttu-id="4b9e4-145">In deze stap maakt u een [Azure Database voor MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instantie met de [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4b9e4-145">In this step, you create an [Azure Database for MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) instance using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="4b9e4-146">U configureert de voorbeeldtoepassing later op deze database gebruiken in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-146">You configure the sample application to use this database later on in the tutorial.</span></span>

<span data-ttu-id="4b9e4-147">Gebruik de Azure CLI 2.0 in een terminalvenster te maken van de bronnen die nodig zijn voor het hosten van uw Java-toepassing in Azure App service.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-147">Use the Azure CLI 2.0 in a terminal window to create the resources needed to host your Java application in Azure appservice.</span></span> <span data-ttu-id="4b9e4-148">Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="4b9e4-149">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="4b9e4-149">Create a resource group</span></span>

<span data-ttu-id="4b9e4-150">Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) met de [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="4b9e4-151">Een Azure-resourcegroep is een logische container waar verwante resources, zoals web-apps, databases en storage-accounts worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-151">An Azure resource group is a logical container where related resources like web apps, databases, and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="4b9e4-152">Het volgende voorbeeld maakt een resourcegroep in de regio Noord-Europa:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-152">The following example creates a resource group in the North Europe region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

<span data-ttu-id="4b9e4-153">Om te zien van de mogelijke waarden die u hebt, kunnen gebruiken voor `--location`, gebruiken de [az appservice lijst-locaties](/cli/azure/appservice#list-locations) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-153">To see the possible values you can use for `--location`, use the [az appservice list-locations](/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-a-mysql-server"></a><span data-ttu-id="4b9e4-154">Een MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="4b9e4-154">Create a MySQL server</span></span>

<span data-ttu-id="4b9e4-155">Een server in Azure-Database voor MySQL (Preview) te maken met de [az mysql-server maken](/cli/azure/mysql/server#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-155">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>    
<span data-ttu-id="4b9e4-156">Vervangen door uw eigen unieke MySQL-servernaam waarin u zien hoe de `<mysql_server_name>` tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-156">Substitute your own unique MySQL server name where you see the `<mysql_server_name>` placeholder.</span></span> <span data-ttu-id="4b9e4-157">Deze naam maakt deel uit van de hostnaam van uw MySQL-server, `<mysql_server_name>.mysql.database.azure.com`, zodat het moet globaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-157">This name is part of your MySQL server's hostname, `<mysql_server_name>.mysql.database.azure.com`, so it needs to be globally unique.</span></span> <span data-ttu-id="4b9e4-158">Ook vervangen `<admin_user>` en `<admin_password>` met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-158">Also substitute `<admin_user>` and `<admin_password>` with your own values.</span></span>

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

<span data-ttu-id="4b9e4-159">Wanneer de MySQL-server is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-159">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="4b9e4-160">Een firewall configureren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-160">Configure server firewall</span></span>

<span data-ttu-id="4b9e4-161">Maken van een firewallregel voor uw MySQL-server clientverbindingen toestaat met behulp van de [az mysql server-firewallregel maken](/cli/azure/mysql/server/firewall-rule#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-161">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span> 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="4b9e4-162">Azure-Database voor MySQL (Preview) kunnen niet automatisch momenteel verbindingen van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-162">Azure Database for MySQL (Preview) does not currently automatically enable connections from Azure services.</span></span> <span data-ttu-id="4b9e4-163">Als het IP-adressen in Azure worden dynamisch toegewezen, is het beter om alle IP-adressen inschakelen voor nu.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-163">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses for now.</span></span> <span data-ttu-id="4b9e4-164">Wanneer de service de preview blijft, kunt u betere methoden voor het beveiligen van uw database wordt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-164">As the service continues its preview, better methods for securing your database will be enabled.</span></span>

## <a name="configure-the-azure-mysql-database"></a><span data-ttu-id="4b9e4-165">De Azure MySQL-database configureren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-165">Configure the Azure MySQL database</span></span>

<span data-ttu-id="4b9e4-166">In het terminalvenster op uw computer verbinding maken met de server MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-166">In the terminal window on your computer, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="4b9e4-167">Gebruik de waarde die u eerder hebt opgegeven voor `<admin_user>` en `<mysql_server_name>`.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-167">Use the value you specified previously for `<admin_user>` and `<mysql_server_name>`.</span></span>

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a><span data-ttu-id="4b9e4-168">Een database maken</span><span class="sxs-lookup"><span data-stu-id="4b9e4-168">Create a database</span></span> 

<span data-ttu-id="4b9e4-169">In de `mysql` vragen, maakt u een database en een tabel voor de taakitems.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-169">In the `mysql` prompt, create a database and a table for the to-do items.</span></span>

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="4b9e4-170">Een gebruiker met machtigingen maken</span><span class="sxs-lookup"><span data-stu-id="4b9e4-170">Create a user with permissions</span></span>

<span data-ttu-id="4b9e4-171">Een databasegebruiker maken en hieraan alle bevoegdheden de `tododb` database.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-171">Create a database user and give it all privileges in the `tododb` database.</span></span> <span data-ttu-id="4b9e4-172">Vervang de tijdelijke aanduidingen `<Javaapp_user>` en `<Javaapp_password>` met uw eigen unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-172">Replace the placeholders `<Javaapp_user>` and `<Javaapp_password>` with your own unique app name.</span></span>

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* TO '<Javaapp_user>';
```

<span data-ttu-id="4b9e4-173">Uw serververbinding sluiten door te typen `quit`.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-173">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="deploy-the-sample-to-azure-app-service"></a><span data-ttu-id="4b9e4-174">Het voorbeeld in Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-174">Deploy the sample to Azure App Service</span></span>

<span data-ttu-id="4b9e4-175">Maken van een Azure App Service-abonnement met de **vrije** prijzen met behulp van laag de [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-175">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="4b9e4-176">Het plan appservice definieert de fysieke resources gebruikt voor het hosten van uw apps.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-176">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="4b9e4-177">Alle toepassingen die zijn toegewezen aan een appservice-abonnement kunt u deze resources, zodat u kosten opslaan bij het hosten van meerdere apps delen.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-177">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="4b9e4-178">Wanneer het plan klaar is, ziet u de Azure CLI vergelijkbare uitvoer naar het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-178">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="4b9e4-179">Een Azure-Web-app maken</span><span class="sxs-lookup"><span data-stu-id="4b9e4-179">Create an Azure Web app</span></span>

 <span data-ttu-id="4b9e4-180">Gebruik de [az webapp maken](/cli/azure/appservice/web#create) CLI-opdracht voor het maken van de definitie van een web-app in de `myAppServicePlan` App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-180">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="4b9e4-181">De definitie van de web-app biedt een URL voor toegang tot uw toepassing met en configureert u diverse opties voor het implementeren van uw code naar Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-181">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="4b9e4-182">Vervang de `<app_name>` aanduiding voor items met uw eigen unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-182">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="4b9e4-183">Deze unieke naam maakt deel uit van de standaard-domeinnaam voor de web-app zodat de naam moet uniek zijn in alle apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-183">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="4b9e4-184">Voordat u het beschikbaar aan uw gebruikers stellen, kunt u een vermelding van de naam van aangepast domein toewijzen aan de web-app.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-184">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="4b9e4-185">Wanneer de definitie van de web-app klaar is, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-185">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="4b9e4-186">Java configureren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-186">Configure Java</span></span> 

<span data-ttu-id="4b9e4-187">Instellen van de Java runtime-configuratie die uw app met moet de [az appservice web config update](/cli/azure/appservice/web/config#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-187">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="4b9e4-188">De volgende opdracht configureert u de web-app uit te voeren op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-188">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-the-app-to-use-the-azure-sql-database"></a><span data-ttu-id="4b9e4-189">De app voor het gebruik van de Azure SQL database configureren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-189">Configure the app to use the Azure SQL database</span></span>

<span data-ttu-id="4b9e4-190">Voordat u de voorbeeld-app, stelt u toepassingsinstellingen op de web-app de Azure-MySQL-database die u hebt gemaakt in Azure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-190">Before running the sample app, set application settings on the web app to use the Azure MySQL database you created in Azure.</span></span> <span data-ttu-id="4b9e4-191">Deze eigenschappen worden blootgesteld aan de webtoepassing als omgevingsvariabelen en de waarden in de application.properties binnen de verpakte web-app overschreven.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-191">These properties are exposed to the web application as environment variables and override the values set in the application.properties inside the packaged web app.</span></span> 

<span data-ttu-id="4b9e4-192">Toepassingsinstellingen met [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in de CLI:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-192">Set application settings using [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in the CLI:</span></span>

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

### <a name="get-ftp-deployment-credentials"></a><span data-ttu-id="4b9e4-193">FTP-implementatiereferenties ophalen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-193">Get FTP deployment credentials</span></span> 
<span data-ttu-id="4b9e4-194">U kunt uw toepassing in Azure App service op verschillende manieren, met inbegrip van de FTP-, lokale Git, GitHub, Visual Studio Team Services en BitBucket implementeren.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-194">You can deploy your application to Azure appservice in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="4b9e4-195">In dit voorbeeld FTP voor het implementeren van de. WAR-bestand is gebouwd eerder op uw lokale machine in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-195">For this example, FTP to deploy the .WAR file built previously on your local machine to Azure App Service.</span></span>

<span data-ttu-id="4b9e4-196">Gebruiken om te bepalen wat referenties door te geven in een FTP-opdracht in de Web-App, [implementatie in az appservice web-lijst-publicatie-profielen](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) opdracht:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-196">To determine what credentials to pass along in an ftp command to the Web App, Use [az appservice web deployment list-publishing-profiles](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) command:</span></span> 

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

### <a name="upload-the-app-using-ftp"></a><span data-ttu-id="4b9e4-197">Uploaden van de app met FTP</span><span class="sxs-lookup"><span data-stu-id="4b9e4-197">Upload the app using FTP</span></span>

<span data-ttu-id="4b9e4-198">Uw favoriete FTP-hulpprogramma gebruiken voor het implementeren van de. WAR-bestand in de */site/wwwroot/webapps* map op het adres van de server die afkomstig zijn uit de `URL` veld in de vorige opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-198">Use your favorite FTP tool to deploy the .WAR file to the */site/wwwroot/webapps* folder on the server address taken from the `URL` field in the previous command.</span></span> <span data-ttu-id="4b9e4-199">Verwijder de bestaande map van de standaard (ROOT)-toepassing en vervang de bestaande ROOT.war met de. WAR-bestand in de eerder in de zelfstudie wordt gebouwd.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-199">Remove the existing default (ROOT) application directory and replace the existing ROOT.war with the .WAR file built in the earlier in the tutorial.</span></span>

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected to waws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-the-web-app"></a><span data-ttu-id="4b9e4-200">De web-app testen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-200">Test the web app</span></span>

<span data-ttu-id="4b9e4-201">Blader naar `http://<app_name>.azurewebsites.net/` en een paar taken toevoegen aan de lijst.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-201">Browse to `http://<app_name>.azurewebsites.net/` and add a few tasks to the list.</span></span> 

![Java-app uitgevoerd in Azure App service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

<span data-ttu-id="4b9e4-203">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="4b9e4-203">**Congratulations!**</span></span> <span data-ttu-id="4b9e4-204">U uitvoert een Java-gegevensgestuurde app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-204">You're running a data-driven Java app in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="4b9e4-205">De app bijwerken en opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-205">Update the app and redeploy</span></span>

<span data-ttu-id="4b9e4-206">Bijwerken van de toepassing te nemen van een extra kolom in de takenlijst voor welke dag het item is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-206">Update the application to include an additional column in the todo list for what day the item was created.</span></span> <span data-ttu-id="4b9e4-207">Spring opstarten verwerkt het databaseschema bijwerken voor u als de wijzigingen in het gegevensmodel zonder uw bestaande databaserecords zelf te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-207">Spring Boot handles updating the database schema for you as the data model changes without altering your existing database records.</span></span>

1. <span data-ttu-id="4b9e4-208">Open op uw lokale systeem *src/main/java/com/example/fabrikam/TodoItem.java* en voeg de volgende import toe aan de klasse:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-208">On your local system, open up *src/main/java/com/example/fabrikam/TodoItem.java* and add the following imports to the class:</span></span>   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. <span data-ttu-id="4b9e4-209">Voeg een `String` eigenschap `timeCreated` naar *src/main/java/com/example/fabrikam/TodoItem.java*, deze met een tijdstempel bij het maken van een object te initialiseren.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-209">Add a `String` property `timeCreated` to *src/main/java/com/example/fabrikam/TodoItem.java*, initializing it with a timestamp at object creation.</span></span> <span data-ttu-id="4b9e4-210">Getters/setters toevoegen voor de nieuwe `timeCreated` eigenschap tijdens het bewerken van dit bestand.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-210">Add getters/setters for the new `timeCreated` property while you are editing this file.</span></span>

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

3. <span data-ttu-id="4b9e4-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* met een regel in de `updateTodo` methode om in te stellen de tijdstempel:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-211">Update *src/main/java/com/example/fabrikam/TodoDemoController.java* with a line in the `updateTodo` method to set the timestamp:</span></span>

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. <span data-ttu-id="4b9e4-212">Ondersteuning voor het nieuwe veld in de sjabloon Thymeleaf toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-212">Add support for the new field in the Thymeleaf template.</span></span> <span data-ttu-id="4b9e4-213">Update *src/main/resources/templates/index.html* met een nieuwe tabel-header voor het tijdstempel en een nieuw veld om de waarde van het tijdstempel in elke tabelrij gegevens weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-213">Update *src/main/resources/templates/index.html* with a new table header for the timestamp, and a new field to display the value of the timestamp in each table data row.</span></span>

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

5. <span data-ttu-id="4b9e4-214">De toepassing bouwen:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-214">Rebuild the application:</span></span>

    ```bash
    mvnw clean package 
    ```

6. <span data-ttu-id="4b9e4-215">FTP-de update. WAR als voorheen kunt u verwijdert de bestaande *site/wwwroot/webapps/ROOT* directory en *ROOT.war*, en vervolgens de bijgewerkte uploaden. WAR-bestand als ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-215">FTP the updated .WAR as before, removing the existing *site/wwwroot/webapps/ROOT* directory and *ROOT.war*, then uploading the updated .WAR file as ROOT.war.</span></span> 

<span data-ttu-id="4b9e4-216">Bij het vernieuwen van de app een **Aanmaaktijd** kolom nu zichtbaar is.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-216">When you refresh the app, a **Time Created** column is now visible.</span></span> <span data-ttu-id="4b9e4-217">Wanneer u een nieuwe taak toevoegt, wordt de app de tijdstempel automatisch gevuld.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-217">When you add a new task, the app will populate the timestamp automatically.</span></span> <span data-ttu-id="4b9e4-218">Uw bestaande taken blijven ongewijzigd en werken met de app, zelfs als het onderliggende gegevensmodel is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-218">Your existing tasks remain unchanged and work with the app even though the underlying data model has changed.</span></span> 

![Java-app bijgewerkt met een nieuwe kolom](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a><span data-ttu-id="4b9e4-220">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="4b9e4-220">Stream diagnostic logs</span></span> 

<span data-ttu-id="4b9e4-221">Als uw Java-toepassing in Azure App Service wordt uitgevoerd, kunt u de logboeken van de console doorgesluisd rechtstreeks aan uw terminal opvragen.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-221">While your Java application runs in Azure App Service, you can get the console logs piped directly to your terminal.</span></span> <span data-ttu-id="4b9e4-222">Op die manier kunt u de dezelfde diagnostische berichten op te sporen toepassingsfouten ophalen.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-222">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="4b9e4-223">Gebruik voor het starten van de streaming-logboek de [az webapp logboek tail](/cli/azure/appservice/web/log#tail) opdracht.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-223">To start log streaming, use the [az webapp log tail](/cli/azure/appservice/web/log#tail) command.</span></span>

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="4b9e4-224">Uw Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-224">Manage your Azure web app</span></span>

<span data-ttu-id="4b9e4-225">Ga naar de Azure-portal om te zien van de web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-225">Go to the Azure portal to see the web app you created.</span></span>

<span data-ttu-id="4b9e4-226">Hiervoor moet u zich aanmelden bij [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b9e4-226">To do this, sign in to [https://portal.azure.com](https://portal.azure.com).</span></span>

<span data-ttu-id="4b9e4-227">Klik vanuit het linkermenu op **App Service** en klik op de naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-227">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-tutorial-java-mysql/access-portal.png)

<span data-ttu-id="4b9e4-229">Standaard toont de blade van uw web-app de pagina **Overzicht**.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-229">By default, your web app's blade shows the **Overview** page.</span></span> <span data-ttu-id="4b9e4-230">Deze pagina geeft u een overzicht van hoe uw app presteert.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-230">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="4b9e4-231">U kunt hier ook beheertaken zoals stoppen, starten, opnieuw opstarten en verwijderen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-231">Here, you can also perform management tasks like stop, start, restart, and delete.</span></span> <span data-ttu-id="4b9e4-232">De tabbladen aan de linkerkant van de blade tonen de verschillende configuratiepagina's die u kunt openen.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-232">The tabs on the left side of the blade show the different configuration pages you can open.</span></span>

![App Service-blade in Azure Portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

<span data-ttu-id="4b9e4-234">Deze tabbladen op de blade bevatten de vele handige functies die kunt u toevoegen aan uw web-app.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-234">These tabs in the blade show the many great features you can add to your web app.</span></span> <span data-ttu-id="4b9e4-235">De volgende lijst bevat slechts enkele van de mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-235">The following list gives you just a few of the possibilities:</span></span>
* <span data-ttu-id="4b9e4-236">Een aangepaste DNS-naam toewijzen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-236">Map a custom DNS name</span></span>
* <span data-ttu-id="4b9e4-237">Een aangepast SSL-certificaat binden</span><span class="sxs-lookup"><span data-stu-id="4b9e4-237">Bind a custom SSL certificate</span></span>
* <span data-ttu-id="4b9e4-238">Continue implementatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-238">Configure continuous deployment</span></span>
* <span data-ttu-id="4b9e4-239">Omhoog en omlaag schalen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-239">Scale up and out</span></span>
* <span data-ttu-id="4b9e4-240">Gebruikersverificatie toevoegen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-240">Add user authentication</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="4b9e4-241">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-241">Clean up resources</span></span>

<span data-ttu-id="4b9e4-242">Als u deze resources niet voor een andere zelfstudie hoeft (Zie [Vervolgstappen](#next)), kunt u ze verwijderen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4b9e4-242">If you don't need these resources for another tutorial (see [Next steps](#next)), you can delete them by running the following command:</span></span> 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="4b9e4-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b9e4-243">Next steps</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b9e4-244">Een MySQL-database maken in Azure</span><span class="sxs-lookup"><span data-stu-id="4b9e4-244">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="4b9e4-245">Een voorbeeld Java-app verbinden met de MySQL</span><span class="sxs-lookup"><span data-stu-id="4b9e4-245">Connect a sample Java app to the MySQL</span></span>
> * <span data-ttu-id="4b9e4-246">De app implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="4b9e4-246">Deploy the app to Azure</span></span>
> * <span data-ttu-id="4b9e4-247">De app bijwerken en opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-247">Update and redeploy the app</span></span>
> * <span data-ttu-id="4b9e4-248">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="4b9e4-248">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="4b9e4-249">De app in de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="4b9e4-249">Manage the app in the Azure portal</span></span>

<span data-ttu-id="4b9e4-250">Ga naar de volgende zelfstudie voor informatie over het toewijzen van een aangepaste DNS-naam naar de app.</span><span class="sxs-lookup"><span data-stu-id="4b9e4-250">Advance to the next tutorial to learn how to map a custom DNS name to the app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="4b9e4-251">Een bestaande aangepaste DNS-naam toewijzen aan Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="4b9e4-251">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)