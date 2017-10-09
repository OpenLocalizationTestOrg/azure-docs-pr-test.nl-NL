---
title: aaaCreate een functie-app van hello Azure Portal | Microsoft Docs
description: Een nieuwe functie-app maken in Azure App Service vanuit Hallo-portal.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>Een functie-app maken vanuit hello Azure-portal

Apps van Azure functie maakt gebruik van hello Azure App Service-infrastructuur. Dit onderwerp leest u hoe toocreate een functie-app in hello Azure-portal. Een functie-app is Hallo-container die als host fungeert voor Hallo uitvoering van afzonderlijke functies. Wanneer u een functie-app in Hallo hosting App Service-abonnement maakt, kan uw app in de functie alle Hallo functies van App Service kunt gebruiken.

## <a name="create-a-function-app"></a>Een functie-app maken

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

Wanneer u een functie-app maakt, Geef een geldige **appnaam**, die kunnen alleen letters, cijfers en afbreekstreepjes bevatten. Het onderstrepingsteken (**_**) is niet toegestaan.

Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en mogen alleen cijfers en kleine letters bevatten. De naam van uw opslagaccount moet uniek zijn binnen Azure. 

Nadat Hallo functie-app is gemaakt, kunt u afzonderlijke functies in een of meer verschillende talen. Functies maken [met behulp van de portal Hallo](functions-create-first-azure-function.md#create-function), [continue implementatie](functions-continuous-deployment.md), of door [uploaden met FTP](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp).

## <a name="service-plans"></a>Service-plannen

Azure Functions heeft twee verschillende serviceplannen: verbruik plannings- en App Service-abonnement. rekencapaciteit Hallo verbruik plan automatisch toegewezen wanneer uw code wordt uitgevoerd, kan worden geschaald-out als nodig toohandle laden, en vervolgens kan worden geschaald in wanneer de code wordt niet uitgevoerd. Hallo App Service-abonnement geeft de functie app toegang tooall Hallo faciliteiten van App Service. Als de functie-app wordt gemaakt en kan niet op dit moment worden gewijzigd, moet u uw service-abonnement kiezen. Zie voor meer informatie [Kies een Azure-functies die als host fungeert voor plan](functions-scale.md).

Als u van plan bent toorun JavaScript-functies op een App Service-abonnement, moet u een plan met minder cores kiezen. Zie voor meer informatie, Hallo [verwijzing in JavaScript voor functies](functions-reference-node.md#choose-single-core-app-service-plans).

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>Opslagvereisten voor account

Wanneer u een functie-app in App Service, moet u maken of tooa voor algemene doeleinden Azure Storage-account koppelen die ondersteuning biedt voor opslag voor blobs, wachtrijen en tabellen. Intern functies opslagruimte gebruikt voor bewerkingen zoals het beheren van triggers en functies die logboekregistratie. Sommige opslagaccounts bieden geen ondersteuning voor wachtrijen en tabellen, zoals alleen-blob storage-accounts, Azure Premium-opslag en opslagaccounts waarvoor ZRS-replicatie. Deze accounts worden gefilterd van Hallo Opslagaccount blade bij het maken van een functie-app.

>[!NOTE]
>Wanneer u Hallo verbruik hosting plan, wordt de functie code en binding configuratiebestanden worden opgeslagen in Azure File storage in Hallo belangrijkste storage-account. Wanneer u de belangrijkste opslagaccount Hallo verwijdert, wordt deze inhoud is verwijderd en kan niet worden hersteld.

toolearn meer informatie over opslagaccounttypen, Zie [Introducing hello Azure Storage-Services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services). 

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



