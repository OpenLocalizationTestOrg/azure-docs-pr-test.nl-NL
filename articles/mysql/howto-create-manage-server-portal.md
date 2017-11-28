---
title: aaaCreate en beheren van Azure-Database voor de MySQL-server met Azure portal | Microsoft Docs
description: Dit artikel wordt beschreven hoe u kunt snel een nieuwe Azure-Database voor de MySQL-server maken en beheren Hallo-server met behulp van hello Azure-Portal.
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="47286-103">Maken en beheren van Azure-Database voor de MySQL-server met Azure portal</span><span class="sxs-lookup"><span data-stu-id="47286-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="47286-104">Dit artikel wordt beschreven hoe u kunt snel een nieuwe Azure-Database voor de MySQL-server maken en beheren Hallo-server met behulp van hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="47286-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="47286-105">Serverbeheer bevat Serverdetails & databases weer te geven, wachtwoord opnieuw instellen en verwijderen van Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="47286-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="47286-106">Meld u bij toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="47286-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="47286-107">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="47286-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="47286-108">Een Azure-database voor MySQL-server maken</span><span class="sxs-lookup"><span data-stu-id="47286-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="47286-109">Volg deze stappen toocreate een Azure-Database voor de MySQL-server met de naam 'mysqlserver4demo'</span><span class="sxs-lookup"><span data-stu-id="47286-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="47286-110">1 Klik **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="47286-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="47286-111">2 Selecteer **Databases** van Hallo nieuwe pagina en selecteer **Azure Database voor MySQL** van Hallo Databases pagina.</span><span class="sxs-lookup"><span data-stu-id="47286-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="47286-112">Een Azure-Database voor de MySQL-server is gemaakt met een gedefinieerde set [berekenings- en](./concepts-compute-unit-and-storage.md) resources.</span><span class="sxs-lookup"><span data-stu-id="47286-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="47286-113">Hallo-database wordt gemaakt vanuit een Azure-resourcegroep en in een Azure-Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="47286-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![Maak nieuwe-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="47286-115">3 - invullen hello Azure Database voor MySQL formulier Hello volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="47286-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="47286-116">**Formulierveld**</span><span class="sxs-lookup"><span data-stu-id="47286-116">**Form Field**</span></span> | <span data-ttu-id="47286-117">**Beschrijving van veld**</span><span class="sxs-lookup"><span data-stu-id="47286-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="47286-118">*Servernaam*</span><span class="sxs-lookup"><span data-stu-id="47286-118">*Server name*</span></span> | <span data-ttu-id="47286-119">Azure-mysql (servernaam is globally unique identifier)</span><span class="sxs-lookup"><span data-stu-id="47286-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="47286-120">*Abonnement*</span><span class="sxs-lookup"><span data-stu-id="47286-120">*Subscription*</span></span> | <span data-ttu-id="47286-121">MySQLaaS (Selecteer in de vervolgkeuzelijst)</span><span class="sxs-lookup"><span data-stu-id="47286-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="47286-122">*Resourcegroep*</span><span class="sxs-lookup"><span data-stu-id="47286-122">*Resource group*</span></span> | <span data-ttu-id="47286-123">MyResource (een nieuwe resourcegroep maken of een bestaande gebruiken)</span><span class="sxs-lookup"><span data-stu-id="47286-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="47286-124">*Aanmeldgegevens van serverbeheerder*</span><span class="sxs-lookup"><span data-stu-id="47286-124">*Server admin login*</span></span> | <span data-ttu-id="47286-125">myadmin (stel accountnaam van beheerder in)</span><span class="sxs-lookup"><span data-stu-id="47286-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="47286-126">*Wachtwoord*</span><span class="sxs-lookup"><span data-stu-id="47286-126">*Password*</span></span> | <span data-ttu-id="47286-127">beheerderswachtwoord voor account Setup</span><span class="sxs-lookup"><span data-stu-id="47286-127">setup admin account password</span></span> |
| <span data-ttu-id="47286-128">*Wachtwoord bevestigen*</span><span class="sxs-lookup"><span data-stu-id="47286-128">*Confirm password*</span></span> | <span data-ttu-id="47286-129">bevestig wachtwoord voor beheerdersaccount</span><span class="sxs-lookup"><span data-stu-id="47286-129">confirm admin account password</span></span> |
| <span data-ttu-id="47286-130">*Locatie*</span><span class="sxs-lookup"><span data-stu-id="47286-130">*Location*</span></span> | <span data-ttu-id="47286-131">Noord-Europa (Selecteer tussen Noord-Europa en VS-West)</span><span class="sxs-lookup"><span data-stu-id="47286-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="47286-132">*Versie*</span><span class="sxs-lookup"><span data-stu-id="47286-132">*Version*</span></span> | <span data-ttu-id="47286-133">5.6 (Kies Azure Database voor MySQL server-versie)</span><span class="sxs-lookup"><span data-stu-id="47286-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="47286-134">4 Klik **prijscategorie** toospecify Hallo prijscategorie en prestatieniveau serviceniveau voor uw nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="47286-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="47286-135">COMPUTE eenheid tussen 50 en 100 in de basisstaffel 100 en 200 in Standard-laag kan worden geconfigureerd en opslag op basis van opgenomen bedrag kan worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="47286-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="47286-136">Voor deze handleiding procedure kiezen we 50 Compute-eenheid en 50GB.</span><span class="sxs-lookup"><span data-stu-id="47286-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="47286-137">Klik op **OK** toosave uw selectie.</span><span class="sxs-lookup"><span data-stu-id="47286-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="47286-138">![Maak-server--prijscategorie](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="47286-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="47286-139">5 Klik **maken** tooprovision Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="47286-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="47286-140">De inrichting duurt een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="47286-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="47286-141">Controleer de Hallo **pincode toodashboard** optie tooallow eenvoudig bijhouden van uw implementaties.</span><span class="sxs-lookup"><span data-stu-id="47286-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="47286-142">Hoewel too1000GB in basisstaffel en 10000GB in standaard laag wordt ondersteund voor opslag, voor de openbare Preview is Hallo maximale opslagcapaciteit het nog steeds beperkt too1000GB tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="47286-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="47286-143">Een Azure-Database voor de MySQL-server bijwerken</span><span class="sxs-lookup"><span data-stu-id="47286-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="47286-144">Nadat de nieuwe server is ingericht, gebruiker heeft van 2 opties tooedit een bestaande server: beheerderswachtwoord of schaal omhoog/omlaag Hallo-server opnieuw instellen door te wijzigen Hallo compute-eenheden.</span><span class="sxs-lookup"><span data-stu-id="47286-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="47286-145">Wachtwoord wijzigen Hallo beheerder-gebruiker</span><span class="sxs-lookup"><span data-stu-id="47286-145">Change hello administrator user password</span></span>
<span data-ttu-id="47286-146">1 - op Hallo server **overzicht** blade, klikt u op **wachtwoord opnieuw instellen** toopopulate de invoer en de bevestiging venster van een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="47286-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="47286-147">2 - nieuw wachtwoord invoeren en Bevestig Hallo-wachtwoord in als hieronder Hallo-venster: ![wachtwoord opnieuw instellen](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="47286-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="47286-148">3 en klik op **OK** toosave Hallo nieuwe wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="47286-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="47286-149">Omhoog/omlaag schalen door het wijzigen van de Compute-eenheden</span><span class="sxs-lookup"><span data-stu-id="47286-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="47286-150">1 - op Hallo serverblade onder **instellingen**, klikt u op **prijscategorie** tooopen Hallo prijzen laag blade voor hello Azure Database voor de MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="47286-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="47286-151">2 volgen stap 4 in **maken van een Azure-Database voor MySQL server** toochange Compute eenheden in dezelfde prijscategorie Hallo.</span><span class="sxs-lookup"><span data-stu-id="47286-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="47286-152">Een Azure-Database voor de MySQL-server verwijderen</span><span class="sxs-lookup"><span data-stu-id="47286-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="47286-153">1 - op Hallo server **overzicht** blade, klikt u op **verwijderen** opdracht knop tooopen Hallo verwijderen bevestiging blade.</span><span class="sxs-lookup"><span data-stu-id="47286-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="47286-154">2-type Hallo juiste servernaam in het invoervak van de blade hello om dubbele bevestiging.</span><span class="sxs-lookup"><span data-stu-id="47286-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="47286-155">3 en klik op **verwijderen** knop opnieuw tooconfirm actie verwijderen en wachten op de pop-up 'Verwijderen geslaagd' op Hallo meldingsbalk.</span><span class="sxs-lookup"><span data-stu-id="47286-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="47286-156">Lijst hello Azure Database voor de MySQL-databases</span><span class="sxs-lookup"><span data-stu-id="47286-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="47286-157">Op de server Hallo **overzicht** blade Schuif omlaag totdat u de database Hallo ziet tegel op Hallo onder.</span><span class="sxs-lookup"><span data-stu-id="47286-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="47286-158">Alle Hallo databases worden vermeld in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="47286-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="47286-159">Klik op **verwijderen** opdracht knop tooopen Hallo verwijderen bevestiging blade.</span><span class="sxs-lookup"><span data-stu-id="47286-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![weergeven-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="47286-161">Details weergeven van een Azure-Database voor de MySQL-server</span><span class="sxs-lookup"><span data-stu-id="47286-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="47286-162">Klik op **eigenschappen** onder **instellingen** op Hallo server blade geopend Hallo **eigenschappen** blade.</span><span class="sxs-lookup"><span data-stu-id="47286-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="47286-163">U kunt vervolgens alle informatie over het Hallo-server weergeven.</span><span class="sxs-lookup"><span data-stu-id="47286-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="47286-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="47286-164">Next steps</span></span>

[<span data-ttu-id="47286-165">Snelstartgids: Azure-Database maken voor de MySQL-server met Azure portal</span><span class="sxs-lookup"><span data-stu-id="47286-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
