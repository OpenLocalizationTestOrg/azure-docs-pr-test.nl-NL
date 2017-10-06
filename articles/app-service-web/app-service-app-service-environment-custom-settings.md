---
title: aaaCustom-instellingen voor App Service-omgevingen
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
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="e7b5b-103">Aangepaste configuratie-instellingen voor App Service-omgevingen</span><span class="sxs-lookup"><span data-stu-id="e7b5b-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="e7b5b-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="e7b5b-104">Overview</span></span>
<span data-ttu-id="e7b5b-105">Omdat App Service-omgevingen geïsoleerd tooa één klant zijn, zijn er bepaalde configuratie-instellingen die kunnen worden toegepast uitsluitend tooApp Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="e7b5b-106">Dit artikel worden Hallo diverse specifieke aanpassingen die beschikbaar voor App Service-omgevingen zijn.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="e7b5b-107">Als u geen App Service-omgeving, Zie [hoe tooCreate een App-serviceomgeving](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="e7b5b-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="e7b5b-108">U kunt de App Service-omgeving aanpassingen opslaan met behulp van een matrix in Hallo nieuwe **clusterSettings** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="e7b5b-109">Dit kenmerk is gevonden in de woordenlijst van Hallo 'Eigenschappen' Hallo *hostingEnvironments* Azure Resource Manager-entiteit.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="e7b5b-110">Hallo volgende afgekorte Resource Manager sjabloon fragment toont Hallo **clusterSettings** kenmerk:</span><span class="sxs-lookup"><span data-stu-id="e7b5b-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

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

<span data-ttu-id="e7b5b-111">Hallo **clusterSettings** kenmerk kan worden opgenomen in een Resource Manager sjabloon tooupdate Hallo App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="e7b5b-112">Gebruik Azure Resource Explorer tooupdate een App-serviceomgeving</span><span class="sxs-lookup"><span data-stu-id="e7b5b-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="e7b5b-113">U kunt ook Hallo App Service-omgeving bijwerken met behulp van [Azure Resource Explorer](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7b5b-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="e7b5b-114">Ga in de Resource Explorer toohello knooppunt voor Hallo App Service-omgeving (**abonnementen** > **resourceGroups** > **providers**  >  **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="e7b5b-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="e7b5b-115">Klik vervolgens op Hallo specifieke App Service-omgeving die u wilt tooupdate.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="e7b5b-116">Klik in het rechterdeelvenster hello, **lezen/schrijven** in Hallo bovenste werkbalk tooallow interactieve bewerken in Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="e7b5b-117">Klik op de blauwe Hallo **bewerken** knop toomake Hallo Resource Manager-sjabloon worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="e7b5b-118">Schuif toohello onder in het rechter deelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="e7b5b-119">Hallo **clusterSettings** kenmerk onderin Hallo zeer, kunt u opgeven of werk de waarde is.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="e7b5b-120">Type (of kopiëren en plakken) Hallo-matrix van configuratiewaarden die u in Hallo wilt **clusterSettings** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="e7b5b-121">Klik op Hallo groen **plaatsen** knop die bovenaan Hallo Hallo rechterdeelvenster toocommit Hallo wijziging toohello App Service-omgeving heeft gevonden.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="e7b5b-122">Maar u Hallo wijziging indient, duurt het ongeveer 30 minuten vermenigvuldigd met het aantal front-ends in Hallo App Service-omgeving voor Hallo wijziging tootake effect Hallo.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="e7b5b-123">Bijvoorbeeld, als een App Service-omgeving vier front-ends heeft, duurt het ongeveer twee uur voor Hallo configuratie update toofinish.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="e7b5b-124">Tijdens het Hallo-configuratiewijziging uitgerold, kunnen geen andere bewerkingen vergroten/verkleinen of wijziging configuratiebewerkingen plaatsvinden in Hallo App Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="e7b5b-125">TLS 1.0 uitschakelen</span><span class="sxs-lookup"><span data-stu-id="e7b5b-125">Disable TLS 1.0</span></span>
<span data-ttu-id="e7b5b-126">Een terugkerende vraag van klanten, met name de klanten die zijn betreft de PCI-naleving audits, is hoe tooexplicitly TLS 1.0 uitschakelen voor hun apps.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="e7b5b-127">TLS 1.0 kan worden uitgeschakeld via de volgende Hallo **clusterSettings** post:</span><span class="sxs-lookup"><span data-stu-id="e7b5b-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="e7b5b-128">Volgorde van wijziging TLS-coderingssuites</span><span class="sxs-lookup"><span data-stu-id="e7b5b-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="e7b5b-129">Een andere vraag van klanten is als ze Hallo lijst met door de server onderhandeld coderingen wijzigen en dit kan worden gerealiseerd kunnen door het wijzigen van Hallo **clusterSettings** zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="e7b5b-130">Hallo-overzicht van coderingssuites die beschikbaar kan worden opgehaald uit [deze MSDN-artikel](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e7b5b-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="e7b5b-131">Als onjuiste waarden zijn ingesteld voor Hallo coderingssuite die geen inzicht in SChannel krijgen, alle tooyour server van de TLS-communicatie mogelijk functioneert.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="e7b5b-132">In dat geval moet u tooremove hello *FrontEndSSLCipherSuiteOrder* vermelding uit **clusterSettings** en het verzenden van Hallo Resource Manager sjabloon toorevert back toohello standaard cipher bijgewerkt Suite-instellingen.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="e7b5b-133">Wees voorzichtig met deze functionaliteit gebruik.</span><span class="sxs-lookup"><span data-stu-id="e7b5b-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="e7b5b-134">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="e7b5b-134">Get started</span></span>
<span data-ttu-id="e7b5b-135">Hello Azure Quickstart-Resource Manager-sjabloonsite bevat een sjabloon met de basisdefinitie Hallo voor [maken van een App-serviceomgeving](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="e7b5b-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
