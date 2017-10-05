---
title: On-premises gegevensgateway installeren | Microsoft Docs
description: Informatie over het installeren en configureren van een On-premises data gateway.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: 6ef296fb98478be9240f0231c8ad39cd2a0af995
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="05e65-103">Installeren en configureren van een lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="05e65-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="05e65-104">Een lokale gegevensgateway is vereist wanneer een of meer Azure Analysis Services-servers in dezelfde regio verbinding met on-premises gegevensbronnen maken.</span><span class="sxs-lookup"><span data-stu-id="05e65-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in the same region connect to on-premises data sources.</span></span> <span data-ttu-id="05e65-105">Zie voor meer informatie over de gateway, [On-premises gegevensgateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="05e65-105">To learn more about the gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05e65-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="05e65-106">Prerequisites</span></span>
<span data-ttu-id="05e65-107">**Minimale vereisten:**</span><span class="sxs-lookup"><span data-stu-id="05e65-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="05e65-108">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="05e65-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="05e65-109">64-bits versie van Windows 7 / Windows Server 2008 R2 (of hoger)</span><span class="sxs-lookup"><span data-stu-id="05e65-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="05e65-110">**Aanbevolen:**</span><span class="sxs-lookup"><span data-stu-id="05e65-110">**Recommended:**</span></span>

* <span data-ttu-id="05e65-111">8-core CPU</span><span class="sxs-lookup"><span data-stu-id="05e65-111">8 Core CPU</span></span>
* <span data-ttu-id="05e65-112">8 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="05e65-112">8 GB Memory</span></span>
* <span data-ttu-id="05e65-113">64-bits versie van Windows 2012 R2 (of hoger)</span><span class="sxs-lookup"><span data-stu-id="05e65-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="05e65-114">**Belangrijke overwegingen:**</span><span class="sxs-lookup"><span data-stu-id="05e65-114">**Important considerations:**</span></span>

* <span data-ttu-id="05e65-115">Tijdens de installatie bij het registreren van uw gateway met Azure, is de standaardregio voor uw abonnement geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="05e65-115">During setup, when registering your gateway with Azure, the default region for your subscription is selected.</span></span> <span data-ttu-id="05e65-116">U kunt een andere regio.</span><span class="sxs-lookup"><span data-stu-id="05e65-116">You can choose a different region.</span></span> <span data-ttu-id="05e65-117">Als u servers in meer dan één regio hebt, moet u een gateway voor elke regio.</span><span class="sxs-lookup"><span data-stu-id="05e65-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="05e65-118">De gateway kan niet worden geïnstalleerd op een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="05e65-118">The gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="05e65-119">Slechts één gateway kan worden geïnstalleerd op een enkele computer.</span><span class="sxs-lookup"><span data-stu-id="05e65-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="05e65-120">De gateway installeren op een computer waarop blijft op en gaat niet naar de slaapstand.</span><span class="sxs-lookup"><span data-stu-id="05e65-120">Install the gateway on a computer that remains on and does not go to sleep.</span></span>
* <span data-ttu-id="05e65-121">Installeer de gateway niet op een computer draadloos verbonden met uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="05e65-121">Do not install the gateway on a computer wirelessly connected to your network.</span></span> <span data-ttu-id="05e65-122">Prestaties kan afnemen.</span><span class="sxs-lookup"><span data-stu-id="05e65-122">Performance can be diminished.</span></span>


## <span data-ttu-id="05e65-123"><a name="download"></a>Downloaden</span><span class="sxs-lookup"><span data-stu-id="05e65-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="05e65-124">De gateway downloaden</span><span class="sxs-lookup"><span data-stu-id="05e65-124">Download the gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="05e65-125"><a name="install"></a>Installeren</span><span class="sxs-lookup"><span data-stu-id="05e65-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="05e65-126">Voer de installatie.</span><span class="sxs-lookup"><span data-stu-id="05e65-126">Run setup.</span></span>

2. <span data-ttu-id="05e65-127">Selecteer een locatie en klik vervolgens op de voorwaarden accepteren **installeren**.</span><span class="sxs-lookup"><span data-stu-id="05e65-127">Select a location, accept the terms, and then click **Install**.</span></span>

   ![Installeren van de locatie en de licentievoorwaarden](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="05e65-129">Selecteer **On-premises gegevensgateway (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="05e65-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="05e65-130">Azure Analysis Services biedt geen ondersteuning voor persoonlijke modus.</span><span class="sxs-lookup"><span data-stu-id="05e65-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Kies het type gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="05e65-132">Geef een account aan te melden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="05e65-132">Enter an account to sign in to Azure.</span></span> <span data-ttu-id="05e65-133">De account moet zich in uw tenant Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05e65-133">The account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="05e65-134">Dit account wordt gebruikt voor de gatewaybeheerder.</span><span class="sxs-lookup"><span data-stu-id="05e65-134">This account is used for the gateway administrator.</span></span> 

   ![Geef een account aan te melden bij Azure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="05e65-136">Als u zich met een domeinaccount aanmeldt, worden deze toegewezen aan uw organisatieaccount in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05e65-136">If you sign in with a domain account, it will be mapped to your organizational account in Azure AD.</span></span> <span data-ttu-id="05e65-137">Account van uw organisatie worden gebruikt als de beheerder van de gateway.</span><span class="sxs-lookup"><span data-stu-id="05e65-137">Your organizational account will be used as the the gateway administrator.</span></span>

## <span data-ttu-id="05e65-138"><a name="register"></a>Registreren</span><span class="sxs-lookup"><span data-stu-id="05e65-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="05e65-139">Om een gateway-resource maken in Azure, moet u het lokale exemplaar dat u hebt geïnstalleerd met de Gateway-Cloudservice registreren.</span><span class="sxs-lookup"><span data-stu-id="05e65-139">In order to create a gateway resource in Azure, you must register the local instance you installed with the Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="05e65-140">Selecteer **registreren van een nieuwe gateway op deze computer**.</span><span class="sxs-lookup"><span data-stu-id="05e65-140">Select **Register a new gateway on this computer**.</span></span>

    ![Registreren](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="05e65-142">Typ een naam en herstel de sleutel voor uw gateway.</span><span class="sxs-lookup"><span data-stu-id="05e65-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="05e65-143">De gateway gebruikt standaard standaardwaarde regio van uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="05e65-143">By default, the gateway uses your subscription's default region.</span></span> <span data-ttu-id="05e65-144">Als u een andere regio selecteren moet, selecteert u **wijziging regio**.</span><span class="sxs-lookup"><span data-stu-id="05e65-144">If you need to select a different region, select **Change Region**.</span></span>

   ![Registreren](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="05e65-146"><a name="create-resource"></a>Een Azure-gateway-resource maken</span><span class="sxs-lookup"><span data-stu-id="05e65-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="05e65-147">Nadat u hebt geïnstalleerd en uw gateway is geregistreerd, moet u een gateway-resource maken in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="05e65-147">After you've installed and registered your gateway, you need to create a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="05e65-148">Aanmelden bij Azure met dezelfde account die u hebt gebruikt bij het registreren van de gateway.</span><span class="sxs-lookup"><span data-stu-id="05e65-148">Sign in to Azure with the same account you used when registering the gateway.</span></span>

1. <span data-ttu-id="05e65-149">Klik in de Azure-portal op **een nieuwe service maken** > **Enterprise Integration** > **On-premises gegevensgateway** > **maken**.</span><span class="sxs-lookup"><span data-stu-id="05e65-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Een gateway-resource maken](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="05e65-151">In **verbinding-gateway maken**, voer de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="05e65-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="05e65-152">**Naam**: Voer een naam voor uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="05e65-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="05e65-153">**Abonnement**: Selecteer de Azure-abonnement wilt koppelen aan uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="05e65-153">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="05e65-154">Dit abonnement moet uw servers bevinden zich in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="05e65-154">This subscription should be the same subscription your servers are in.</span></span>
   
      <span data-ttu-id="05e65-155">Het standaardabonnement is gebaseerd op het Azure-account dat u gebruikt voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="05e65-155">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="05e65-156">**Resourcegroep**: maak een resourcegroep of selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="05e65-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="05e65-157">**Locatie**: Selecteer de regio die u uw gateway in geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="05e65-157">**Location**: Select the region you registered your gateway in.</span></span>

    * <span data-ttu-id="05e65-158">**De naam van de installatie**: als uw gateway-installatie niet is geselecteerd, selecteert u de gateway is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="05e65-158">**Installation Name**: If your gateway installation isn't already selected, select the gateway registered.</span></span> 

    <span data-ttu-id="05e65-159">Wanneer u bent klaar, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="05e65-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="05e65-160"><a name="connect-servers"></a>Verbinding maken met servers van de gateway-resource</span><span class="sxs-lookup"><span data-stu-id="05e65-160"><a name="connect-servers"></a>Connect servers to the gateway resource</span></span>

1. <span data-ttu-id="05e65-161">Klik in het overzicht Azure Analysis Services-server op **On-Premises Data Gateway**.</span><span class="sxs-lookup"><span data-stu-id="05e65-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Server-gateway verbinding maken](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="05e65-163">In **een On-Premises Data Gateway om verbinding te kiezen**, selecteer uw gateway-resource en klik vervolgens op **verbinding maken met geselecteerde gatewayapparaat**.</span><span class="sxs-lookup"><span data-stu-id="05e65-163">In **Pick an On-Premises Data Gateway to connect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Verbinding maken met server gateway-resource](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="05e65-165">Als uw gateway niet wordt weergegeven in de lijst, wordt de server is waarschijnlijk dat niet bij dezelfde regio bevinden als de regio u hebt opgegeven bij het registreren van de gateway.</span><span class="sxs-lookup"><span data-stu-id="05e65-165">If your gateway does not appear in the list, your server is likely not in the same region as the region you specified when registering the gateway.</span></span> 

<span data-ttu-id="05e65-166">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="05e65-166">That's it.</span></span> <span data-ttu-id="05e65-167">Als u wilt openen van poorten of problemen oplost, moet u uitchecken [On-premises gegevensgateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="05e65-167">If you need to open ports or do any troubleshooting, be sure to check out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05e65-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="05e65-168">Next steps</span></span>
* [<span data-ttu-id="05e65-169">Analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="05e65-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="05e65-170">Gegevens ophalen uit Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="05e65-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
