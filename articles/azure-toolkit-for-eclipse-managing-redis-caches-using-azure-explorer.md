---
title: Azure Explorer voor Eclipse aaaManaging met behulp van Redis-Caches Hallo | Microsoft Docs
description: Meer informatie over hoe toomanage uw Azure redis cache met behulp van hello Azure Explorer voor Eclipse.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a>Beheren van Redis-Caches hello Azure Explorer gebruiken voor Eclipse

Hello Azure Explorer, die deel uitmaakt van hello Azure Toolkit voor Eclipse, Java-ontwikkelaars met een eenvoudig-en-klare oplossing voor het beheren van redis-caches in de Azure-account uit in Eclipse IDE Hallo biedt.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>Een Redis-Cache maken met behulp van Eclipse

Hallo stappen doorlopen Hallo stappen toocreate een redis-cache met behulp van hello Azure Explorer.

1. Meld u aan tooyour Azure-account met Hallo stappen in Hallo [aanmelding In instructies voor het hello Azure Toolkit voor Eclipse] artikel.

1. In Hallo **Azure Explorer** venster hulpprogramma uit, vouw Hallo **Azure** knooppunt met de rechtermuisknop op **Redis-Caches**, en klik vervolgens op **Redis-Cache maken**.

   ![Menu voor Redis-Cache maken][CR01]

1. Wanneer Hallo **nieuwe Redis-Cache** dialoogvenster wordt weergegeven, Hallo volgende opties opgeven:

   ![Dialoogvenster Nieuwe Redis-Cache maken][CR02]

   a. **DNS-naam**: Hiermee geeft u de DNS-subdomein Hallo voor Hallo nieuwe redis-cache, dat wordt voorafgegaan te '. redis.cache.windows .net "; bijvoorbeeld: *wingtiptoys.redis.cache.windows.net*.

   b. **Abonnement**: Hiermee geeft u hello Azure-abonnement u toouse voor de nieuwe redis-cache hello wilt.

   c. **Resourcegroep**: Hiermee geeft u de resourcegroep Hallo voor redis-cache; moet u toochoose Hallo volgende opties:
      * **Maken van nieuw**: geeft aan dat u wilt dat toocreate een nieuwe resourcegroep.
      * **Gebruik bestaande**: Hiermee geeft u op dat u uit een lijst met resourcegroepen die zijn gekoppeld aan uw Azure-account kiest.

   d. **Locatie**: Hiermee geeft u Hallo-locatie waar uw redis-cache wordt gemaakt; bijvoorbeeld *VS-West*.

   e. **Prijscategorie**: Hiermee geeft u op welke prijscategorie uw redis-cache wordt gebruikt; deze instelling bepaalt u het aantal clientverbindingen Hallo. (Zie voor meer informatie [Redis-Cache prijzen].)

   f. **Niet-SSL-poort**: Hiermee geeft u op of de redis-cache niet-SSL-verbindingen toestaat; standaard SSL-verbindingen zijn toegestaan.

1. Wanneer u alle instellingen van uw redis-cache hebt opgegeven, klikt u op **OK**.

Nadat uw redis-cache is gemaakt, wordt deze in hello Azure Explorer worden weergegeven.

   ![Redis-Cache in Azure Explorer][CR03]

> [!NOTE]
>
> Voor meer informatie over het configureren van uw Azure redis-cache-instellingen, Zie [hoe tooconfigure Azure Redis-Cache].
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a>Hallo-eigenschappen voor uw Redis-Cache in Eclipse weergeven

1. In Azure Explorer hello, met de rechtermuisknop op uw redis-cache en klik op **eigenschappen weergeven**.

   ![Azure Explorer toodisplay eigenschappen van contextmenu voor een redis-cache][SP01]

1. Hello Azure Explorer weergeven Hallo-eigenschappen voor uw redis-cache

   ![Eigenschappen van Redis-cache][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>Verwijderen van uw Redis-Cache met behulp van Eclipse

1. In Azure Explorer hello, met de rechtermuisknop op uw redis-cache en klik op **verwijderen**.

   ![Azure Explorer context menu toodelete een redis-cache][DE01]

1. Klik op **OK** wanneer u daarom wordt gevraagd toodelete redis-cache.

   ![Prompt voor redis-cache verwijderen][DE02]

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Zie voor meer informatie over Azure redis-caches, configuratie-instellingen en prijzen Hallo koppelingen te volgen:

* [Azure Redis-cache]
* [Redis-Cache-documentatie]
* [Redis-Cache prijzen]
* [hoe tooconfigure Azure Redis-Cache]

<!-- URL List -->

[Redis-Cache prijzen]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis-cache]: https://azure.microsoft.com/services/cache/
[Redis-Cache-documentatie]: ./redis-cache/index.md
[hoe tooconfigure Azure Redis-Cache]: ./redis-cache/cache-configure.md
[aanmelding In instructies voor het hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
