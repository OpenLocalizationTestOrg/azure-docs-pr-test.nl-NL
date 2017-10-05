---
title: Storage-accounts beheren met behulp van de Azure-Explorer voor IntelliJ | Microsoft Docs
description: Informatie over het beheren van uw Azure storage-accounts met behulp van de Azure-Explorer voor IntelliJ.
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a>Storage-accounts beheren met behulp van de Azure-Explorer voor IntelliJ

De Azure-Explorer, die deel van de Azure-werkset voor IntelliJ uitmaakt, biedt Java ontwikkelaars een oplossing eenvoudig te gebruiken voor het beheren van storage-accounts in de Azure-account uit binnen de IntelliJ integrated development environment (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Een opslagaccount in IntelliJ maken

Voor het maken van een opslagaccount met behulp van de Azure-Explorer, het volgende doen:

1. Aanmelden bij uw Azure-account met behulp van de [aanmelden instructies voor de Azure-werkset voor Eclipse]. 

2. In de **Azure Explorer** weergeven, vouw de **Azure** knooppunt met de rechtermuisknop op **Opslagaccounts**, en klik vervolgens op **Storage-Account maken**.

   ![Opdracht voor Storage-Account maken][CS01]

3. In de **Storage-Account maken** dialoogvenster geeft u de volgende opties:

   ![Dialoogvenster Nieuw Opslagaccount maken][CS02]

   * **Naam**: Hiermee geeft u de naam voor het nieuwe opslagaccount.

   * **Account kind**: geeft het type opslagaccount maken (bijvoorbeeld 'Blob storage'). Zie voor meer informatie [over Azure storage-accounts]. 

   * **Prestaties**: Hiermee geeft u op welke storage-account met gebruik van de geselecteerde uitgever (bijvoorbeeld 'Premium'). Zie voor meer informatie [Azure storage schaalbaarheids- en prestatiedoelen]. 

   * **Replicatie**: Hiermee geeft u de replicatie voor het opslagaccount (bijvoorbeeld ' Zone-redundante'). Zie voor meer informatie [Azure storage-replicatie]. 

   * **Abonnement**: Hiermee geeft u de Azure-abonnement dat u wilt gebruiken voor het nieuwe opslagaccount.

   * **Locatie**: Hiermee geeft u de locatie waar uw storage-account wordt gemaakt (bijvoorbeeld 'West ons').

   * **Resourcegroep**: Hiermee geeft u de resourcegroep voor uw virtuele machine. Selecteer een van de volgende opties:
      * **Maken van nieuwe**: geeft aan dat u wilt maken van een nieuwe resourcegroep.
      * **Gebruik bestaande**: Hiermee geeft u op dat u selecteert in een lijst met resourcegroepen die gekoppeld aan uw Azure-account zijn.

4. Wanneer u alle van de voorgaande opties hebt opgegeven, klikt u op **OK**.

## <a name="create-a-storage-container-in-intellij"></a>Storage-container in IntelliJ maken

Voor het maken van een storage-container met de Verkenner Azure, het volgende doen:

1. In de weergave Azure Explorer met de rechtermuisknop op het opslagaccount waar u een container maken en klik vervolgens op **maken blob-container**.

   ![Opdracht voor blob-container maken][CC01]

2. In de **maken blob-container** in het dialoogvenster geeft de naam voor de container en klik vervolgens op **OK**. Zie voor meer informatie over de naamgeving van storage-containers [Naming en verwijzen naar containers, blobs en metagegevens].

   ![Dialoogvenster Storage-Container maken][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Een opslagcontainer voor in IntelliJ verwijderen

Als u wilt een opslagcontainer verwijderen met behulp van de Azure-Explorer, het volgende doen:

1. In de weergave Azure Explorer met de rechtermuisknop op de storage-container en klik vervolgens op **verwijderen**.

   ![Storage-container opdracht verwijderen][DC01]

2. Klik in het bevestigingsvenster **Ja**.

   ![Storage-container bevestigingsvenster verwijderen][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Een opslagaccount in IntelliJ verwijderen

Als u wilt een opslagaccount verwijderen met behulp van de Azure-Explorer, het volgende doen:

1. In de **Azure Explorer** bekijken, met de rechtermuisknop op het opslagaccount en selecteer vervolgens **verwijderen**.

   ![Menu voor storage-account verwijderen][DS01]

2. Klik in het bevestigingsvenster **Ja**.

   ![Bevestigingsvenster storage-account verwijderen][DS02]

## <a name="next-steps"></a>Volgende stappen
Zie de volgende bronnen voor meer informatie over Azure storage-accounts, grootten en prijzen:

* [Inleiding tot Microsoft Azure Storage]
* [over Azure storage-accounts]
* Grootten van Azure storage-account
  * [Grootten voor Windows storage-accounts in Azure]
  * [Grootten voor Linux-accounts voor opslag in Azure]
* Prijzen voor Azure storage-account
  * [Prijzen voor Windows storage-account]
  * [Prijzen voor Linux-opslagaccount]

Zie de volgende bronnen voor meer informatie over Azure Toolkits voor IDE voor Java:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in de Azure-werkset voor Eclipse]
  * [Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)
  * [aanmelden instructies voor de Azure-werkset voor Eclipse]
  * [Een Hallo wereld-web-app maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in de Azure-werkset voor IntelliJ]
  * [Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)
  * [Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]
  * [Een Hallo wereld-web-app maken voor Azure in IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)
[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)
[aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

[Inleiding tot Microsoft Azure Storage]: /azure/storage/storage-introduction
[over Azure storage-accounts]: /azure/storage/storage-create-storage-account
[Azure storage-replicatie]: /azure/storage/storage-redundancy
[Schaalbaarheid van de Azure-opslag- en prestatiedoelen]: /azure/storage/storage-scalability-targets
[Naming en verwijzen naar containers, blobs en metagegevens]: http://go.microsoft.com/fwlink/?LinkId=255555

[Grootten voor Windows storage-accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Grootten voor Linux-accounts voor opslag in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Prijzen voor Windows storage-account]: /pricing/details/virtual-machines/windows/
[Prijzen voor Linux-opslagaccount]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
