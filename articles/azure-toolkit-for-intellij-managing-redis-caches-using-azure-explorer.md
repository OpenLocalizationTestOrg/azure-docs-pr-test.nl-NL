---
title: Het beheren van Redis-cache met behulp van de Azure-Explorer voor IntelliJ | Microsoft Docs
description: Informatie over het beheren van uw Azure redis-caches met behulp van de Azure-Explorer voor IntelliJ.
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
ms.openlocfilehash: 9ab8ae17ee2a92b5b16d2210366c00b5b8023fa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-redis-caches-using-the-azure-explorer-for-intellij"></a>Met de Azure-Explorer voor IntelliJ Redis-Caches beheren

De Azure-Explorer, die deel van de Azure-werkset voor IntelliJ uitmaakt, biedt de redis-caches in de Azure-account uit binnen de IntelliJ IDE voor Java-ontwikkelaars met een eenvoudig-en-klare oplossing voor het beheren van.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-intellij"></a>Een Redis-Cache maken met behulp van IntelliJ

De volgende stappen maakt u de stappen voor het maken van een redis-cache met behulp van de Azure-Explorer.

1. Aanmelden bij uw Azure-account met behulp van de stappen in de [aanmelding In instructies voor de Azure-werkset voor IntelliJ] artikel.

1. In de **Azure Explorer** venster hulpprogramma uit, vouw de **Azure** knooppunt met de rechtermuisknop op **Redis-Caches**, en klik vervolgens op **Redis-Cache maken**.

   ![Menu Redis-Cache maken][CR01]

1. Wanneer de **nieuwe Redis-Cache** dialoogvenster wordt weergegeven, geeft u de volgende opties:

   ![Dialoogvenster Nieuwe Redis-Cache maken][CR02]

   a. **DNS-naam**: Hiermee geeft u het DNS-subdomein voor de nieuwe redis-cache, die functienaam worden geplaatst om '. redis.cache.windows.net "; bijvoorbeeld: *wingtiptoys.redis.cache.windows.net*.

   b. **Abonnement**: Hiermee geeft u het Azure-abonnement u wilt gebruiken voor de nieuwe redis-cache.

   c. **Resourcegroep**: Hiermee geeft u de resourcegroep voor uw redis-cache; u moet een van de volgende opties kiezen:
      * **Maken van nieuw**: geeft aan dat u wilt maken van een nieuwe resourcegroep.
      * **Gebruik bestaande**: Hiermee geeft u op dat u uit een lijst met resourcegroepen die zijn gekoppeld aan uw Azure-account kiest.

   d. **Locatie**: Hiermee geeft u de locatie waar uw redis-cache wordt gemaakt; bijvoorbeeld *VS-West*.

   e. **Prijscategorie**: Hiermee geeft u op welke prijscategorie uw redis-cache wordt gebruikt; deze instelling bepaalt u het aantal verbindingen van clients. (Zie voor meer informatie [Redis-Cache prijzen].)

   f. **Niet-SSL-poort**: Hiermee geeft u op of de redis-cache niet-SSL-verbindingen toestaat; standaard SSL-verbindingen zijn toegestaan.

1. Wanneer u alle instellingen van uw redis-cache hebt opgegeven, klikt u op **OK**.

Nadat uw redis-cache is gemaakt, wordt deze weergegeven in de Azure-Explorer.

   ![Redis-Cache in Azure Explorer][CR03]

> [!NOTE]
>
> Voor meer informatie over het configureren van uw Azure redis-cache-instellingen, Zie [het configureren van Azure Redis-Cache].
>

## <a name="display-the-properties-for-your-redis-cache-in-intellij"></a>De eigenschappen voor uw Redis-Cache in IntelliJ weergeven

1. In de Azure-Explorer met de rechtermuisknop op uw redis-cache en klikt u op **eigenschappen weergeven**.

   ![Azure Explorer contextmenu Eigenschappen weergeven voor een redis-cache][SP01]

1. De Azure-Explorer geeft de eigenschappen voor uw redis-cache.

   ![Eigenschappen van Redis-cache][SP02]

## <a name="delete-your-redis-cache-by-using-intellij"></a>Verwijderen van uw Redis-Cache met behulp van IntelliJ

1. In de Azure-Explorer met de rechtermuisknop op uw redis-cache en klikt u op **verwijderen**.

   ![Azure Explorer contextmenu een redis-cache verwijderen][DE01]

1. Klik op **Ja** wanneer u wordt gevraagd uw redis-cache verwijderen.

   ![Prompt voor redis-cache verwijderen][DE02]

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Zie de volgende koppelingen voor meer informatie over Azure redis-caches, configuratie-instellingen en prijzen:

* [Azure Redis-cache]
* [Redis-Cache-documentatie]
* [Redis-Cache prijzen]
* [het configureren van Azure Redis-Cache]

<!-- URL List -->

[Redis-Cache prijzen]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis-cache]: https://azure.microsoft.com/services/cache/
[Redis-Cache-documentatie]: ./redis-cache/index.md
[het configureren van Azure Redis-Cache]: ./redis-cache/cache-configure.md
[aanmelding In instructies voor de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md (Aanmeldingsinstructies voor de Azure Toolkit voor IntelliJ)

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-redis-caches-using-azure-explorer/DE02.png
