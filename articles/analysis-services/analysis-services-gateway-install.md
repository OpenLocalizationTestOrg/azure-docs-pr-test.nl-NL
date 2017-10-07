---
title: aaaInstall On-premises gegevensgateway | Microsoft Docs
description: Meer informatie over hoe tooinstall en configureer een On-premises data gateway.
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
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="299ad-103">Installeren en configureren van een lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="299ad-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="299ad-104">Een lokale gegevensgateway is vereist wanneer een of meer Azure Analysis Services-servers in Hallo dezelfde regio verbinding tooon-premises gegevensbronnen.</span><span class="sxs-lookup"><span data-stu-id="299ad-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="299ad-105">toolearn meer informatie over het Hallo-gateway, Zie [On-premises gegevensgateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="299ad-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="299ad-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="299ad-106">Prerequisites</span></span>
<span data-ttu-id="299ad-107">**Minimale vereisten:**</span><span class="sxs-lookup"><span data-stu-id="299ad-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="299ad-108">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="299ad-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="299ad-109">64-bits versie van Windows 7 / Windows Server 2008 R2 (of hoger)</span><span class="sxs-lookup"><span data-stu-id="299ad-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="299ad-110">**Aanbevolen:**</span><span class="sxs-lookup"><span data-stu-id="299ad-110">**Recommended:**</span></span>

* <span data-ttu-id="299ad-111">8-core CPU</span><span class="sxs-lookup"><span data-stu-id="299ad-111">8 Core CPU</span></span>
* <span data-ttu-id="299ad-112">8 GB geheugen</span><span class="sxs-lookup"><span data-stu-id="299ad-112">8 GB Memory</span></span>
* <span data-ttu-id="299ad-113">64-bits versie van Windows 2012 R2 (of hoger)</span><span class="sxs-lookup"><span data-stu-id="299ad-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="299ad-114">**Belangrijke overwegingen:**</span><span class="sxs-lookup"><span data-stu-id="299ad-114">**Important considerations:**</span></span>

* <span data-ttu-id="299ad-115">Tijdens de installatie bij het registreren van uw gateway met Azure, is Hallo standaard regio voor uw abonnement geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="299ad-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="299ad-116">U kunt een andere regio.</span><span class="sxs-lookup"><span data-stu-id="299ad-116">You can choose a different region.</span></span> <span data-ttu-id="299ad-117">Als u servers in meer dan één regio hebt, moet u een gateway voor elke regio.</span><span class="sxs-lookup"><span data-stu-id="299ad-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="299ad-118">Hallo-gateway kan niet worden geïnstalleerd op een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="299ad-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="299ad-119">Slechts één gateway kan worden geïnstalleerd op een enkele computer.</span><span class="sxs-lookup"><span data-stu-id="299ad-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="299ad-120">Hallo-gateway installeren op een computer die op blijft en toosleep niet verder.</span><span class="sxs-lookup"><span data-stu-id="299ad-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="299ad-121">Installeer geen Hallo-gateway op een computer tooyour draadloos verbonden netwerk.</span><span class="sxs-lookup"><span data-stu-id="299ad-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="299ad-122">Prestaties kan afnemen.</span><span class="sxs-lookup"><span data-stu-id="299ad-122">Performance can be diminished.</span></span>


## <span data-ttu-id="299ad-123"><a name="download"></a>Downloaden</span><span class="sxs-lookup"><span data-stu-id="299ad-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="299ad-124">Hallo gateway downloaden</span><span class="sxs-lookup"><span data-stu-id="299ad-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="299ad-125"><a name="install"></a>Installeren</span><span class="sxs-lookup"><span data-stu-id="299ad-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="299ad-126">Voer de installatie.</span><span class="sxs-lookup"><span data-stu-id="299ad-126">Run setup.</span></span>

2. <span data-ttu-id="299ad-127">Selecteer een locatie en klik vervolgens op Hallo voorwaarden accepteren **installeren**.</span><span class="sxs-lookup"><span data-stu-id="299ad-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Installeren van de locatie en de licentievoorwaarden](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="299ad-129">Selecteer **On-premises gegevensgateway (aanbevolen)**.</span><span class="sxs-lookup"><span data-stu-id="299ad-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="299ad-130">Azure Analysis Services biedt geen ondersteuning voor persoonlijke modus.</span><span class="sxs-lookup"><span data-stu-id="299ad-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Kies het type gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="299ad-132">Geef een account toosign in tooAzure.</span><span class="sxs-lookup"><span data-stu-id="299ad-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="299ad-133">Hallo-account moet zich in uw tenant Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="299ad-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="299ad-134">Dit account wordt gebruikt voor het Hallo-gatewaybeheerder.</span><span class="sxs-lookup"><span data-stu-id="299ad-134">This account is used for hello gateway administrator.</span></span> 

   ![Geef een account toosign in tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="299ad-136">Als u zich met een domeinaccount aanmeldt, moeten worden toegewezen tooyour organisatieaccount in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="299ad-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="299ad-137">Account van uw organisatie wordt gebruikt als Hallo Hallo gatewaybeheerder.</span><span class="sxs-lookup"><span data-stu-id="299ad-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="299ad-138"><a name="register"></a>Registreren</span><span class="sxs-lookup"><span data-stu-id="299ad-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="299ad-139">In de volgorde toocreate een bron van de gateway in Azure, moet u Hallo lokaal exemplaar die u geïnstalleerd met Hallo Gateway Cloud Service registreren.</span><span class="sxs-lookup"><span data-stu-id="299ad-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="299ad-140">Selecteer **registreren van een nieuwe gateway op deze computer**.</span><span class="sxs-lookup"><span data-stu-id="299ad-140">Select **Register a new gateway on this computer**.</span></span>

    ![Registreren](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="299ad-142">Typ een naam en herstel de sleutel voor uw gateway.</span><span class="sxs-lookup"><span data-stu-id="299ad-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="299ad-143">Hallo-gateway gebruikt standaard standaardwaarde regio van uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="299ad-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="299ad-144">Als u een andere regio tooselect nodig hebt, selecteert u **wijziging regio**.</span><span class="sxs-lookup"><span data-stu-id="299ad-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![Registreren](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="299ad-146"><a name="create-resource"></a>Een Azure-gateway-resource maken</span><span class="sxs-lookup"><span data-stu-id="299ad-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="299ad-147">Nadat u hebt geïnstalleerd en uw gateway is geregistreerd, moet u een gateway-resource toocreate in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="299ad-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="299ad-148">Meld u aan tooAzure Hello dezelfde account die u hebt gebruikt bij het registreren van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="299ad-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="299ad-149">Klik in de Azure-portal op **een nieuwe service maken** > **Enterprise Integration** > **On-premises gegevensgateway** > **maken**.</span><span class="sxs-lookup"><span data-stu-id="299ad-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Een gateway-resource maken](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="299ad-151">In **verbinding-gateway maken**, voer de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="299ad-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="299ad-152">**Naam**: Voer een naam voor uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="299ad-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="299ad-153">**Abonnement**: Selecteer Hallo tooassociate Azure-abonnement met uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="299ad-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="299ad-154">Dit abonnement moet hetzelfde abonnement uw servers bevinden zich in Hallo.</span><span class="sxs-lookup"><span data-stu-id="299ad-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="299ad-155">Hallo standaardabonnement is gebaseerd op Hallo Azure-account waarmee u toosign in.</span><span class="sxs-lookup"><span data-stu-id="299ad-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="299ad-156">**Resourcegroep**: maak een resourcegroep of selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="299ad-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="299ad-157">**Locatie**: Selecteer Hallo regio geregistreerd van uw gateway in.</span><span class="sxs-lookup"><span data-stu-id="299ad-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="299ad-158">**De naam van de installatie**: als uw gateway-installatie niet is geselecteerd, selecteer Hallo gateway is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="299ad-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="299ad-159">Wanneer u bent klaar, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="299ad-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="299ad-160"><a name="connect-servers"></a>Verbinding maken met servers toohello gateway resource</span><span class="sxs-lookup"><span data-stu-id="299ad-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="299ad-161">Klik in het overzicht Azure Analysis Services-server op **On-Premises Data Gateway**.</span><span class="sxs-lookup"><span data-stu-id="299ad-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Verbinding maken met server toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="299ad-163">In **kiezen van een On-Premises Data Gateway tooconnect**, selecteer uw gateway-resource en klik vervolgens op **verbinding maken met geselecteerde gatewayapparaat**.</span><span class="sxs-lookup"><span data-stu-id="299ad-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Verbinding maken met server toogateway-bron](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="299ad-165">Als uw gateway niet wordt weergegeven in de lijst hello, uw server is waarschijnlijk niet in dezelfde regio bevinden als het Hallo-regio die u hebt opgegeven bij het registreren van de gateway Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="299ad-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="299ad-166">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="299ad-166">That's it.</span></span> <span data-ttu-id="299ad-167">Als tooopen poorten of u problemen oplost, moet u ervoor toocheck uit [On-premises gegevensgateway](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="299ad-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="299ad-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="299ad-168">Next steps</span></span>
* [<span data-ttu-id="299ad-169">Analyseservices beheren</span><span class="sxs-lookup"><span data-stu-id="299ad-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="299ad-170">Gegevens ophalen uit Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="299ad-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
