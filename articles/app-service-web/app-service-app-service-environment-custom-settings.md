---
title: Aangepaste instellingen voor App Service-omgevingen
description: Aangepaste configuratie-instellingen voor App Service-omgevingen
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 687475fae0c90713c15e8abbb92b71059eae81c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="b2185-103">Aangepaste configuratie-instellingen voor App Service-omgevingen</span><span class="sxs-lookup"><span data-stu-id="b2185-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="b2185-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b2185-104">Overview</span></span>
<span data-ttu-id="b2185-105">Omdat App Service-omgevingen beperkt tot één klant zijn, zijn er bepaalde configuratie-instellingen die uitsluitend op App Service-omgevingen kunnen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="b2185-105">Because App Service Environments are isolated to a single customer, there are certain configuration settings that can be applied exclusively to App Service Environments.</span></span> <span data-ttu-id="b2185-106">In dit artikel worden de verschillende specifieke aanpassingen die beschikbaar voor App Service-omgevingen zijn.</span><span class="sxs-lookup"><span data-stu-id="b2185-106">This article documents the various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="b2185-107">Als u geen App Service-omgeving, Zie [het maken van een App-serviceomgeving](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="b2185-107">If you do not have an App Service Environment, see [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="b2185-108">U kunt de App Service-omgeving aanpassingen opslaan met behulp van een matrix in de nieuwe **clusterSettings** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b2185-108">You can store App Service Environment customizations by using an array in the new **clusterSettings** attribute.</span></span> <span data-ttu-id="b2185-109">Dit kenmerk is gevonden in de woordenlijst 'Eigenschappen' van de *hostingEnvironments* Azure Resource Manager-entiteit.</span><span class="sxs-lookup"><span data-stu-id="b2185-109">This attribute is found in the "Properties" dictionary of the *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="b2185-110">De volgende afgekort Resource Manager-sjabloon codefragment bevat de **clusterSettings** kenmerk:</span><span class="sxs-lookup"><span data-stu-id="b2185-110">The following abbreviated Resource Manager template snippet shows the **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="b2185-111">De **clusterSettings** kenmerk kan worden opgenomen in een Resource Manager-sjabloon voor het bijwerken van de App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="b2185-111">The **clusterSettings** attribute can be included in a Resource Manager template to update the App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-to-update-an-app-service-environment"></a><span data-ttu-id="b2185-112">Azure Resource Explorer gebruiken voor het bijwerken van een App-serviceomgeving</span><span class="sxs-lookup"><span data-stu-id="b2185-112">Use Azure Resource Explorer to update an App Service Environment</span></span>
<span data-ttu-id="b2185-113">U kunt ook de App Service-omgeving bijwerken met behulp van [Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b2185-113">Alternatively, you can update the App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="b2185-114">In Resource Explorer, gaat u naar het knooppunt voor de App Service-omgeving (**abonnementen** > **resourceGroups** > **providers**  >  **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="b2185-114">In Resource Explorer, go to the node for the App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="b2185-115">Klik vervolgens op de specifieke App Service-omgeving, die u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b2185-115">Then click the specific App Service Environment that you want to update.</span></span>
2. <span data-ttu-id="b2185-116">Klik in het rechterdeelvenster **lezen/schrijven** in de bovenste werkbalk om toe te staan interactieve bewerken in Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="b2185-116">In the right pane, click **Read/Write** in the upper toolbar to allow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="b2185-117">Klik op de blauwe **bewerken** knop om te zorgen dat de Resource Manager-sjabloon worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="b2185-117">Click the blue **Edit** button to make the Resource Manager template editable.</span></span>
4. <span data-ttu-id="b2185-118">Ga naar de onderkant van het rechter deelvenster.</span><span class="sxs-lookup"><span data-stu-id="b2185-118">Scroll to the bottom of the right pane.</span></span> <span data-ttu-id="b2185-119">De **clusterSettings** kenmerk helemaal onder, kunt u opgeven of werk de waarde is.</span><span class="sxs-lookup"><span data-stu-id="b2185-119">The **clusterSettings** attribute is at the very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="b2185-120">Typ (of kopieer en plak) de matrix van configuratiewaarden die u wilt dat in de **clusterSettings** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b2185-120">Type (or copy and paste) the array of configuration values you want in the **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="b2185-121">Klik op de groene **plaatsen** knop die aan de bovenkant van het rechter deelvenster doorvoeren van de wijziging aan de App Service-omgeving heeft gevonden.</span><span class="sxs-lookup"><span data-stu-id="b2185-121">Click the green **PUT** button that's located at the top of the right pane to commit the change to the App Service Environment.</span></span>

<span data-ttu-id="b2185-122">Maar u de wijziging dient, duurt het ongeveer 30 minuten vermenigvuldigd met het nummer van de front-ends in de App Service-omgeving om de wijziging van kracht te laten worden.</span><span class="sxs-lookup"><span data-stu-id="b2185-122">However you submit the change, it takes roughly 30 minutes multiplied by the number of front ends in the App Service Environment for the change to take effect.</span></span>
<span data-ttu-id="b2185-123">Bijvoorbeeld, als een App Service-omgeving vier front-ends heeft, duurt het ongeveer twee uur voor de configuratie-update te voltooien.</span><span class="sxs-lookup"><span data-stu-id="b2185-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for the configuration update to finish.</span></span> <span data-ttu-id="b2185-124">Tijdens het wijzigen van de configuratie uitgerold, geen andere vergroten/verkleinen operations of configuratie wijzigen-bewerkingen kunnen worden uitgevoerd in App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="b2185-124">While the configuration change is being rolled out, no other scaling operations or configuration change operations can take place in the App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="b2185-125">TLS 1.0 uitschakelen</span><span class="sxs-lookup"><span data-stu-id="b2185-125">Disable TLS 1.0</span></span>
<span data-ttu-id="b2185-126">Een terugkerende vraag van klanten, vooral klanten die zijn betreft de PCI-naleving audits, is het TLS 1.0 expliciet uitschakelen voor hun apps.</span><span class="sxs-lookup"><span data-stu-id="b2185-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how to explicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="b2185-127">TLS 1.0 kan worden uitgeschakeld via de volgende **clusterSettings** post:</span><span class="sxs-lookup"><span data-stu-id="b2185-127">TLS 1.0 can be disabled through the following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="b2185-128">Volgorde van wijziging TLS-coderingssuites</span><span class="sxs-lookup"><span data-stu-id="b2185-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="b2185-129">Een andere vraag van klanten is als ze de lijst met door de server onderhandeld coderingen wijzigen en dit kan worden gerealiseerd kunnen door het wijzigen van de **clusterSettings** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b2185-129">Another question from customers is if they can modify the list of ciphers negotiated by their server and this can be achieved by modifying the **clusterSettings** as shown below.</span></span> <span data-ttu-id="b2185-130">De lijst met coderingssuites die beschikbaar kan worden opgehaald uit [deze MSDN-artikel](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="b2185-130">The list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="b2185-131">Als onjuiste waarden worden ingesteld voor de coderingssuite die SChannel kan niet begrijpt, kan alle TLS-communicatie met de server mogelijk niet meer.</span><span class="sxs-lookup"><span data-stu-id="b2185-131">If incorrect values are set for the cipher suite that SChannel cannot understand, all TLS communication to your server might stop functioning.</span></span> <span data-ttu-id="b2185-132">In dat geval moet u verwijderen de *FrontEndSSLCipherSuiteOrder* vermelding uit **clusterSettings** en het verzenden van de bijgewerkte Resource Manager-sjabloon als u wilt terugkeren naar de standaard coderingssuite Instellingen.</span><span class="sxs-lookup"><span data-stu-id="b2185-132">In such a case, you will need to remove the *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit the updated Resource Manager template to revert back to the default cipher suite settings.</span></span>  <span data-ttu-id="b2185-133">Wees voorzichtig met deze functionaliteit gebruik.</span><span class="sxs-lookup"><span data-stu-id="b2185-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="b2185-134">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="b2185-134">Get started</span></span>
<span data-ttu-id="b2185-135">De Azure Quickstart-Resource Manager sjabloonsite bevat een sjabloon met de basisdefinitie voor [maken van een App-serviceomgeving](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="b2185-135">The Azure Quickstart Resource Manager template site includes a template with the base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
