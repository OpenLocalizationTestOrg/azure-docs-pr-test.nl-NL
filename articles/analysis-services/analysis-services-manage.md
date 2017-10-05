---
title: Azure analyseservices beheren | Microsoft Docs
description: Informatie over het beheren van een Analysis Services-server in Azure.
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
ms.openlocfilehash: b897e81351ebee11c292e67ac76ba8202a6f0108
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="cbea6-103">Analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="cbea6-103">Manage Analysis Services</span></span>
<span data-ttu-id="cbea6-104">Als u een Analysis Services-server hebt gemaakt in Azure, worden sommige administratie en beheer taken moet u meteen of later opnieuw uitvoeren op de weg.</span><span class="sxs-lookup"><span data-stu-id="cbea6-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="cbea6-105">Voer bijvoorbeeld verwerking naar de gegevens vernieuwen, bepalen wie toegang de modellen op uw server of controleren van de status van uw server.</span><span class="sxs-lookup"><span data-stu-id="cbea6-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="cbea6-106">Bepaalde beheertaken kunnen alleen worden uitgevoerd in Azure-portal anderen in SQL Server Management Studio (SSMS), en sommige taken kunnen worden uitgevoerd op een.</span><span class="sxs-lookup"><span data-stu-id="cbea6-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="cbea6-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cbea6-107">Azure portal</span></span>
<span data-ttu-id="cbea6-108">[Azure-portal](http://portal.azure.com/) is waar u kunt maken en verwijderen van servers, serverbronnen bewaken, grootte wijzigen en beheren wie toegang heeft tot uw servers.</span><span class="sxs-lookup"><span data-stu-id="cbea6-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="cbea6-109">Als u problemen ondervindt, kunt u ook een verzoek om ondersteuning te verzenden.</span><span class="sxs-lookup"><span data-stu-id="cbea6-109">If you're having some problems, you can also submit a support request.</span></span>

![Servernaam bepalen in Azure](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="cbea6-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="cbea6-111">SQL Server Management Studio</span></span>
<span data-ttu-id="cbea6-112">Verbinding maken met uw server in Azure is net als de verbinding te maken met een exemplaar van de server in uw eigen organisatie.</span><span class="sxs-lookup"><span data-stu-id="cbea6-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="cbea6-113">Van SSMS, kunt u veel van dezelfde taken zoals gegevens over het installatieproces uitvoeren of maken van een verwerkingsscript, rollen beheren en PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cbea6-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="cbea6-115">Download en installeer SSMS</span><span class="sxs-lookup"><span data-stu-id="cbea6-115">Download and install SSMS</span></span>
<span data-ttu-id="cbea6-116">Als u de nieuwste functies en de meest vloeiende ervaring bij het verbinden met uw Azure Analysis Services-server, moet u de nieuwste versie van SSMS.</span><span class="sxs-lookup"><span data-stu-id="cbea6-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="cbea6-117">[SQL Server Management Studio downloaden](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="cbea6-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="cbea6-118">Verbinding maken met SSMS</span><span class="sxs-lookup"><span data-stu-id="cbea6-118">To connect with SSMS</span></span>
 <span data-ttu-id="cbea6-119">Wanneer u SSMS, voordat u verbinding maakt met de server het eerst gebruikt, zorg er dan voor dat uw gebruikersnaam is opgenomen in de Analysis Services-beheerdersgroep.</span><span class="sxs-lookup"><span data-stu-id="cbea6-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="cbea6-120">Zie voor meer informatie, [serverbeheerders](#server-administrators) verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="cbea6-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="cbea6-121">Voordat u verbinding maakt, moet u de naam van de server ophalen.</span><span class="sxs-lookup"><span data-stu-id="cbea6-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="cbea6-122">In **Azure Portal** > server > **Overview** > **Servernaam**,kopieer de servernaam.</span><span class="sxs-lookup"><span data-stu-id="cbea6-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Servernaam bepalen in Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="cbea6-124">In SSMS > **Objectverkenner**, klikt u op **Connect** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="cbea6-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="cbea6-125">In de **verbinding maken met Server** in het dialoogvenster Plakken in de naam van de server vervolgens in **verificatie**, kies een van de volgende verificatietypen:</span><span class="sxs-lookup"><span data-stu-id="cbea6-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>
   
    <span data-ttu-id="cbea6-126">**Windows-verificatie** om uw Windows-referenties voor domein\gebruikersnaam en het wachtwoord te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cbea6-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="cbea6-127">**Active Directory-wachtwoordverificatie** om een organisatie-account te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cbea6-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="cbea6-128">Bijvoorbeeld, wanneer verbinding maakt vanaf een niet-domein lid zijn van computer.</span><span class="sxs-lookup"><span data-stu-id="cbea6-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="cbea6-129">**Verificatie van Active Directory-universele** gebruiken [niet-interactieve of multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cbea6-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![Verbinding maken in SSMS](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="cbea6-131">Serverbeheerders en databasegebruikers</span><span class="sxs-lookup"><span data-stu-id="cbea6-131">Server administrators and database users</span></span>
<span data-ttu-id="cbea6-132">Er zijn twee typen van gebruikers, beheerders en databasegebruikers in Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="cbea6-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="cbea6-133">Beide typen gebruikers, moeten in uw Azure Active Directory en moeten worden opgegeven met de organisatie-e-mailadres of de UPN.</span><span class="sxs-lookup"><span data-stu-id="cbea6-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="cbea6-134">Raadpleeg voor meer informatie [Verificatie en gebruikersmachtigingen](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="cbea6-134">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="cbea6-135">Het oplossen van problemen met de verbinding</span><span class="sxs-lookup"><span data-stu-id="cbea6-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="cbea6-136">Wanneer u verbinding maakt met behulp van SSMS, als u op problemen stuit, moet u wellicht de aanmeldings-cache wissen.</span><span class="sxs-lookup"><span data-stu-id="cbea6-136">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="cbea6-137">Niets in cache wordt opgeslagen op schijf. Schakel de cache, sluiten en opnieuw starten van het proces connect.</span><span class="sxs-lookup"><span data-stu-id="cbea6-137">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cbea6-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cbea6-138">Next steps</span></span>
<span data-ttu-id="cbea6-139">Als u dit nog niet hebt al een model in tabelvorm geïmplementeerd naar de nieuwe server, is een goed moment.</span><span class="sxs-lookup"><span data-stu-id="cbea6-139">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="cbea6-140">Zie [Implementeren naar Azure Analysis Services](analysis-services-deploy.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cbea6-140">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="cbea6-141">Als u een model hebt geïmplementeerd met de server, bent u klaar om te verbinden met met behulp van een client of de browser.</span><span class="sxs-lookup"><span data-stu-id="cbea6-141">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="cbea6-142">Zie voor meer informatie, [gegevens ophalen uit Azure Analysis Services-server](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="cbea6-142">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

