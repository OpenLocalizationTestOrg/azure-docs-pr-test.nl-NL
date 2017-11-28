---
title: aaaCreate en beheren van Azure-Database voor firewallregels MySQL met Azure CLI | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate en beheren van Azure-Database voor firewallregels MySQL via Azure CLI-opdrachtregel.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="71bd1-103">Maken en beheren van Azure-Database voor firewallregels MySQL met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="71bd1-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="71bd1-104">Firewallregels op serverniveau inschakelen beheerders toomanage toegang tooan Azure Database voor MySQL-Server van een specifiek IP-adres of een bereik van IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="71bd1-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="71bd1-105">U handige Azure CLI-opdrachten gebruikt, kunt u maken, bijwerken, verwijderen, lijst, en firewall-regels toomanage uw server weergeven.</span><span class="sxs-lookup"><span data-stu-id="71bd1-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="71bd1-106">Zie voor een overzicht van Azure-Database voor MySQL firewalls [Azure Database voor de MySQL-firewallregels voor server](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="71bd1-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71bd1-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="71bd1-107">Prerequisites</span></span>
* [<span data-ttu-id="71bd1-108">Installeer Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="71bd1-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="71bd1-109">Azure Python SDK voor PostgreSQL en MySQL Services installeren</span><span class="sxs-lookup"><span data-stu-id="71bd1-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="71bd1-110">Hello Azure CLI-component voor PostgreSQL en MySQL services installeren</span><span class="sxs-lookup"><span data-stu-id="71bd1-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="71bd1-111">Een Azure-database voor MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="71bd1-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="71bd1-112">Firewallregel opdrachten:</span><span class="sxs-lookup"><span data-stu-id="71bd1-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="71bd1-113">Hallo **az mysql server-firewallregel** opdracht wordt gebruikt voor Azure CLI toocreate, verwijderen, lijst, weergeven en bijwerken van firewallregels.</span><span class="sxs-lookup"><span data-stu-id="71bd1-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="71bd1-114">Opdrachten:</span><span class="sxs-lookup"><span data-stu-id="71bd1-114">Commands:</span></span>
- <span data-ttu-id="71bd1-115">**Maak**: een firewallregel op Azure MySQL-server maken.</span><span class="sxs-lookup"><span data-stu-id="71bd1-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="71bd1-116">**verwijderen**: verwijderen van een firewallregel voor Azure MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="71bd1-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="71bd1-117">**lijst** : lijst hello Azure MySQL-firewallregels voor server.</span><span class="sxs-lookup"><span data-stu-id="71bd1-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="71bd1-118">**weergeven** : Hallo details weergeven van een server Azure MySQL firewallregel.</span><span class="sxs-lookup"><span data-stu-id="71bd1-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="71bd1-119">**bijwerken**: een firewallregel voor Azure MySQL-server bijwerken.</span><span class="sxs-lookup"><span data-stu-id="71bd1-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="71bd1-120">Aanmelding tooAzure en de lijst met uw Azure-Database voor de MySQL-Servers</span><span class="sxs-lookup"><span data-stu-id="71bd1-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="71bd1-121">Azure CLI veilig met uw Azure-account verbinding kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="71bd1-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="71bd1-122">Gebruik Hallo **az aanmelding** toodo deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="71bd1-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="71bd1-123">Hallo volgende opdracht uit vanaf de opdrachtregel Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="71bd1-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="71bd1-124">Met deze opdracht wordt een toouse code in de volgende stap Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="71bd1-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="71bd1-125">Gebruik van een webpagina browser tooopen hello [https://aka.ms/devicelogin](https://aka.ms/devicelogin) en Voer Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="71bd1-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="71bd1-126">Bij de prompt hello, meld u aan met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="71bd1-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="71bd1-127">Wanneer uw aanmelding is geautoriseerd, wordt een lijst met abonnementen afgedrukt in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="71bd1-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="71bd1-128">Kopiëren Hallo-id van Hallo gewenste abonnement tooset Hallo huidige abonnement toobe gebruikt u verder gaat.</span><span class="sxs-lookup"><span data-stu-id="71bd1-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="71bd1-129">Lijst hello Azure-Databases van MySQL-servers voor uw abonnement en de resource-groep als u niet zeker van Hallo namen.</span><span class="sxs-lookup"><span data-stu-id="71bd1-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="71bd1-130">Houd er rekening mee Hallo kenmerk name in Hallo op te nemen, die wordt gebruikt toospecify welke toowork MySQL-server op.</span><span class="sxs-lookup"><span data-stu-id="71bd1-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="71bd1-131">Indien nodig, hello om details te bevestigen voor die server toousing Hallo naam kenmerk tooconfirm naam juist is:</span><span class="sxs-lookup"><span data-stu-id="71bd1-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="71bd1-132">Lijst met firewallregels voor Azure-Database voor de MySQL-Server</span><span class="sxs-lookup"><span data-stu-id="71bd1-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="71bd1-133">Hallo-servernaam en naam resourcegroep hello, lijst Hallo bestaande firewallregels voor server op Hallo-server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71bd1-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="71bd1-134">U ziet dat Hallo server name-kenmerk is opgegeven in Hallo **--server** -switch en niet Hallo **--naam** overschakelen.</span><span class="sxs-lookup"><span data-stu-id="71bd1-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="71bd1-135">Hallo regels Hallo uitvoer wordt een lijst als een standaard in JSON opmaken.</span><span class="sxs-lookup"><span data-stu-id="71bd1-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="71bd1-136">U Hallo switch **--uitvoertabel** voor een beter leesbare tabelindeling als Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="71bd1-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="71bd1-137">Firewallregel op Azure-Database maken voor de MySQL-Server</span><span class="sxs-lookup"><span data-stu-id="71bd1-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="71bd1-138">Hello Azure MySQL-servernaam en Hallo de naam van resourcegroep gebruikt, een nieuwe firewallregel maken op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="71bd1-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="71bd1-139">Geef een naam voor het Hallo-regel Hallo begin-IP- en laatste IP-voor Hallo regel toocover een bereik met IP-adressen tooallow toegang.</span><span class="sxs-lookup"><span data-stu-id="71bd1-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="71bd1-140">Voor een enkel IP-adressen toobe toegang hebben, Geef hetzelfde adres Hallo zoals Hallo eerste IP- en eind-IP, zoals in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="71bd1-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="71bd1-141">Als dit lukt, wordt een opdrachtuitvoer Hallo Hallo details van de firewallregel die u hebt gemaakt, in JSON-indeling standaard Hallo lijst.</span><span class="sxs-lookup"><span data-stu-id="71bd1-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="71bd1-142">Als er een storing, ziet Hallo uitvoer fouttekst in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="71bd1-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="71bd1-143">Firewallregel op Azure-Database voor de MySQL-server bijwerken</span><span class="sxs-lookup"><span data-stu-id="71bd1-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="71bd1-144">Een bestaande firewallregel op Hallo server hello Azure MySQL-servernaam en Hallo de naam van resourcegroep gebruikt, worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="71bd1-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="71bd1-145">Hallo-naam van bestaande firewallregel Hallo als invoer- en Hallo start IP- en end IP-tooupdate kenmerken opgeven.</span><span class="sxs-lookup"><span data-stu-id="71bd1-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="71bd1-146">Als dit lukt, wordt een opdrachtuitvoer Hallo Hallo details van de firewallregel die u hebt bijgewerkt, in JSON-indeling standaard Hallo lijst.</span><span class="sxs-lookup"><span data-stu-id="71bd1-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="71bd1-147">Als er een storing, ziet Hallo uitvoer fouttekst in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="71bd1-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="71bd1-148">Als de firewallregel Hallo niet bestaat, wordt deze gemaakt door de opdracht update Hallo.</span><span class="sxs-lookup"><span data-stu-id="71bd1-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="71bd1-149">Details van de Firewall-regels op Azure-Database voor de MySQL-Server weergeven</span><span class="sxs-lookup"><span data-stu-id="71bd1-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="71bd1-150">Hallo bestaande firewallregelgegevens van Hallo server hello Azure MySQL-servernaam en Hallo de naam van resourcegroep gebruikt, worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="71bd1-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="71bd1-151">Hallo-naam van de bestaande firewallregel Hallo opgeven als invoer.</span><span class="sxs-lookup"><span data-stu-id="71bd1-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="71bd1-152">Als dit lukt, wordt een opdrachtuitvoer Hallo Hallo details van de firewallregel die u hebt opgegeven, in JSON-indeling standaard Hallo lijst.</span><span class="sxs-lookup"><span data-stu-id="71bd1-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="71bd1-153">Als er een storing, ziet Hallo uitvoer fouttekst in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="71bd1-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="71bd1-154">Firewallregel op Azure-Database voor de MySQL-Server verwijderen</span><span class="sxs-lookup"><span data-stu-id="71bd1-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="71bd1-155">Hello Azure MySQL-servernaam en Hallo de naam van resourcegroep gebruikt, een bestaande firewallregel van Hallo server verwijderen.</span><span class="sxs-lookup"><span data-stu-id="71bd1-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="71bd1-156">Hallo-naam van de bestaande firewallregel Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="71bd1-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="71bd1-157">Als dit lukt wordt er geen uitvoer.</span><span class="sxs-lookup"><span data-stu-id="71bd1-157">Upon success, there is no output.</span></span> <span data-ttu-id="71bd1-158">Bij storingen tekst hello foutbericht geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="71bd1-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71bd1-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="71bd1-159">Next steps</span></span>
- <span data-ttu-id="71bd1-160">Meer inzicht te geven over [Azure voor firewallregels voor MySQL Server-Database](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="71bd1-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="71bd1-161">Maken en beheren van Azure-Database voor firewallregels MySQL met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="71bd1-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
