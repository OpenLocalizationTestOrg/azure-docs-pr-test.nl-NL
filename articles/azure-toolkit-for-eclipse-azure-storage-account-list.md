---
title: lijst met Opslagaccounts aaaAzure
description: De instellingen van uw storage-account met hello Azure Toolkit voor Eclipse beheren
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Lijst met Azure Storage-Account
Azure storage accounts inschakelen downloaden locaties toobe gebruikt voor uw JDK, toepassingsserver en willekeurige onderdelen, evenals voor het opslaan van status wanneer u opslaan in cache. Eclipse houdt een lijst met bekende storage-accounts die beschikbaar tooyour projecten in uw Eclipse-werkruimte zijn. Hallo tooopen **Opslagaccounts** dialoogvenster dat wordt gebruikt toomanage die lijst in Eclipse, klikt u op **venster**, klikt u op **voorkeuren**, vouw **Azure** , en klik vervolgens op **Opslagaccounts**.

Hallo hieronder vindt u Hallo **Opslagaccounts** dialoogvenster.

![][ic719496]

Dit dialoogvenster kan ook worden geopend vanuit een **Accounts** koppeling op de dialoogvensters die storage-accounts, zoals Hallo volgende gebruiken:

* Hallo **JDK** tabblad Hallo **serverconfiguratie** dialoogvenster.
* Hallo **Server** tabblad Hallo **serverconfiguratie** dialoogvenster.
* Hallo **onderdeel toevoegen** dialoogvenster.
* Hallo **opslaan in cache** dialoogvenster met eigenschappen.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>tooimport uw opslag gebruikersaccounts via een bestand met publicatie-instellingen
1. Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op **importeren uit bestand publiceren instellingen**.

2. (Deze stap overslaan als u al een publiceren instellingen bestand tooyour lokale computer opgeslagen). In Hallo **importeren abonnementsgegevens** dialoogvenster, klikt u op **publiceren-SETTINGS-bestand downloaden**. Als u nog niet aangemeld bij uw Azure-account, kunt u zich na vragen aan gebruiker toolog in. Vervolgens wordt u gevraagd een Azure toosave bestand publicatie-instellingen. (U kunt resulterende Hallo-instructies weergegeven op pagina's aanmelden van Hallo - negeren ze worden geleverd door hello Azure-portal en zijn bedoeld voor gebruikers van de Visual Studio.) Sla het op de lokale computer tooyour.

3. Nog steeds in Hallo **importeren abonnementsgegevens** dialoogvenster, klikt u op Hallo **Bladeren** knop, selecteer Hallo bestand publicatie-instellingen die u eerder hebt lokaal opgeslagen en klik vervolgens op **openen**.

4. Klik op **OK** tooclose hello **importeren abonnementsgegevens** dialoogvenster.

## <a name="toocreate-a-new-storage-account"></a>een nieuw opslagaccount toocreate
1. Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op **toevoegen**.

2. Binnen Hallo **Storage-Account toevoegen** dialoogvenster, klikt u op **nieuw**.

3. Binnen Hallo **nieuw Opslagaccount** dialoogvenster waarden voor Hallo volgende opgeven:

   * De naam van opslagaccount.

   * Locatie van Hallo storage-account.

   * Beschrijving van Hallo storage-account.

   * Hallo abonnement toowhich Hallo storage-account hoort.

4. Klik op **OK** tooclose hello **nieuw Opslagaccount** dialoogvenster.

Het kan enkele minuten duren voordat uw storage-account toobe gemaakt. Nadat deze is gemaakt, klikt u op **OK** tooclose hello **Storage-Account toevoegen** dialoogvenster en uw nieuwe opslagaccount worden toohello lijst met beschikbare opslagaccounts toegevoegd.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>een bestaande lijst van storage account toohello tooadd
1. Als u nog geen een Azure storage-account, maakt u een Hallo stappen te volgen weergegeven in Hallo **toocreate een nieuwe sectie van de storage-account** hierboven. (U kunt ook een nieuw opslagaccount maken op Hallo [Azure Management Portal][Azure Management Portal].)

2. Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op **toevoegen**.

3. Binnen Hallo **Storage-Account toevoegen** dialoogvenster waarden opgeven voor **naam** en **toegangssleutel**. Hallo account naam en toegangssleutel moet zijn voor een bestaand Azure-opslagaccount. Gebruik Hallo **opslag** sectie Hallo [Azure Management Portal] [ Azure Management Portal] tooview uw storage-account namen en -sleutels. Uw **Storage-Account toevoegen** dialoogvenster ziet er vergelijkbare toohello volgende.
   
   ![][ic719497]

4. Klik op **OK** tooclose hello **Storage-Account toevoegen** dialoogvenster.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>een storage account toouse een nieuwe toegangssleutel toomodify
1. Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op Hallo storage-account dat u wilt dat tooedit en klik vervolgens op **bewerken**.

2. Binnen Hallo **bewerken toegangssleutel voor Opslagaccount** dialoogvenster Hallo wijzigen **toegangssleutel** waarde.

3. Klik op **OK** tooclose hello **bewerken toegangssleutel voor Opslagaccount** dialoogvenster.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove een opslagaccount in de lijst Hallo onderhouden in Eclipse
1. Binnen Hallo **Opslagaccounts** dialoogvenster, klikt u op Hallo storage-account dat u wilt dat tooedit en klik vervolgens op **verwijderen**.

2. Klik op **OK** wanneer na vragen aan gebruiker tooremove Hallo storage-account.

> [!NOTE]
> Verwijderen van opslagaccount Hallo via Hallo **Opslagaccounts** dialoogvenster alleen, wordt deze verwijderd uit de lijst Hallo met storage-accounts worden bekeken in Eclipse. Dit wordt niet Hallo storage-account van uw Azure-abonnement verwijderd. Bovendien Hallo storage-account kan worden weergegeven opnieuw in de lijst met nadat Eclipse opnieuw Hallo details van uw abonnement geladen.
> 
> 

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse] 

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
