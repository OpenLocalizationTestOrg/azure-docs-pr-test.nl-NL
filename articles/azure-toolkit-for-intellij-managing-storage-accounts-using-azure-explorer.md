---
title: storage-accounts met behulp van aaaManage hello Azure Explorer voor IntelliJ | Microsoft Docs
description: Meer informatie over hoe toomanage uw Azure-opslag gebruikersaccounts met behulp hello Azure Explorer voor IntelliJ.
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
ms.openlocfilehash: b094bdcd2fa2782cb12b67c96ac406fbe4c1aa3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-intellij"></a>Storage-accounts beheren met behulp van hello Azure Explorer voor IntelliJ

Hello Azure Explorer, die deel van hello Azure Toolkit voor IntelliJ uitmaakt, Java-ontwikkelaars met een eenvoudig-en-klare oplossing biedt voor het beheren van opslagaccounts in het Azure-account via binnen Hallo IntelliJ integrated development environment (IDE).

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a>Een opslagaccount in IntelliJ maken

een opslagaccount met behulp van hello Azure Explorer toocreate Hallo te volgen:

1. Meld u aan tooyour Azure-account met behulp van Hallo [aanmelden instructies voor het hello Azure Toolkit voor Eclipse]. 

2. In Hallo **Azure Explorer** weergeven, vouwt u Hallo **Azure** knooppunt met de rechtermuisknop op **Opslagaccounts**, en klik vervolgens op **Storage-Account maken**.

   ![Opdracht voor Storage-Account maken][CS01]

3. In Hallo **Storage-Account maken** dialoogvenster geeft u de Hallo volgende opties:

   ![Dialoogvenster Nieuw Opslagaccount maken][CS02]

   * **Naam**: Hiermee geeft u Hallo-naam voor het nieuwe opslagaccount Hallo.

   * **Account kind**: Hiermee geeft u Hallo type storage account toocreate (bijvoorbeeld ' Blob-opslag'). Zie voor meer informatie [over Azure storage-accounts]. 

   * **Prestaties**: Hiermee geeft u op welke opslagaccount toouse aanbieding van de geselecteerde uitgever hello (bijvoorbeeld 'Premium'). Zie voor meer informatie [Azure storage schaalbaarheids- en prestatiedoelen]. 

   * **Replicatie**: Hiermee geeft u de replicatie Hallo voor Hallo storage-account (bijvoorbeeld ' Zone-redundante'). Zie voor meer informatie [Azure storage-replicatie]. 

   * **Abonnement**: Hiermee geeft u hello Azure-abonnement dat u voor het nieuwe opslagaccount hello toouse wilt.

   * **Locatie**: Hiermee geeft u Hallo-locatie waar uw storage-account wordt gemaakt (bijvoorbeeld 'West ons').

   * **Resourcegroep**: Hiermee geeft u de resourcegroep Hallo voor uw virtuele machine. Selecteer een Hallo volgende opties:
      * **Maken van nieuwe**: geeft aan dat u wilt dat toocreate een nieuwe resourcegroep.
      * **Gebruik bestaande**: Hiermee geeft u op dat u selecteert in een lijst met resourcegroepen die gekoppeld aan uw Azure-account zijn.

4. Wanneer u alle Hallo voorgaande opties hebt opgegeven, klikt u op **OK**.

## <a name="create-a-storage-container-in-intellij"></a>Storage-container in IntelliJ maken

een opslagcontainer met behulp van hello Azure Explorer toocreate Hallo te volgen:

1. Hallo Azure Verkenner-weergave, met de rechtermuisknop op Hallo opslagaccount waar toocreate een container en klik vervolgens op **maken blob-container**.

   ![Opdracht voor blob-container maken][CC01]

2. In Hallo **maken blob-container** in het dialoogvenster Hallo naam opgeven voor de container en klik vervolgens op **OK**. Zie voor meer informatie over de naamgeving van storage-containers [Naming en verwijzen naar containers, blobs en metagegevens].

   ![Dialoogvenster Storage-Container maken][CC02]

## <a name="delete-a-storage-container-in-intellij"></a>Een opslagcontainer voor in IntelliJ verwijderen

een opslagcontainer met behulp van hello Azure Explorer toodelete Hallo te volgen:

1. Met de rechtermuisknop op Hallo storage-container in hello Azure Verkenner-weergave, en klik vervolgens op **verwijderen**.

   ![Storage-container opdracht verwijderen][DC01]

2. Klik in het bevestigingsvenster hello, **Ja**.

   ![Storage-container bevestigingsvenster verwijderen][DC02]

## <a name="delete-a-storage-account-in-intellij"></a>Een opslagaccount in IntelliJ verwijderen

een opslagaccount met behulp van hello Azure Explorer toodelete Hallo te volgen:

1. In Hallo **Azure Explorer** bekijken, met de rechtermuisknop op Hallo storage-account en selecteer vervolgens **verwijderen**.

   ![Menu voor storage-account verwijderen][DS01]

2. Klik in het bevestigingsvenster hello, **Ja**.

   ![Bevestigingsvenster storage-account verwijderen][DS02]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Azure storage-accounts, grootten en prijzen Hallo resources te volgen:

* [Inleiding tooMicrosoft Azure Storage]
* [over Azure storage-accounts]
* Grootten van Azure storage-account
  * [Grootten voor Windows storage-accounts in Azure]
  * [Grootten voor Linux-accounts voor opslag in Azure]
* Prijzen voor Azure storage-account
  * [Prijzen voor Windows storage-account]
  * [Prijzen voor Linux-opslagaccount]

Zie voor meer informatie over Azure Toolkits voor IDE voor Java Hallo resources te volgen:

* [Azure Toolkit voor Eclipse]
  * [Wat is er nieuw in hello Azure Toolkit voor Eclipse]
  * [Hello Azure Toolkit voor Eclipse installeren]
  * [aanmelden instructies voor het hello Azure Toolkit voor Eclipse]
  * [Een Hallo wereld-web-app maken voor Azure in Eclipse]
* [Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)
  * [Wat is er nieuw in hello Azure Toolkit voor IntelliJ]
  * [Hello Azure Toolkit voor IntelliJ installeren]
  * [Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]
  * [Een Hallo wereld-web-app maken voor Azure in IntelliJ]

Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ./azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ./azure-toolkit-for-intellij-installation.md
[aanmelden instructies voor het hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

[Inleiding tooMicrosoft Azure Storage]: /azure/storage/storage-introduction
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
