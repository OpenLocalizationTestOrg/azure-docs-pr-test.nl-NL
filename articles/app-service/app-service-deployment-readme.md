---
title: aaaDeploying toepassingen tooAzure App Service
description: Meer informatie over de werking van tooDeploy toepassingen tooApp Service
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
ms.openlocfilehash: 925341e12daf3cb05b25199f5c5218e82f062f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-deployment-overview"></a><span data-ttu-id="0935e-104">Overzicht van de Azure App Service-implementatie</span><span class="sxs-lookup"><span data-stu-id="0935e-104">Azure App Service Deployment Overview</span></span>
<span data-ttu-id="0935e-105">Azure App Service biedt een uitgebreide en geïntegreerde functieset toosupport krachtige en flexibele implementatiewerkstromen maken.</span><span class="sxs-lookup"><span data-stu-id="0935e-105">Azure App Service provides a rich and integrated feature set toosupport creating powerful and flexible deployment workflows.</span></span> <span data-ttu-id="0935e-106">Opties, zoals continue integratie of lokale broncodebeheer publiceert, WebDeploy en FTP kan gebruikmaken van App-implementatie.</span><span class="sxs-lookup"><span data-stu-id="0935e-106">App deployment can leverage options that include continuous integration or local source control publishing, WebDeploy, and FTP.</span></span> <span data-ttu-id="0935e-107">Hallo aanbevolen methode voor productie-app-implementatie is implementatiesleuf wisselen.</span><span class="sxs-lookup"><span data-stu-id="0935e-107">hello recommended method for production app deployment is deployment slot swap.</span></span> <span data-ttu-id="0935e-108">Implementatiesites vertegenwoordigen faserings- en integratie omgevingen die zijn gekoppeld aan apps die productie.</span><span class="sxs-lookup"><span data-stu-id="0935e-108">Deployment slots represent staging and integration environments associated with production apps.</span></span> <span data-ttu-id="0935e-109">Implementatiesites kunnen worden geconfigureerd en toegepast op webverkeer voor validatie en verkeer worden ingewisseld op aanvraag voor implementatie tooproduction met niets uitvaltijd en geautomatiseerde opgewarmd.</span><span class="sxs-lookup"><span data-stu-id="0935e-109">Deployment slots can be configured and targeted with web traffic for validation, and traffic can be swapped on demand for deployment tooproduction with no down time and automated warm-up.</span></span> <span data-ttu-id="0935e-110">Hallo stappen van een implementatiewerkstroom kunnen eenvoudig via release management producten zoals Visual Studio Release Management worden geautomatiseerd.</span><span class="sxs-lookup"><span data-stu-id="0935e-110">hello steps of a deployment workflow can be easily automated via release management products such as Visual Studio Release Management.</span></span> <span data-ttu-id="0935e-111">Dit is handig voor coördinatie met een andere oplossing resources (bijvoorbeeld gegevens opslaan), terugkeerpatroon en replicatie over meerdere van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="0935e-111">This is useful for coordination with other solution resources (e.g. data store), recurrence, and replication across multiple units of deployment.</span></span> 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

