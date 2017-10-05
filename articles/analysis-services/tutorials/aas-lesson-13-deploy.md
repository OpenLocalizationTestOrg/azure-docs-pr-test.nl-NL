---
title: 'Azure Analysis Services-zelfstudie - Les 13: Implementeren | Microsoft Docs'
description: In deze les wordt beschreven hoe u het zelfstudieproject implementeert in Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/17/2017
ms.author: owend
ms.openlocfilehash: 70dbf5786262f75199270aa8009e03b9b48b8559
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="8bea7-103">Les 13: Implementeren</span><span class="sxs-lookup"><span data-stu-id="8bea7-103">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="8bea7-104">In deze les gaat u eigenschappen voor de implementatie configureren. U gaat een Azure Analysis Services-server voor implementatie en een naam voor het model opgeven.</span><span class="sxs-lookup"><span data-stu-id="8bea7-104">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server to deploy to and a name for the model.</span></span> <span data-ttu-id="8bea7-105">Vervolgens implementeert u het model naar dat exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8bea7-105">You then deploy the model to that instance.</span></span> <span data-ttu-id="8bea7-106">Na de implementatie van het model kunnen gebruikers er via een rapportageclienttoepassing verbinding mee maken.</span><span class="sxs-lookup"><span data-stu-id="8bea7-106">After your model is deployed, users can connect to it by using a reporting client application.</span></span> <span data-ttu-id="8bea7-107">Zie [Implementeren naar Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8bea7-107">To learn more, see [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="8bea7-108">Geschatte tijd voor het voltooien van deze les: **5 minuten**</span><span class="sxs-lookup"><span data-stu-id="8bea7-108">Estimated time to complete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="8bea7-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8bea7-109">Prerequisites</span></span>  
<span data-ttu-id="8bea7-110">Dit onderwerp maakt deel uit van een zelfstudie over het ontwerpen van een tabellair model. De lessen van de zelfstudie moeten op volgorde worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8bea7-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="8bea7-111">Voordat u de taken in deze les gaat uitvoeren, moet u de vorige les hebben voltooid: [Les 12: Analyseren in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="8bea7-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="8bea7-112">U hebt [beheerdersmachtigingen](../analysis-services-server-admins.md) nodig voor de externe Analysis Services-server om hiernaar te kunnen implementeren.</span><span class="sxs-lookup"><span data-stu-id="8bea7-112">You must have [Administrator permissions](../analysis-services-server-admins.md) on the remote Analysis Services server in-order to deploy to it.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="8bea7-113">Als u de voorbeelddatabase AdventureWorksDW2014 hebt geïnstalleerd op een on-premises SQL Server en u uw model implementeert naar een Azure Analysis Services-server, is een [on-premises gegevensgateway](../analysis-services-gateway.md) vereist.</span><span class="sxs-lookup"><span data-stu-id="8bea7-113">If you installed the AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-the-model"></a><span data-ttu-id="8bea7-114">Het model implementeren</span><span class="sxs-lookup"><span data-stu-id="8bea7-114">Deploy the model</span></span>  
  
#### <a name="to-configure-deployment-properties"></a><span data-ttu-id="8bea7-115">Implementatie-eigenschappen configureren:</span><span class="sxs-lookup"><span data-stu-id="8bea7-115">To configure deployment properties</span></span>  

  
1.  <span data-ttu-id="8bea7-116">Klik in **Solution Explorer** met de rechtermuisknop op het project **AW Internet Sales** en klik vervolgens op **Properties**.</span><span class="sxs-lookup"><span data-stu-id="8bea7-116">In **Solution Explorer**, right-click the **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="8bea7-117">Voer bij de eigenschap **Server** onder **Deployment Server** in het dialoogvenster **AW Internet Sales Property Pages** de volledige server in.</span><span class="sxs-lookup"><span data-stu-id="8bea7-117">In the **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in the **Server** property, enter the full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="8bea7-119">Typ **Adventure Works Internet Sales** voor de eigenschap **Database**.</span><span class="sxs-lookup"><span data-stu-id="8bea7-119">In the **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="8bea7-120">Typ **Adventure Works Internet Sales Model** voor de eigenschap **Model Name**.</span><span class="sxs-lookup"><span data-stu-id="8bea7-120">In the **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="8bea7-121">Controleer de invoer en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bea7-121">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a><span data-ttu-id="8bea7-122">Het model Adventure Works Internet Sales implementeren:</span><span class="sxs-lookup"><span data-stu-id="8bea7-122">To deploy the Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="8bea7-123">Klik in **Solution Explorer** met de rechtermuisknop op het project **AW Internet Sales** > **Build**.</span><span class="sxs-lookup"><span data-stu-id="8bea7-123">In **Solution Explorer**, right-click the **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="8bea7-124">Klik met de rechtermuisknop op het project **AW Internet Sales** > **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="8bea7-124">Right-click the **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="8bea7-125">Als u implementeert naar Azure Analysis Services, wordt u mogelijk gevraagd om uw account.</span><span class="sxs-lookup"><span data-stu-id="8bea7-125">When deploying to Azure Analysis Services, you may be prompted to enter your account.</span></span> <span data-ttu-id="8bea7-126">Voer in dat geval uw organisatieaccount en het bijbehorende wachtwoord in, zoals nancy@adventureworks.com. Dit account moet een beheerdersaccount zijn op de server.</span><span class="sxs-lookup"><span data-stu-id="8bea7-126">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on the server.</span></span>
  
    <span data-ttu-id="8bea7-127">Het dialoogvenster Deploy wordt weergegeven en toont de implementatiestatus van de metagegevens en tabellen die zijn opgenomen in het model.</span><span class="sxs-lookup"><span data-stu-id="8bea7-127">The Deploy dialog box appears and displays the deployment status of the metadata and each table included in the model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="8bea7-129">Als de implementatie is voltooid, kunt u op **Close** klikken.</span><span class="sxs-lookup"><span data-stu-id="8bea7-129">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="8bea7-130">Conclusie</span><span class="sxs-lookup"><span data-stu-id="8bea7-130">Conclusion</span></span>  
<span data-ttu-id="8bea7-131">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="8bea7-131">Congratulations!</span></span> <span data-ttu-id="8bea7-132">U bent klaar met het ontwerpen en implementeren van uw eerste tabellaire model van Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="8bea7-132">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="8bea7-133">Deze zelfstudie heeft u stapsgewijs begeleid bij het uitvoeren van de algemene taken voor het maken van een tabellair model.</span><span class="sxs-lookup"><span data-stu-id="8bea7-133">This tutorial has helped guide you through completing the most common tasks in creating a tabular model.</span></span> <span data-ttu-id="8bea7-134">Het model Adventure Works Internet Sales is nu geïmplementeerd. U kunt nu SQL Server Management Studio gebruiken om het model te beheren, en processcripts en een back-upplan te maken.</span><span class="sxs-lookup"><span data-stu-id="8bea7-134">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio to manage the model; create process scripts and a backup plan.</span></span> <span data-ttu-id="8bea7-135">Gebruikers kunnen nu ook verbinding maken met het model met behulp van een rapportageclienttoepassing zoals Microsoft Excel of Power BI.</span><span class="sxs-lookup"><span data-stu-id="8bea7-135">Users can also now connect to the model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="8bea7-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8bea7-137">What's next?</span></span>
<span data-ttu-id="8bea7-138">[Verbinden met Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="8bea7-138">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="8bea7-139">[Aanvullende les: Dynamische beveiliging](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="8bea7-139">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="8bea7-140">[Aanvullende les: Detailrijen](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="8bea7-140">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="8bea7-141">Aanvullende les: Onregelmatige hiërarchieën</span><span class="sxs-lookup"><span data-stu-id="8bea7-141">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
