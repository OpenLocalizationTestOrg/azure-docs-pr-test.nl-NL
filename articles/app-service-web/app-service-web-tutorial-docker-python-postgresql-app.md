---
title: Een Docker Python en PostgreSQL web-app in Azure bouwen | Microsoft Docs
description: Informatie over het ophalen van een Docker-Python-app in Azure, werkt met verbinding met een PostgreSQL-database.
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e70f85a1eb4a6e1a81e0ca4fae228ca97deca6fe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="e2b7e-103">Een Docker Python en PostgreSQL web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="e2b7e-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="e2b7e-104">Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e2b7e-105">Deze zelfstudie laat zien hoe een eenvoudige Docker Python-web-app maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-105">This tutorial shows how to create a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="e2b7e-106">U hebt deze app verbinding maken met een PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-106">You'll connect this app to a PostgreSQL database.</span></span> <span data-ttu-id="e2b7e-107">Wanneer u bent klaar, hebt u een Python Flask-toepassing uitgevoerd binnen een Docker-container op [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e2b7e-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Docker Python Flask-app in Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="e2b7e-109">U kunt de onderstaande stappen volgen op Mac OS.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-109">You can follow the steps below on macOS.</span></span> <span data-ttu-id="e2b7e-110">Linux- en Windows-instructies zijn hetzelfde in de meeste gevallen, maar de verschillen worden niet beschreven in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-110">Linux and Windows instructions are the same in most cases, but the differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="e2b7e-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2b7e-111">Prerequisites</span></span>

<span data-ttu-id="e2b7e-112">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-112">To complete this tutorial:</span></span>

1. [<span data-ttu-id="e2b7e-113">Git installeren</span><span class="sxs-lookup"><span data-stu-id="e2b7e-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="e2b7e-114">Python installeren</span><span class="sxs-lookup"><span data-stu-id="e2b7e-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="e2b7e-115">Installeren en uitvoeren van PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e2b7e-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="e2b7e-116">Docker-Community Edition installeren</span><span class="sxs-lookup"><span data-stu-id="e2b7e-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e2b7e-117">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-117">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e2b7e-118">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="e2b7e-119">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e2b7e-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="e2b7e-120">Lokale PostgreSQL-installatie testen en een database maken</span><span class="sxs-lookup"><span data-stu-id="e2b7e-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="e2b7e-121">Open het terminalvenster en voer `psql postgres` verbinding maken met uw lokale PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-121">Open the terminal window and run `psql postgres` to connect to your local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="e2b7e-122">Als de verbinding geslaagd is, wordt uw PostgreSQL-database wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="e2b7e-123">Als dit niet het geval is, zorg ervoor dat de lokale PostgresQL-database is gestart door de stappen op [Downloads - PostgreSQL Core distributie](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="e2b7e-123">If not, make sure that your local PostgresQL database is started by following the steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="e2b7e-124">Maken van een database met de naam *eventregistration* en instellen van de gebruiker van een aparte database met de naam *manager* met wachtwoord *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```
<span data-ttu-id="e2b7e-125">Type *\q* om af te sluiten van de PostgreSQL-client.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-125">Type *\q* to exit the PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="e2b7e-126">Lokale Python Flask-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="e2b7e-126">Create local Python Flask application</span></span>

<span data-ttu-id="e2b7e-127">In deze stap moet u het lokale Python Flask-project instellen.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-127">In this step, you set up the local Python Flask project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="e2b7e-128">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="e2b7e-128">Clone the sample application</span></span>

<span data-ttu-id="e2b7e-129">Open een terminalvenster en `CD` in een werkmap.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-129">Open the terminal window, and `CD` to a working directory.</span></span>  

<span data-ttu-id="e2b7e-130">Voer de volgende opdrachten de voorbeeld-opslagplaats klonen en gaat u naar de *0,1 initialapp* release.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-130">Run the following commands to clone the sample repository and go to the *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="e2b7e-131">Deze repository voorbeeld bevat een [Flask](http://flask.pocoo.org/) toepassing.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-the-application"></a><span data-ttu-id="e2b7e-132">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e2b7e-132">Run the application</span></span>

> [!NOTE] 
> <span data-ttu-id="e2b7e-133">In een latere stap kunt u dit proces met het bouwen van een Docker-container voor gebruik met de productiedatabase vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-133">In a later step you simplify this process by building a Docker container to use with the production database.</span></span>

<span data-ttu-id="e2b7e-134">Installeer de vereiste pakketten en start de toepassing.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-134">Install the required packages and start the application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="e2b7e-135">Wanneer de app volledig wordt geladen is, ziet u iets soortgelijks als in het volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-135">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="e2b7e-136">Ga naar http://127.0.0.1:5000 in een browser.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-136">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="e2b7e-137">Klik op **registreren!**</span><span class="sxs-lookup"><span data-stu-id="e2b7e-137">Click **Register!**</span></span> <span data-ttu-id="e2b7e-138">en een testgebruiker maken.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-138">and create a test user.</span></span>

![Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="e2b7e-140">De voorbeeldtoepassing Flask slaat gebruikersgegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-140">The Flask sample application stores user data in the database.</span></span> <span data-ttu-id="e2b7e-141">Als u succesvol bij het registreren van een gebruiker, wordt uw app schrijven van gegevens naar de lokale PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-141">If you are successful at registering a user, your app is writing data to the local PostgreSQL database.</span></span>

<span data-ttu-id="e2b7e-142">Als u wilt de Flask-server op elk gewenst moment stoppen, typt u Ctrl + C in de terminal.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-142">To stop the Flask server at anytime, type Ctrl+C in the terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="e2b7e-143">Een productie-PostgreSQL-database maken</span><span class="sxs-lookup"><span data-stu-id="e2b7e-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="e2b7e-144">In deze stap maakt u een PostgreSQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="e2b7e-145">Wanneer uw app wordt geïmplementeerd naar Azure, wordt deze cloud-database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-145">When your app is deployed to Azure, it will use this cloud database.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="e2b7e-146">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-146">Log in to Azure</span></span>

<span data-ttu-id="e2b7e-147">Nu gaat u de Azure CLI 2.0 gebruiken om de resources die nodig zijn voor het hosten van uw toepassing Python in Azure App Service te maken.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-147">You are now going to use the Azure CLI 2.0 to create the resources needed to host your Python application in Azure App Service.</span></span>  <span data-ttu-id="e2b7e-148">Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-148">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="e2b7e-149">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="e2b7e-149">Create a resource group</span></span>

<span data-ttu-id="e2b7e-150">Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e2b7e-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with the [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="e2b7e-151">Het volgende voorbeeld maakt een resourcegroep in de regio VS-West:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-151">The following example creates a resource group in the West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="e2b7e-152">Gebruik de [az appservice lijst-locaties](/cli/azure/appservice#list-locations) Azure CLI-opdracht naar de lijst met beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-152">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="e2b7e-153">Een Azure-database voor PostgreSQL-server maken</span><span class="sxs-lookup"><span data-stu-id="e2b7e-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="e2b7e-154">Maak een PostgreSQL-server met de [az postgres server maken](/cli/azure/documentdb#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-154">Create a PostgreSQL server with the [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="e2b7e-155">In de volgende opdracht te vervangen door een unieke naam voor de  *\<postgresql_name >* tijdelijke aanduiding en een gebruiker een naam voor de  *\<admin_username >* tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-155">In the following command, substitute a unique server name for the *\<postgresql_name>* placeholder and a user name for the *\<admin_username>* placeholder.</span></span> <span data-ttu-id="e2b7e-156">Naam van de server wordt gebruikt als onderdeel van uw eindpunt PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), zodat de naam moet uniek zijn in alle servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-156">The server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so the name needs to be unique across all servers in Azure.</span></span> <span data-ttu-id="e2b7e-157">De gebruikersnaam is voor de gebruikersaccount van de oorspronkelijke database-beheerder.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-157">The user name is for the initial database admin user account.</span></span> <span data-ttu-id="e2b7e-158">U wordt gevraagd een wachtwoord voor deze gebruiker kiest.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-158">You are prompted to pick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="e2b7e-159">Wanneer de Azure-Database voor PostgreSQL-server is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-159">When the Azure Database for PostgreSQL server is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-the-azure-database-for-postgresql-server"></a><span data-ttu-id="e2b7e-160">Een firewallregel maken voor de Azure-Database voor PostgreSQL-server</span><span class="sxs-lookup"><span data-stu-id="e2b7e-160">Create a firewall rule for the Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="e2b7e-161">Voer de volgende opdracht in de Azure CLI om toegang te verlenen tot de database van alle IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-161">Run the following Azure CLI command to allow access to the database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="e2b7e-162">De Azure CLI bevestigt de firewall-regel maken met de uitvoer lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-162">The Azure CLI confirms the firewall rule creation with output similar to the following example:</span></span>

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-to-the-database"></a><span data-ttu-id="e2b7e-163">Verbinding maken met uw Python Flask-toepassing met de database</span><span class="sxs-lookup"><span data-stu-id="e2b7e-163">Connect your Python Flask application to the database</span></span>

<span data-ttu-id="e2b7e-164">In deze stap maakt u verbinding maken uw Python Flask-voorbeeldtoepassing voor de Azure-Database voor PostgreSQL-server die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-164">In this step, you connect your Python Flask sample application to the Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="e2b7e-165">Een lege database maken en een nieuwe gebruiker van de database-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="e2b7e-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="e2b7e-166">Maak een databasegebruiker met toegang tot één database.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-166">Create a database user with access to a single database only.</span></span> <span data-ttu-id="e2b7e-167">U gebruikt deze referenties om te voorkomen dat de toepassing volledige toegang geven tot de server.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-167">You'll use these credentials to avoid giving the application full access to the server.</span></span>

<span data-ttu-id="e2b7e-168">Verbinding maken met de database (u wordt gevraagd om uw wachtwoord admin).</span><span class="sxs-lookup"><span data-stu-id="e2b7e-168">Connect to the database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="e2b7e-169">De database en de gebruiker van de CLI PostgreSQL maken.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-169">Create the database and user from the PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration TO manager;
```

<span data-ttu-id="e2b7e-170">Type *\q* om af te sluiten van de PostgreSQL-client.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-170">Type *\q* to exit the PostgreSQL client.</span></span>

### <a name="test-the-application-locally-against-the-azure-postgresql-database"></a><span data-ttu-id="e2b7e-171">Test de toepassing lokaal op de Azure-PostgreSQL-database</span><span class="sxs-lookup"><span data-stu-id="e2b7e-171">Test the application locally against the Azure PostgreSQL database</span></span> 

<span data-ttu-id="e2b7e-172">Ga terug nu naar de *app* map van de gekloonde Github-opslagplaats, kunt u de Python Flask-toepassing uitvoeren door de omgevingsvariabelen database bij te werken.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-172">Going back now to the *app* folder of the cloned Github repository, you can run the Python Flask application by updating the database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="e2b7e-173">Wanneer de app volledig wordt geladen is, ziet u iets soortgelijks als in het volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-173">When the app is fully loaded, you see something similar to the following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="e2b7e-174">Ga naar http://127.0.0.1:5000 in een browser.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-174">Navigate to http://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="e2b7e-175">Klik op **registreren!**</span><span class="sxs-lookup"><span data-stu-id="e2b7e-175">Click **Register!**</span></span> <span data-ttu-id="e2b7e-176">en maak de registratie van een test.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-176">and create a test registration.</span></span> <span data-ttu-id="e2b7e-177">U schrijft gegevens nu met de database in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-177">You are now writing data to the database in Azure.</span></span>

![Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-the-application-from-a-docker-container"></a><span data-ttu-id="e2b7e-179">De toepassing wordt uitgevoerd vanuit een Docker-Container</span><span class="sxs-lookup"><span data-stu-id="e2b7e-179">Running the application from a Docker Container</span></span>

<span data-ttu-id="e2b7e-180">De Docker een installatiekopie van de container maken.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-180">Build the Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="e2b7e-181">Docker geeft een bevestiging dat deze de container is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-181">Docker displays a confirmation that it successfully created the container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="e2b7e-182">Omgevingsvariabelen database toevoegen aan een variabele bestand omgeving *db.env*.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-182">Add database environment variables to an environment variable file *db.env*.</span></span> <span data-ttu-id="e2b7e-183">De app maakt verbinding met de productie PostgreSQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-183">The app will connect to the PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="e2b7e-184">Voer de app uit in de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-184">Run the app from within the Docker container.</span></span> <span data-ttu-id="e2b7e-185">De volgende opdracht geeft de variabele omgeving-bestand en de Flask standaardpoort 5000 wordt toegewezen aan de lokale poort 5000.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-185">The following command specifies the environment variable file and maps the default Flask port 5000 to local port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="e2b7e-186">De uitvoer is vergelijkbaar met wat u eerder hebt gezien.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-186">The output is similar to what you saw earlier.</span></span> <span data-ttu-id="e2b7e-187">De databasemigratie van de oorspronkelijke wordt echter niet meer hoeft te worden uitgevoerd en daarom wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-187">However, the initial database migration no longer needs to be performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

<span data-ttu-id="e2b7e-188">De database bevat al de registratie die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-188">The database already contains the registration you created previously.</span></span>

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-the-docker-container-to-a-container-registry"></a><span data-ttu-id="e2b7e-190">De Docker-container uploaden naar een container-register</span><span class="sxs-lookup"><span data-stu-id="e2b7e-190">Upload the Docker container to a container registry</span></span>

<span data-ttu-id="e2b7e-191">In deze stap kunt u de Docker-container uploaden naar een container-register.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-191">In this step, you upload the Docker container to a container registry.</span></span> <span data-ttu-id="e2b7e-192">Gebruikt u Azure Container register, maar u kunt ook andere populaire protocollen zoals Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="e2b7e-193">Een Azure Container Registry maken</span><span class="sxs-lookup"><span data-stu-id="e2b7e-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="e2b7e-194">Vervang in de volgende opdracht voor het maken van een container register  *\<registry_name >* met een unieke Azure container register-naam van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-194">In the following command to create a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="e2b7e-195">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="e2b7e-195">Output</span></span>
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-the-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="e2b7e-196">De referenties van het register voor pushen en installatiekopieën van Docker binnenhalen ophalen</span><span class="sxs-lookup"><span data-stu-id="e2b7e-196">Retrieve the registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="e2b7e-197">Als u wilt weergeven register referenties, eerst Administrator-modus inschakelen</span><span class="sxs-lookup"><span data-stu-id="e2b7e-197">To show registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="e2b7e-198">Ziet u twee wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-198">You see two passwords.</span></span> <span data-ttu-id="e2b7e-199">Noteer de gebruikersnaam en het eerste wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-199">Make note of the user name and the first password.</span></span>

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-to-azure-container-registry"></a><span data-ttu-id="e2b7e-200">Upload uw Docker-container in Azure Container register</span><span class="sxs-lookup"><span data-stu-id="e2b7e-200">Upload your Docker container to Azure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-the-docker-python-flask-application-to-azure"></a><span data-ttu-id="e2b7e-201">De Docker Python Flask-toepassing in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="e2b7e-201">Deploy the Docker Python Flask application to Azure</span></span>

<span data-ttu-id="e2b7e-202">In deze stap maakt implementeren u om uw toepassing Docker-container op basis van een Python Flask in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-202">In this step, you deploy your Docker container-based Python Flask application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="e2b7e-203">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="e2b7e-203">Create an App Service plan</span></span>

<span data-ttu-id="e2b7e-204">Maak een App Service-plan met de opdracht [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="e2b7e-204">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="e2b7e-205">Het volgende voorbeeld wordt een op basis van Linux-App Service-plan met de naam *myAppServicePlan* met behulp van de prijzen voor S1 trapsgewijs:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-205">The following example creates a Linux-based App Service plan named *myAppServicePlan* using the S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="e2b7e-206">Wanneer de App Service-abonnement is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-206">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a><span data-ttu-id="e2b7e-207">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="e2b7e-207">Create a web app</span></span>

<span data-ttu-id="e2b7e-208">Maak een WebApp in de *myAppServicePlan* App Service-abonnement met de [az webapp maken](/cli/azure/webapp#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-208">Create a web app in the *myAppServicePlan* App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="e2b7e-209">De web-app hebt u een hosting ruimte om uw code te implementeren en biedt een URL op voor u de gedistribueerde toepassing weergeven.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-209">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="e2b7e-210">Gebruik te maken van de web-app.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-210">Use  to create the web app.</span></span> 

<span data-ttu-id="e2b7e-211">Vervang in de volgende opdracht, de  *\<app_naam >* aanduiding voor items met een unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-211">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="e2b7e-212">Deze naam is onderdeel van de standaard-URL voor de web-app zodat de naam moet uniek zijn in alle apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-212">This name is part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="e2b7e-213">Wanneer de web-app is gemaakt, toont de Azure CLI soortgelijke informatie als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-213">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-the-database-environment-variables"></a><span data-ttu-id="e2b7e-214">De omgevingsvariabelen database configureren</span><span class="sxs-lookup"><span data-stu-id="e2b7e-214">Configure the database environment variables</span></span>

<span data-ttu-id="e2b7e-215">Eerder in de zelfstudie u omgevingsvariabelen verbinding maken met uw PostgreSQL-database gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-215">Earlier in the tutorial, you defined environment variables to connect to your PostgreSQL database.</span></span>

<span data-ttu-id="e2b7e-216">In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van de [az webapp config appsettings set](/cli/azure/webapp/config#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-216">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="e2b7e-217">Het volgende voorbeeld geeft de details van de database-verbinding als de app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-217">The following example specifies the database connection details as app settings.</span></span> <span data-ttu-id="e2b7e-218">Gebruikt ook de *poort* poort 5000 kaart variabele van uw Docker-Container voor het ontvangen van HTTP-verkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-218">It also uses the *PORT* variable to map PORT 5000 from your Docker Container to receive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="e2b7e-219">Docker-container implementatie configureren</span><span class="sxs-lookup"><span data-stu-id="e2b7e-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="e2b7e-220">AppService kan automatisch downloaden en uitvoeren van een Docker-container.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="e2b7e-221">Wanneer u de Docker-container bijwerken of de instellingen wijzigt, start u de app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-221">Whenever you update the Docker container or change the settings, restart the app.</span></span> <span data-ttu-id="e2b7e-222">Opnieuw opstarten zorgt ervoor dat alle instellingen worden toegepast en de meest recente container wordt opgehaald uit het register.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-222">Restarting ensures that all settings are applied and the latest container is pulled from the registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="e2b7e-223">Blader naar de Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="e2b7e-223">Browse to the Azure web app</span></span> 

<span data-ttu-id="e2b7e-224">Blader naar de geïmplementeerde web-app met behulp van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-224">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="e2b7e-225">De web-app langer laden omdat de container moet worden gedownload en gestart nadat de configuratie van de container is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-225">The web app takes longer to load because the container has to be downloaded and started after the container configuration is changed.</span></span>

<span data-ttu-id="e2b7e-226">Er is eerder geregistreerde gasten die zijn opgeslagen in de Azure-productiedatabase in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-226">You see previously registered guests that were saved to the Azure production database in the previous step.</span></span>

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="e2b7e-228">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="e2b7e-228">**Congratulations!**</span></span> <span data-ttu-id="e2b7e-229">U uitvoert een Docker-container gebaseerde Python Flask-app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="e2b7e-230">Update-gegevensmodel en de implementatie opnieuw uit</span><span class="sxs-lookup"><span data-stu-id="e2b7e-230">Update data model and redeploy</span></span>

<span data-ttu-id="e2b7e-231">In deze stap maakt toevoegen u het aantal deelnemers aan elke gebeurtenisregistratie door het bijwerken van het model van de Gast.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-231">In this step, you add the number of attendees to each event registration by updating the Guest model.</span></span>

<span data-ttu-id="e2b7e-232">Bekijk de *0,2 migratie* uitgebracht met de volgende git-opdracht:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-232">Check out the *0.2-migration* release with the following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="e2b7e-233">Deze release wordt al de vereiste wijzigingen aangebracht in weergaven, domeincontrollers en model.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-233">This release already made the necessary changes to views, controllers, and model.</span></span> <span data-ttu-id="e2b7e-234">Dit omvat ook de databasemigratie van een gegenereerd *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="e2b7e-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="e2b7e-235">Hier ziet u alle wijzigingen die via de volgende git-opdracht:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-235">You can see all changes made via the following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="e2b7e-236">Uw wijzigingen lokaal testen</span><span class="sxs-lookup"><span data-stu-id="e2b7e-236">Test your changes locally</span></span>

<span data-ttu-id="e2b7e-237">Voer de volgende opdrachten voor het testen van uw wijzigingen door lokaal uit te voeren van de flask-server.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-237">Run the following commands to test your changes locally by running the flask server.</span></span>

<span data-ttu-id="e2b7e-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="e2b7e-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="e2b7e-239">Ga naar http://127.0.0.1:5000 in uw browser om de wijzigingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-239">Navigate to http://127.0.0.1:5000 in your browser to view the changes.</span></span> <span data-ttu-id="e2b7e-240">Een test maken.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-240">Create a test registration.</span></span>

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-to-azure"></a><span data-ttu-id="e2b7e-242">Wijzigingen publiceren naar Azure</span><span class="sxs-lookup"><span data-stu-id="e2b7e-242">Publish changes to Azure</span></span>

<span data-ttu-id="e2b7e-243">De nieuwe docker-installatiekopie bouwen, dit doorgeven aan het register van de container en start de app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-243">Build the new docker image, push it to the container registry, and restart the app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="e2b7e-244">Navigeer naar uw Azure-web-app en probeer opnieuw om de nieuwe functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-244">Navigate to your Azure web app and try out the new functionality again.</span></span> <span data-ttu-id="e2b7e-245">Maak een andere gebeurtenisregistratie.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask-app in Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="e2b7e-247">Uw Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="e2b7e-247">Manage your Azure web app</span></span>

<span data-ttu-id="e2b7e-248">Ga naar de [Azure-portal](https://portal.azure.com) om te zien van de web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-248">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="e2b7e-249">Klik vanuit het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-249">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="e2b7e-251">Standaard ziet u de portal voor uw web-app **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-251">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="e2b7e-252">Deze pagina geeft u een overzicht van hoe uw app presteert.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="e2b7e-253">Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="e2b7e-254">De tabbladen aan de linkerkant van de pagina's worden weergegeven de andere configuratie dat kunt u openen.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-254">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="e2b7e-256">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2b7e-256">Next steps</span></span>

<span data-ttu-id="e2b7e-257">Ga naar de volgende zelfstudie voor informatie over het toewijzen van een aangepaste DNS-naam aan uw web-app.</span><span class="sxs-lookup"><span data-stu-id="e2b7e-257">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="e2b7e-258">Een bestaande aangepaste DNS-naam toewijzen aan Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="e2b7e-258">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
