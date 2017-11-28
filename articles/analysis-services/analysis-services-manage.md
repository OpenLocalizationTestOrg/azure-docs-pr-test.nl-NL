---
title: aaaManage Azure Analysis Services | Microsoft Docs
description: Meer informatie over hoe toomanage een Analysis Services-server in Azure.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="311ee-103">Analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="311ee-103">Manage Analysis Services</span></span>
<span data-ttu-id="311ee-104">Als u een Analysis Services-server hebt gemaakt in Azure, mogelijk zijn er enkele administratie en beheer taken die u tooperform meteen moet of ergens omlaag Hallo weg.</span><span class="sxs-lookup"><span data-stu-id="311ee-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="311ee-105">Voer bijvoorbeeld verwerken toohello vernieuwen van gegevens, bepalen wie toegang Hallo modellen op uw server of controleren van de status van uw server.</span><span class="sxs-lookup"><span data-stu-id="311ee-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="311ee-106">Bepaalde beheertaken kunnen alleen worden uitgevoerd in Azure-portal anderen in SQL Server Management Studio (SSMS), en sommige taken kunnen worden uitgevoerd op een.</span><span class="sxs-lookup"><span data-stu-id="311ee-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="311ee-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="311ee-107">Azure portal</span></span>
<span data-ttu-id="311ee-108">[Azure-portal](http://portal.azure.com/) is waar u kunt maken en verwijderen van servers, serverbronnen bewaken, grootte wijzigen en beheren wie heeft toegang tot tooyour servers.</span><span class="sxs-lookup"><span data-stu-id="311ee-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="311ee-109">Als u problemen ondervindt, kunt u ook een verzoek om ondersteuning te verzenden.</span><span class="sxs-lookup"><span data-stu-id="311ee-109">If you're having some problems, you can also submit a support request.</span></span>

![Servernaam bepalen in Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="311ee-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="311ee-111">SQL Server Management Studio</span></span>
<span data-ttu-id="311ee-112">Verbinding maken met server tooyour in Azure is net als bij verbinding maken met server-exemplaar tooa in uw eigen organisatie.</span><span class="sxs-lookup"><span data-stu-id="311ee-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="311ee-113">Van SSMS, kunt u veel van Hallo dezelfde taken zoals gegevens over het installatieproces of maken van een verwerkingsscript, rollen beheren en gebruiken van PowerShell uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="311ee-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="311ee-115">Download en installeer SSMS</span><span class="sxs-lookup"><span data-stu-id="311ee-115">Download and install SSMS</span></span>
<span data-ttu-id="311ee-116">tooget alle Hallo nieuwste functies en Hallo meest vloeiende ervaring bij het verbinden van tooyour Azure Analysis Services-server, zorg ervoor dat u Hallo meest recente versie van SSMS.</span><span class="sxs-lookup"><span data-stu-id="311ee-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="311ee-117">[SQL Server Management Studio downloaden](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="311ee-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="311ee-118">tooconnect met SSMS</span><span class="sxs-lookup"><span data-stu-id="311ee-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="311ee-119">Wanneer met behulp van SSMS, voordat u verbinding maakt tooyour Hallo van server eerst, zorg er dan voor dat uw gebruikersnaam is opgenomen in Hallo Analysis Services-beheerdersgroep.</span><span class="sxs-lookup"><span data-stu-id="311ee-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="311ee-120">toolearn meer, Zie [serverbeheerders](#server-administrators) verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="311ee-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="311ee-121">Voordat u verbinding maakt, moet u tooget Hallo servernaam.</span><span class="sxs-lookup"><span data-stu-id="311ee-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="311ee-122">In **Azure-portal** > server > **overzicht** > **servernaam**, kopie Hallo servernaam.</span><span class="sxs-lookup"><span data-stu-id="311ee-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="311ee-124">In SSMS > **Objectverkenner**, klikt u op **Connect** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="311ee-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="311ee-125">In Hallo **verbinding tooServer** in het dialoogvenster Plakken Hallo-servernaam, vervolgens in **verificatie**, kies een van de volgende verificatietypen Hallo:</span><span class="sxs-lookup"><span data-stu-id="311ee-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="311ee-126">**Windows-verificatie** toouse uw Windows-referenties voor domein\gebruikersnaam en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="311ee-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="311ee-127">**Active Directory-wachtwoordverificatie** toouse een organisatieaccount.</span><span class="sxs-lookup"><span data-stu-id="311ee-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="311ee-128">Bijvoorbeeld, wanneer verbinding maakt vanaf een niet-domein lid zijn van computer.</span><span class="sxs-lookup"><span data-stu-id="311ee-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="311ee-129">**Verificatie van Active Directory-universele** toouse [niet-interactieve of multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="311ee-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Verbinding maken in SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="311ee-131">Serverbeheerders en databasegebruikers</span><span class="sxs-lookup"><span data-stu-id="311ee-131">Server administrators and database users</span></span>
<span data-ttu-id="311ee-132">Er zijn twee typen van gebruikers, beheerders en databasegebruikers in Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="311ee-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="311ee-133">Beide typen gebruikers, moeten in uw Azure Active Directory en moeten worden opgegeven met de organisatie-e-mailadres of de UPN.</span><span class="sxs-lookup"><span data-stu-id="311ee-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="311ee-134">toolearn meer, Zie [verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="311ee-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="311ee-135">Het oplossen van problemen met de verbinding</span><span class="sxs-lookup"><span data-stu-id="311ee-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="311ee-136">Wanneer u verbinding maakt met behulp van SSMS, als u op problemen stuit, moet u wellicht tooclear Hallo aanmelding cache.</span><span class="sxs-lookup"><span data-stu-id="311ee-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="311ee-137">Er is niets is in de cache toodisc.</span><span class="sxs-lookup"><span data-stu-id="311ee-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="311ee-138">verbinding maken proces tooclear Hallo cache, sluiten en opnieuw opstarten Hallo.</span><span class="sxs-lookup"><span data-stu-id="311ee-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="311ee-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="311ee-139">Next steps</span></span>
<span data-ttu-id="311ee-140">Als u al een model in tabelvorm tooyour nieuwe server nog niet hebt geïmplementeerd, is een goed moment.</span><span class="sxs-lookup"><span data-stu-id="311ee-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="311ee-141">toolearn meer, Zie [tooAzure Analysis Services implementeren](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="311ee-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="311ee-142">Als u een model tooyour-server hebt geïmplementeerd, bent u klaar tooconnect tooit met behulp van een client of de browser.</span><span class="sxs-lookup"><span data-stu-id="311ee-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="311ee-143">toolearn meer, Zie [gegevens ophalen uit Azure Analysis Services-server](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="311ee-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

