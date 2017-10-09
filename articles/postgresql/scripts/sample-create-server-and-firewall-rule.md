---
title: aaa "Azure CLI Script - Maak een Azure-Database voor PostgreSQL | Microsoft Docs'
description: Azure CLI-voorbeeldscript - maakt een Azure-Database voor PostgreSQL-server en configureert u een firewallregel op serverniveau.
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="a57a2-103">Een Azure-Database voor PostgreSQL-server maken en configureren van een firewallregel hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="a57a2-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="a57a2-104">Dit voorbeeldscript CLI maakt een Azure-Database voor PostgreSQL-server en configureert u een firewallregel op serverniveau.</span><span class="sxs-lookup"><span data-stu-id="a57a2-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="a57a2-105">Zodra het Hallo-script is uitgevoerd, Hallo PostgreSQL server toegankelijk is vanaf alle Azure-services en Hallo geconfigureerd IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a57a2-105">Once hello script has been successfully run, hello PostgreSQL server can be accessed from all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a57a2-106">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a57a2-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a57a2-107">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="a57a2-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a57a2-108">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a57a2-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a57a2-109">Voorbeeld van een script</span><span class="sxs-lookup"><span data-stu-id="a57a2-109">Sample script</span></span>
<span data-ttu-id="a57a2-110">In dit voorbeeldscript bewerken Hallo gemarkeerde regels toocustomize Hallo beheerdersgebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a57a2-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a57a2-111">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="a57a2-111">Clean up deployment</span></span>
<span data-ttu-id="a57a2-112">Na het uitvoeren van het voorbeeldscript Hallo mag na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep en alle resources die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a57a2-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="a57a2-113">Script uitleg</span><span class="sxs-lookup"><span data-stu-id="a57a2-113">Script explanation</span></span>
<span data-ttu-id="a57a2-114">Dit script maakt gebruik van Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a57a2-114">This script uses hello following commands.</span></span> <span data-ttu-id="a57a2-115">Elke opdracht in Hallo tabel koppelingen toocommand specifieke documentatie.</span><span class="sxs-lookup"><span data-stu-id="a57a2-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a57a2-116">**Opdracht**</span><span class="sxs-lookup"><span data-stu-id="a57a2-116">**Command**</span></span> | <span data-ttu-id="a57a2-117">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="a57a2-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="a57a2-118">AZ groep maken</span><span class="sxs-lookup"><span data-stu-id="a57a2-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="a57a2-119">Maakt een resourcegroep waarin alle resources worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a57a2-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a57a2-120">AZ postgres server maken</span><span class="sxs-lookup"><span data-stu-id="a57a2-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="a57a2-121">Maakt een PostgreSQL-server die als host fungeert voor Hallo-databases.</span><span class="sxs-lookup"><span data-stu-id="a57a2-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="a57a2-122">AZ postgres serverfirewall maken</span><span class="sxs-lookup"><span data-stu-id="a57a2-122">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="a57a2-123">Maakt een regel tooallow toegang toohello firewallserver en databases die onder deze van Hallo opgegeven IP-adresbereik.</span><span class="sxs-lookup"><span data-stu-id="a57a2-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="a57a2-124">AZ groep verwijderen</span><span class="sxs-lookup"><span data-stu-id="a57a2-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="a57a2-125">Hiermee verwijdert u een resourcegroep met inbegrip van alle ingesloten resources.</span><span class="sxs-lookup"><span data-stu-id="a57a2-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a57a2-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a57a2-126">Next steps</span></span>
- <span data-ttu-id="a57a2-127">Meer informatie over hello Azure CLI: [Azure CLI-documentatie](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="a57a2-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="a57a2-128">Probeer extra scripts: [voorbeelden van Azure CLI voor Azure-Database voor PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a57a2-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
