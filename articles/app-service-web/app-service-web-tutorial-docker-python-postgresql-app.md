---
title: aaaBuild een Docker Python en PostgreSQL web-app in Azure | Microsoft Docs
description: Meer informatie over hoe tooget een Docker-Python-app in Azure AD werkt met verbinding tooa PostgreSQL-database.
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
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="5ca1f-103">Een Docker Python en PostgreSQL web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="5ca1f-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="5ca1f-104">Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="5ca1f-105">Deze zelfstudie laat zien hoe een basic Docker-Python toocreate web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="5ca1f-106">U maakt verbinding met deze app tooa PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="5ca1f-107">Wanneer u bent klaar, hebt u een Python Flask-toepassing uitgevoerd binnen een Docker-container op [Azure App Service Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5ca1f-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![Docker Python Flask-app in Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="5ca1f-109">U kunt stappen Hallo hieronder op Mac OS.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="5ca1f-110">Instructies voor Linux en Windows zijn hetzelfde in de meeste gevallen hello, maar Hallo verschillen niet worden beschreven in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="5ca1f-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5ca1f-111">Prerequisites</span></span>

<span data-ttu-id="5ca1f-112">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="5ca1f-113">Git installeren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="5ca1f-114">Python installeren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="5ca1f-115">Installeren en uitvoeren van PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="5ca1f-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="5ca1f-116">Docker-Community Edition installeren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5ca1f-117">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5ca1f-118">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5ca1f-119">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5ca1f-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="5ca1f-120">Lokale PostgreSQL-installatie testen en een database maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="5ca1f-121">Open Hallo terminalvenster en voer `psql postgres` tooconnect tooyour lokale PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="5ca1f-122">Als de verbinding geslaagd is, wordt uw PostgreSQL-database wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="5ca1f-123">Als dit niet het geval is, zorg ervoor dat de lokale PostgresQL-database is gestart door Hallo stappen op te volgen [Downloads - PostgreSQL Core distributie](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="5ca1f-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="5ca1f-124">Maken van een database met de naam *eventregistration* en instellen van de gebruiker van een aparte database met de naam *manager* met wachtwoord *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="5ca1f-125">Type *\q* tooexit hello PostgreSQL-client.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="5ca1f-126">Lokale Python Flask-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-126">Create local Python Flask application</span></span>

<span data-ttu-id="5ca1f-127">In deze stap maakt instellen u lokaal Python Flask-project Hallo.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="5ca1f-128">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="5ca1f-128">Clone hello sample application</span></span>

<span data-ttu-id="5ca1f-129">Open Hallo terminalvenster, en `CD` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="5ca1f-130">Voer Hallo deze opdrachten tooclone Hallo voorbeeld opslagplaats en gaat u naar toohello *0,1 initialapp* release.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="5ca1f-131">Deze repository voorbeeld bevat een [Flask](http://flask.pocoo.org/) toepassing.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="5ca1f-132">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="5ca1f-133">In een latere stap kunt u dit proces met het bouwen van een toouse Docker-container met de productiedatabase Hallo vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="5ca1f-134">Vereist hello-pakketten installeren en start de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="5ca1f-135">Wanneer de app Hallo volledig geladen is, ziet u iets dergelijks toohello volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="5ca1f-136">Toohttp://127.0.0.1:5000 in een browser navigeren.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="5ca1f-137">Klik op **registreren!**</span><span class="sxs-lookup"><span data-stu-id="5ca1f-137">Click **Register!**</span></span> <span data-ttu-id="5ca1f-138">en een testgebruiker maken.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-138">and create a test user.</span></span>

![Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="5ca1f-140">Hallo Flask-voorbeeldtoepassing slaat gebruikersgegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="5ca1f-141">Als u succesvol bij het registreren van een gebruiker, wordt uw app gegevens toohello lokale PostgreSQL-database geschreven.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="5ca1f-142">toostop hello Flask-server op elk gewenst moment, typt u Ctrl + C in Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="5ca1f-143">Een productie-PostgreSQL-database maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="5ca1f-144">In deze stap maakt u een PostgreSQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="5ca1f-145">Wanneer uw app geïmplementeerde tooAzure is, wordt deze cloud-database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="5ca1f-146">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="5ca1f-146">Log in tooAzure</span></span>

<span data-ttu-id="5ca1f-147">U bent nu gaat toouse hello Azure CLI 2.0 toocreate Hallo resources die nodig toohost uw toepassing Python in Azure App Service zijn.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="5ca1f-148">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="5ca1f-149">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-149">Create a resource group</span></span>

<span data-ttu-id="5ca1f-150">Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) Hello [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="5ca1f-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="5ca1f-151">Hallo volgende voorbeeld wordt een resourcegroep in de regio VS-West Hallo:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="5ca1f-152">Gebruik Hallo [az appservice lijst-locaties](/cli/azure/appservice#list-locations) Azure CLI opdracht toolist beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="5ca1f-153">Een Azure-database voor PostgreSQL-server maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="5ca1f-154">Een PostgreSQL-server maken met de Hallo [az postgres server maken](/cli/azure/documentdb#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="5ca1f-155">In Hallo volgende opdracht, vervangt u een unieke naam voor Hallo  *\<postgresql_name >* tijdelijke aanduiding en een gebruikersnaam voor Hallo  *\<admin_username >* tijdelijke aanduiding voor .</span><span class="sxs-lookup"><span data-stu-id="5ca1f-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="5ca1f-156">Hallo-servernaam wordt gebruikt als onderdeel van uw eindpunt PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), zodat het Hallo-naam moet toobe unieke op alle servers in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="5ca1f-157">Hallo-gebruikersnaam is voor Hallo initiële database admin-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="5ca1f-158">U bent na vragen aan gebruiker toopick een wachtwoord voor deze gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="5ca1f-159">Wanneer hello Azure Database voor PostgreSQL-server is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="5ca1f-160">Een firewallregel voor hello Azure Database voor PostgreSQL-server maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="5ca1f-161">Hallo volgende Azure CLI opdracht tooallow access toohello-database uit alle IP-adressen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="5ca1f-162">Hello Azure CLI bevestigt Hallo firewall-regel maken met uitvoer vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="5ca1f-163">Verbinding maken met uw database Python Flask-toepassing toohello</span><span class="sxs-lookup"><span data-stu-id="5ca1f-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="5ca1f-164">In deze stap maakt u verbinding maken uw Python Flask-voorbeeld toepassing toohello Azure Database voor PostgreSQL-server die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="5ca1f-165">Een lege database maken en een nieuwe gebruiker van de database-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="5ca1f-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="5ca1f-166">Maak een databasegebruiker met toegang tooa enkele database alleen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="5ca1f-167">U gebruikt deze referenties tooavoid geeft volledige toegang Hallo-toohello toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="5ca1f-168">Verbinding maken met toohello-database (u wordt gevraagd om uw wachtwoord admin).</span><span class="sxs-lookup"><span data-stu-id="5ca1f-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="5ca1f-169">Hallo-database en de gebruikersgegevens van Hallo PostgreSQL CLI maken.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="5ca1f-170">Type *\q* tooexit hello PostgreSQL-client.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="5ca1f-171">Hallo toepassing testen lokaal op Hallo Azure PostgreSQL-database</span><span class="sxs-lookup"><span data-stu-id="5ca1f-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="5ca1f-172">Ga terug nu toohello *app* map Hallo gekloond Github-opslagplaats, kunt u Hallo Python Flask-toepassing uitvoeren door omgevingsvariabelen Hallo-database bij te werken.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="5ca1f-173">Wanneer de app Hallo volledig geladen is, ziet u iets dergelijks toohello volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="5ca1f-174">Toohttp://127.0.0.1:5000 in een browser navigeren.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="5ca1f-175">Klik op **registreren!**</span><span class="sxs-lookup"><span data-stu-id="5ca1f-175">Click **Register!**</span></span> <span data-ttu-id="5ca1f-176">en maak de registratie van een test.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-176">and create a test registration.</span></span> <span data-ttu-id="5ca1f-177">U schrijft gegevens toohello database nu in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-177">You are now writing data toohello database in Azure.</span></span>

![Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="5ca1f-179">Hallo toepassing uitvoert vanuit een Docker-Container</span><span class="sxs-lookup"><span data-stu-id="5ca1f-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="5ca1f-180">Hallo Docker-container installatiekopie maken.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="5ca1f-181">Docker geeft een bevestiging die it gemaakt Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="5ca1f-182">Toevoegen van de omgeving variabelen tooan omgeving variabele databasebestand *db.env*.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="5ca1f-183">Hallo-app verbinding toohello PostgreSQL-productiedatabase in Azure.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="5ca1f-184">Hallo-app uit Hallo Docker-container wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="5ca1f-185">Hallo volgende opdracht geeft Hallo omgeving variabele bestand en Hallo Flask poort 5000 toolocal standaardpoort 5000 wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="5ca1f-186">Hallo-uitvoer is vergelijkbaar toowhat die u eerder hebt gezien.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="5ca1f-187">Echter Hallo initiële database wilt migreren niet langer nodig heeft toobe uitgevoerd en daarom wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="5ca1f-188">Hallo-database bevat al Hallo registratie die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-188">hello database already contains hello registration you created previously.</span></span>

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="5ca1f-190">Hallo Docker-container tooa container register uploaden</span><span class="sxs-lookup"><span data-stu-id="5ca1f-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="5ca1f-191">In deze stap maakt uploaden u Hallo Docker-container tooa container register.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="5ca1f-192">Gebruikt u Azure Container register, maar u kunt ook andere populaire protocollen zoals Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="5ca1f-193">Een Azure Container Registry maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="5ca1f-194">Vervang in Hallo na de opdracht toocreate een container register  *\<registry_name >* met een unieke Azure container register-naam van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="5ca1f-195">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="5ca1f-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="5ca1f-196">Hallo register referenties voor pushen en installatiekopieën van Docker binnenhalen ophalen</span><span class="sxs-lookup"><span data-stu-id="5ca1f-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="5ca1f-197">tooshow register referenties, schakel eerst Administrator-modus.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="5ca1f-198">Ziet u twee wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-198">You see two passwords.</span></span> <span data-ttu-id="5ca1f-199">Noteer Hallo-gebruikersnaam en het Hallo eerste wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="5ca1f-200">Upload uw Docker-container tooAzure Container register</span><span class="sxs-lookup"><span data-stu-id="5ca1f-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="5ca1f-201">Hallo Docker Python Flask-toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="5ca1f-202">In deze stap maakt implementeren u uw tooAzure in Docker-container gebaseerde door toepassing Python Flask-App Service.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="5ca1f-203">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-203">Create an App Service plan</span></span>

<span data-ttu-id="5ca1f-204">Maken van een App Service-abonnement met Hallo [az appservice-abonnement maken](/cli/azure/appservice/plan#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="5ca1f-205">Hallo volgende voorbeeld wordt een op basis van Linux-App Service-plan met de naam *myAppServicePlan* Hallo S1 prijscategorie met:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="5ca1f-206">Wanneer Hallo App Service-abonnement is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="5ca1f-207">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="5ca1f-207">Create a web app</span></span>

<span data-ttu-id="5ca1f-208">Een web-app maken in Hallo *myAppServicePlan* App Service-abonnement met Hallo [az webapp maken](/cli/azure/webapp#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="5ca1f-209">Hallo web app geeft u een hosting-ruimte toodeploy uw code en biedt een URL voor u tooview Hallo toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="5ca1f-210">Gebruik toocreate Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="5ca1f-211">Hallo opdracht, na Vervang in Hallo  *\<app_naam >* aanduiding voor items met een unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="5ca1f-212">Deze naam is onderdeel van Hallo standaard-URL voor de web-app hello, zodat het Hallo-naam moet toobe uniek zijn in alle apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="5ca1f-213">Wanneer het Hallo-web-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="5ca1f-214">Omgevingsvariabelen Hallo-database configureren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-214">Configure hello database environment variables</span></span>

<span data-ttu-id="5ca1f-215">Eerder in de zelfstudie hello, moet u omgeving variabelen tooconnect tooyour PostgreSQL-database gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="5ca1f-216">In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van Hallo [az webapp config appsettings set](/cli/azure/webapp/config#set) opdracht.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="5ca1f-217">Hallo geeft volgende voorbeeld Hallo database Verbindingsdetails als app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="5ca1f-218">Gebruikt ook Hallo *poort* variabele toomap poort 5000 van uw Docker-Container tooreceive HTTP-verkeer op poort 80.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="5ca1f-219">Docker-container implementatie configureren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="5ca1f-220">AppService kan automatisch downloaden en uitvoeren van een Docker-container.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="5ca1f-221">Wanneer u Hallo Docker-container bijwerken of Hallo instellingen wijzigt, start u Hallo app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="5ca1f-222">Opnieuw opstarten zorgt ervoor dat alle instellingen worden toegepast en de meest recente container Hallo vandaan Hallo register.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="5ca1f-223">Toohello Azure-web-app bladeren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="5ca1f-224">Bladeren toohello geïmplementeerd web-app met uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="5ca1f-225">Hallo-web-app duurt langer tooload omdat Hallo container toobe gedownload en gestart nadat het Hallo-container configuratie wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="5ca1f-226">Er is eerder geregistreerde gasten die toohello Azure productiedatabase zijn opgeslagen in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="5ca1f-228">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="5ca1f-228">**Congratulations!**</span></span> <span data-ttu-id="5ca1f-229">U uitvoert een Docker-container gebaseerde Python Flask-app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="5ca1f-230">Update-gegevensmodel en de implementatie opnieuw uit</span><span class="sxs-lookup"><span data-stu-id="5ca1f-230">Update data model and redeploy</span></span>

<span data-ttu-id="5ca1f-231">In deze stap kunt u het aantal deelnemers tooeach gebeurtenisregistratie Hallo toevoegen door Hallo Gast model bij te werken.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="5ca1f-232">Bekijk Hallo *0,2 migratie* release Hello volgende git-opdracht:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="5ca1f-233">Deze release Hallo noodzakelijke wijzigingen tooviews, domeincontrollers en model al is gedaan.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="5ca1f-234">Dit omvat ook de databasemigratie van een gegenereerd *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="5ca1f-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="5ca1f-235">Hier ziet u alle wijzigingen die via Hallo volgende git-opdracht:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="5ca1f-236">Uw wijzigingen lokaal testen</span><span class="sxs-lookup"><span data-stu-id="5ca1f-236">Test your changes locally</span></span>

<span data-ttu-id="5ca1f-237">Hallo opdrachten tootest na uw wijzigingen lokaal uitvoeren door waarop Hallo flask-server.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="5ca1f-238">Mac / Linux:</span><span class="sxs-lookup"><span data-stu-id="5ca1f-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="5ca1f-239">Navigeer toohttp://127.0.0.1:5000 in uw browser tooview Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="5ca1f-240">Een test maken.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-240">Create a test registration.</span></span>

![Docker-container op basis van een Python Flask-toepassing die lokaal wordt uitgevoerd](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="5ca1f-242">TooAzure wijzigingen publiceren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-242">Publish changes tooAzure</span></span>

<span data-ttu-id="5ca1f-243">Hallo nieuwe docker-installatiekopie bouwen, dit toohello container register doorgeven en start Hallo app opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="5ca1f-244">Navigeer tooyour Azure-web-app en nieuwe functionaliteit Hallo opnieuw uitproberen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="5ca1f-245">Maak een andere gebeurtenisregistratie.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![Docker Python Flask-app in Azure App Service](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="5ca1f-247">Uw Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="5ca1f-247">Manage your Azure web app</span></span>

<span data-ttu-id="5ca1f-248">Ga toohello [Azure-portal](https://portal.azure.com) toosee Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="5ca1f-249">In het linkermenu hello, klikt u op **App Services**, klikt u op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="5ca1f-251">Standaard Hallo portal uw web-app toont **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="5ca1f-252">Deze pagina geeft u een overzicht van hoe uw app presteert.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="5ca1f-253">Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="5ca1f-254">Hallo tabbladen aan de linkerkant Hallo van Hallo pagina bevatten Hallo verschillende configuratiepagina's die u kunt openen.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="5ca1f-256">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ca1f-256">Next steps</span></span>

<span data-ttu-id="5ca1f-257">De volgende zelfstudie toolearn toohello gaan hoe toomap een aangepaste DNS-Server name tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="5ca1f-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="5ca1f-258">Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="5ca1f-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
