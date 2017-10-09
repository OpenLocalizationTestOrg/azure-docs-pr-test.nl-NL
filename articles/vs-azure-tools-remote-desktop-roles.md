---
title: Extern bureaublad met de Azure-functies aaaUsing | Microsoft Docs
description: Extern bureaublad gebruiken met Azure-functies
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="dd5c9-103">Extern bureaublad gebruiken met Azure-functies</span><span class="sxs-lookup"><span data-stu-id="dd5c9-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="dd5c9-104">Hello Azure SDK en extern bureaublad-Services gebruikt, kunt u toegang tot Azure-functies en virtuele machines die worden gehost door Azure.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="dd5c9-105">U kunt Extern bureaublad-Services configureren vanuit een Azure-cloud service-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="dd5c9-106">tooenable extern bureaublad-Services, moet u een project werkt met een of meer rollen maken en vervolgens publiceren tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dd5c9-107">U moet toegang tot een Azure-functie voor het oplossen van problemen of alleen-ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="dd5c9-108">Hallo doel van elke virtuele machine is een specifieke functie in uw Azure-toepassing, niet toorun toorun andere clienttoepassingen.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="dd5c9-109">Als u toouse Azure toohost een virtuele machine die u gebruiken voor enig doel wilt kunt, raadpleegt u toegang tot Azure virtuele Machines in Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="dd5c9-110">tooenable en gebruik extern bureaublad voor een Azure-rol</span><span class="sxs-lookup"><span data-stu-id="dd5c9-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="dd5c9-111">Klik in Solution Explorer open Hallo snelmenu voor uw cloud service-project en kies vervolgens **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="dd5c9-112">Hallo **Publish Azure Application** wizard wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![Opdracht voor een Cloud Service-project publiceren](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="dd5c9-114">Hallo onderaan in **Microsoft Azure Publish Settings** pagina van wizard hello, selecteer Hallo **extern bureaublad inschakelen** voor alle functies selectievakje.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="dd5c9-115">Hallo **configuratie voor extern bureaublad** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="dd5c9-116">Hallo Hallo onderaan in **configuratie voor extern bureaublad** dialoogvenster Kies Hallo **meer opties** knop.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="dd5c9-117">U ziet nu een vervolgkeuzelijst waarmee u Maak of Selecteer een certificaat dat u referenties gegevens versleutelen kunt om verbinding te maken via Extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="dd5c9-118">Kies in de vervolgkeuzelijst Hallo  **&lt;maken >**, of kies een bestaande uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="dd5c9-119">Als u een bestaand certificaat kiest, slaat u Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dd5c9-120">Hallo-certificaten die u nodig hebt voor een verbinding met extern bureaublad wijken af van het Hallo-certificaten die u voor andere Azure-bewerkingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="dd5c9-121">Hallo RAS-certificaat moet een persoonlijke sleutel hebben.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="dd5c9-122">Hallo **certificaat maken** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="dd5c9-123">Geef een beschrijvende naam voor het nieuwe certificaat Hallo en kies vervolgens Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="dd5c9-124">Hallo nieuw certificaat wordt weergegeven in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="dd5c9-125">In Hallo **configuratie voor extern bureaublad** dialoogvenster Geef een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="dd5c9-126">U kunt een bestaand account niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-126">You can’t use an existing account.</span></span> <span data-ttu-id="dd5c9-127">Geen beheerder opgeven als de gebruikersnaam Hallo voor Hallo nieuw account.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="dd5c9-128">Als Hallo wachtwoord niet voldoet aan de complexiteitsvereisten hello, verschijnt een rode volgende toohello wachtwoord in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="dd5c9-129">Hallo-wachtwoord moet bevatten hoofdletters, kleine letters en cijfers of symbolen.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="dd5c9-130">Kies een datum op welk account Hallo verloopt en na welke Extern bureaublad-verbindingen worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="dd5c9-131">Nadat u hebt opgegeven alle vereiste gegevens hello, kiest u Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="dd5c9-132">Diverse instellingen waarmee u Remote Access Services worden toohello .cscfg en .csdef-bestanden worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="dd5c9-133">In Hallo **Microsoft Azure Publish Settings** wizard Hallo kiezen **OK** knop wanneer u bent klaar toopublish uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="dd5c9-134">Als u niet klaar toopublish bent, kiest u Hallo **annuleren** knop.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="dd5c9-135">Hallo-configuratie-instellingen worden opgeslagen en u kunt uw cloudservice later publiceren.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="dd5c9-136">Tooan Azure rol verbinding met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="dd5c9-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="dd5c9-137">Nadat u uw cloudservice op Azure hebt gepubliceerd, kunt u Server Explorer toolog in Hallo virtuele machines die Azure als host fungeert.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="dd5c9-138">Vouw in Server Explorer Hallo **Azure** knooppunt, en vouw vervolgens Hallo knooppunt voor een cloudservice en een van de rollen toodisplay een lijst van exemplaren.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="dd5c9-139">Open Hallo snelmenu voor een exemplaar-knooppunt en kies vervolgens **verbinding maken met behulp van extern bureaublad**.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Verbinding maken via Extern bureaublad](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="dd5c9-141">Voer Hallo-gebruikersnaam en wachtwoord die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="dd5c9-142">U bent nu aangemeld bij de externe sessie.</span><span class="sxs-lookup"><span data-stu-id="dd5c9-142">You are now logged into your remote session.</span></span>

