---
title: 'Problemen oplossen: Maken en koppelen van Machine Learning-werkruimte tooa | Microsoft Docs'
description: Oplossingen voor algemene problemen bij het maken en verbinding maken met tooan Azure Machine Learning-werkruimte
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="ddef8-103">Gids voor probleemoplossing: maken en koppelen tooan Machine Learning-werkruimte</span><span class="sxs-lookup"><span data-stu-id="ddef8-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="ddef8-104">Deze handleiding bevat oplossingen voor enkele uitdagingen vaak aangetroffen bij het instellen van Azure Machine Learning-werkruimten.</span><span class="sxs-lookup"><span data-stu-id="ddef8-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="ddef8-105">De eigenaar van de werkruimte</span><span class="sxs-lookup"><span data-stu-id="ddef8-105">Workspace owner</span></span>
<span data-ttu-id="ddef8-106">tooopen een werkruimte in Machine Learning Studio, moet u zijn aangemeld toohello Microsoft-Account gebruikt toocreate Hallo werkruimte of moet u een uitnodiging uit Hallo eigenaar toojoin Hallo werkruimte tooreceive.</span><span class="sxs-lookup"><span data-stu-id="ddef8-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="ddef8-107">U kunt hello Azure-portal Hallo-werkruimte, waaronder Hallo mogelijkheid tooconfigure toegang beheren.</span><span class="sxs-lookup"><span data-stu-id="ddef8-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="ddef8-108">Zie voor meer informatie over het beheren van een werkruimte [beheren van een Azure Machine Learning-werkruimte].</span><span class="sxs-lookup"><span data-stu-id="ddef8-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[beheren van een Azure Machine Learning-werkruimte]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="ddef8-110">Toegestane regio 's</span><span class="sxs-lookup"><span data-stu-id="ddef8-110">Allowed regions</span></span>
<span data-ttu-id="ddef8-111">Machine Learning is momenteel beschikbaar in een beperkt aantal regio's.</span><span class="sxs-lookup"><span data-stu-id="ddef8-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="ddef8-112">Als uw abonnement niet onder een van deze gebieden, wordt er fout het Hallo-bericht, 'U hebt geen abonnementen in Hallo regio's toegestaan.'</span><span class="sxs-lookup"><span data-stu-id="ddef8-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="ddef8-113">toorequest die een regio zijn tooyour abonnement toegevoegd, een nieuw Microsoft-ondersteuningsverzoek maken vanuit hello Azure-portal, kies **facturering** als Hallo probleemtype en volg Hallo vraagt toosubmit uw aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ddef8-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="ddef8-114">Storage-account</span><span class="sxs-lookup"><span data-stu-id="ddef8-114">Storage account</span></span>
<span data-ttu-id="ddef8-115">Hallo Machine Learning-service moet een storage account toostore-gegevens.</span><span class="sxs-lookup"><span data-stu-id="ddef8-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="ddef8-116">U kunt een bestaand opslagaccount gebruiken of u kunt een nieuw opslagaccount maken bij het maken van de nieuwe Machine Learning-werkruimte hello (als u een nieuw opslagaccount quotum toocreate hebt).</span><span class="sxs-lookup"><span data-stu-id="ddef8-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="ddef8-117">Nadat de nieuwe Machine Learning-werkruimte Hallo is gemaakt, kunt u tooMachine Learning Studio aanmelden met behulp van Microsoft-account Hallo toocreate Hallo werkruimte die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ddef8-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="ddef8-118">Als u het foutbericht Hallo tegenkomt, gebruik 'Werkruimte niet gevonden' (vergelijkbaar toohello volgende schermopname), Hallo toodelete stappen te volgen cookies in de browser.</span><span class="sxs-lookup"><span data-stu-id="ddef8-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![Werkruimte niet gevonden][screen3]

<span data-ttu-id="ddef8-120">**browsercookies toodelete**</span><span class="sxs-lookup"><span data-stu-id="ddef8-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="ddef8-121">Als u Internet Explorer gebruikt, klikt u op Hallo **extra** in de rechterbovenhoek Hallo en selecteer **Internetopties**.</span><span class="sxs-lookup"><span data-stu-id="ddef8-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![Internet-opties][screen4]

2. <span data-ttu-id="ddef8-123">Onder Hallo **algemene** tabblad **verwijderen...**</span><span class="sxs-lookup"><span data-stu-id="ddef8-123">Under hello **General** tab, click **Delete…**</span></span>

![Tabblad Algemeen][screen5]

3. <span data-ttu-id="ddef8-125">In Hallo **Browsegeschiedenis verwijderen** dialoogvenster zorg **Cookies en websitegegevens** is geselecteerd en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="ddef8-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Verwijderen van cookies][screen6]

<span data-ttu-id="ddef8-127">Hallo cookies zijn verwijderd, start Hallo browser opnieuw en ga toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) pagina.</span><span class="sxs-lookup"><span data-stu-id="ddef8-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="ddef8-128">Wanneer u wordt gevraagd een gebruikersnaam en wachtwoord, voert u Hallo hetzelfde Microsoft-account toocreate Hallo werkruimte die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ddef8-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="ddef8-129">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ddef8-129">Comments</span></span>

<span data-ttu-id="ddef8-130">Ons doel is toomake Hallo Machine Learning-ervaring zo weinig mogelijk.</span><span class="sxs-lookup"><span data-stu-id="ddef8-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="ddef8-131">Neem na de eventuele opmerkingen en problemen op Hallo [Azure Machine Learning-forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp ons u beter bedienen.</span><span class="sxs-lookup"><span data-stu-id="ddef8-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
