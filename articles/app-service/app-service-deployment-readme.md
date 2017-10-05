---
title: Implementatie van toepassingen in Azure App Service
description: Meer informatie over het implementeren van toepassingen met App Service-werk
keywords: App service, azure app service implementeren, implementatie
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="9ff0b-104">Overzicht van de Azure App Service-implementatie</span><span class="sxs-lookup"><span data-stu-id="9ff0b-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="9ff0b-105">Azure App Service biedt een uitgebreide en geïntegreerde functie ingesteld voor het maken van werkstromen voor de implementatie van krachtige en flexibele.</span><span class="sxs-lookup"><span data-stu-id="9ff0b-105">Azure App Service provides a rich and integrated feature set to support creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="9ff0b-106">Opties, zoals continue integratie of lokale broncodebeheer publiceert, WebDeploy en FTP kan gebruikmaken van App-implementatie.</span><span class="sxs-lookup"><span data-stu-id="9ff0b-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="9ff0b-107">De aanbevolen methode voor productie-app-implementatie is implementatiesleuf wisselen.</span><span class="sxs-lookup"><span data-stu-id="9ff0b-107">The recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="9ff0b-108">Implementatiesites vertegenwoordigen faserings- en integratie omgevingen die zijn gekoppeld aan apps die productie.</span><span class="sxs-lookup"><span data-stu-id="9ff0b-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="9ff0b-109">Implementatiesites kunnen worden geconfigureerd en toegepast op webverkeer voor validatie en verkeer worden ingewisseld op aanvraag voor implementatie naar de productieomgeving geen uitvaltijd en geautomatiseerde opgewarmd.</span><span class="sxs-lookup"><span data-stu-id="9ff0b-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment to production with no down time and automated warm-up.</span></span> <span data-ttu-id="9ff0b-110">De stappen van een werkstroom voor de implementatie kunnen eenvoudig via release management producten zoals Visual Studio Release Management worden geautomatiseerd.</span><span class="sxs-lookup"><span data-stu-id="9ff0b-110">The steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="9ff0b-111">Dit is handig voor coördinatie met een andere oplossing resources (bijvoorbeeld gegevens opslaan), terugkeerpatroon en replicatie over meerdere van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="9ff0b-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

