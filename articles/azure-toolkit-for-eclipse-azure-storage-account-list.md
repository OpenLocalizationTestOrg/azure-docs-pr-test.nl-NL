---
title: Lijst met Azure Storage-Account
description: De instellingen van uw storage-account met de Azure-Toolkit voor Eclipse beheren
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
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a>Lijst met Azure Storage-Account
Azure storage-accounts inschakelen downloadlocaties moet worden gebruikt voor uw JDK, toepassingsserver en willekeurige onderdelen, evenals voor het opslaan van status wanneer u opslaan in cache. Eclipse houdt een lijst van bekende opslagaccounts die beschikbaar voor uw projecten in uw Eclipse-werkruimte zijn. Openen van de **Opslagaccounts** dialoogvenster dat wordt gebruikt voor het beheren van deze lijst, in Eclipse, klikt u op **venster**, klikt u op **voorkeuren**, vouw **Azure**, en klik vervolgens op **Storage-Accounts**.

Het volgende bevat de **Opslagaccounts** dialoogvenster.

![][ic719496]

Dit dialoogvenster kan ook worden geopend vanuit een **Accounts** op dialoogvensters met storage-accounts, zoals de volgende koppeling:

* De **JDK** tabblad van de **serverconfiguratie** dialoogvenster.
* De **Server** tabblad van de **serverconfiguratie** dialoogvenster.
* De **onderdeel toevoegen** dialoogvenster.
* De **opslaan in cache** dialoogvenster met eigenschappen.

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a>Uw storage-accounts met behulp van een bestand met publicatie-instellingen importeren
1. Binnen de **Opslagaccounts** dialoogvenster, klikt u op **importeren uit bestand publiceren instellingen**.

2. (Deze stap overslaan als u al een bestand met publicatie-instellingen hebt opgeslagen op uw lokale computer). In de **importeren abonnementsgegevens** dialoogvenster, klikt u op **publiceren-SETTINGS-bestand downloaden**. Als u nog niet aangemeld bij uw Azure-account, wordt u gevraagd om aan te melden. U wordt vervolgens gevraagd te Sla een Azure bestand publicatie-instellingen. (Kunt u de resulterende instructies op de pagina's voor aanmelding - negeren ze worden geleverd door de Azure-portal en zijn bedoeld voor gebruikers van de Visual Studio.) Sla deze op uw lokale computer.

3. Nog steeds in de **importeren abonnementsgegevens** dialoogvenster, klikt u op de **Bladeren** , selecteer het instellingenbestand publiceren die u eerder hebt lokaal opgeslagen en klik vervolgens op **Open**.

4. Klik op **OK** sluiten de **importeren abonnementsgegevens** dialoogvenster.

## <a name="to-create-a-new-storage-account"></a>Een nieuw opslagaccount maken
1. Binnen de **Opslagaccounts** dialoogvenster, klikt u op **toevoegen**.

2. Binnen de **Storage-Account toevoegen** dialoogvenster, klikt u op **nieuw**.

3. Binnen de **nieuw Opslagaccount** dialoogvenster waarden opgeven voor het volgende:

   * De naam van opslagaccount.

   * Locatie van het opslagaccount.

   * Beschrijving van het opslagaccount.

   * Het abonnement waaraan het opslagaccount hoort.

4. Klik op **OK** sluiten de **nieuw Opslagaccount** dialoogvenster.

Het kan enkele minuten duren voordat uw storage-account moet worden gemaakt. Nadat deze is gemaakt, klikt u op **OK** sluiten de **Storage-Account toevoegen** dialoogvenster en uw nieuwe opslagaccount wordt toegevoegd aan de lijst met beschikbare storage-accounts.

## <a name="to-add-an-existing-storage-account-to-the-list"></a>Een bestaand opslagaccount toevoegen aan de lijst
1. Als u nog geen Azure storage-account, maken door de stappen die worden vermeld in de **voor het maken van een nieuwe sectie van de storage-account** hierboven. (U kunt ook kunt u een nieuw opslagaccount op de [Azure Management Portal][Azure Management Portal].)

2. Binnen de **Opslagaccounts** dialoogvenster, klikt u op **toevoegen**.

3. Binnen de **Storage-Account toevoegen** dialoogvenster waarden opgeven voor **naam** en **toegangssleutel**. De naam en toegangssleutel van het account moet voor een bestaand Azure-opslagaccount. Gebruik de **opslag** sectie van de [Azure Management Portal] [ Azure Management Portal] om de namen van opslagaccounts en de sleutels weer te geven. Uw **Storage-Account toevoegen** dialoogvenster ziet er ongeveer als volgt.
   
   ![][ic719497]

4. Klik op **OK** sluiten de **Storage-Account toevoegen** dialoogvenster.

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a>Een opslagaccount voor het gebruik van een nieuwe toegangssleutel wijzigen
1. Binnen de **Opslagaccounts** dialoogvenster, klikt u op de opslag account dat u wilt bewerken en klik vervolgens op **bewerken**.

2. Binnen de **bewerken toegangssleutel voor Opslagaccount** dialoogvenster wijzigen de **toegangssleutel** waarde.

3. Klik op **OK** sluiten de **bewerken toegangssleutel voor Opslagaccount** dialoogvenster.

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a>Een opslagaccount verwijderen uit de lijst die wordt bijgehouden in Eclipse
1. Binnen de **Opslagaccounts** dialoogvenster, klikt u op de opslag account dat u wilt bewerken en klik vervolgens op **verwijderen**.

2. Klik op **OK** wanneer u wordt gevraagd de storage-account te verwijderen.

> [!NOTE]
> Verwijderen van het opslagaccount via de **Opslagaccounts** dialoogvenster is alleen verwijderd uit de lijst met opslagaccounts worden bekeken in Eclipse. Deze verwijdert niet de storage-account van uw Azure-abonnement. Daarnaast het storage-account kan worden weergegeven opnieuw in de lijst met nadat Eclipse opnieuw de details van uw abonnement laadt.
> 
> 

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse] 

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
