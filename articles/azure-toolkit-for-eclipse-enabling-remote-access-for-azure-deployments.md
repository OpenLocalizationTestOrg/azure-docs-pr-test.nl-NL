---
title: Externe toegang voor Azure-implementaties in Eclipse aaaEnabling
description: Meer informatie over hoe tooenable van RAS voor Azure met hello Azure Toolkit voor Eclipse-implementaties.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Externe toegang inschakelen voor Azure-implementaties in Eclipse
toohelp oplossen van uw implementaties, mag u inschakelen en gebruiken van externe toegang tooconnect toohello virtuele machine die als host fungeert voor uw implementatie. Hallo functionaliteit voor externe toegang is afhankelijk van Hallo Remote Desktop Protocol (RDP). Nadat u tooAzure hebt gepubliceerd, of als u Eclipse met een Windows-besturingssysteem gebruikt, u externe toegang configureren kunt voordat u tooAzure publiceert, kunt u externe toegang configureert voor uw implementatie. Houd er rekening mee dat u moet een extern-bureaubladclient die compatibel is met het besturingssysteem in volgorde tooconnect tooyour implementatie van virtuele machine in Azure.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>Hoe tooenable RAS voordat u tooAzure implementeren
> [!NOTE]
> tooenable RAS voordat u uw toepassing tooAzure implementeert, moet u toobe Eclipse met Windows.
> 
> 

Hallo volgende afbeelding toont Hallo **RAS** eigenschappenvenster tooenable externe toegang gebruikt.

![][ic719494]

Er zijn twee manieren toodisplay hello **RAS** dialoogvenster met eigenschappen:

* Klik op Hallo **Geavanceerd** koppeling in Hallo **RAS** sectie Hallo **tooAzure publiceren** dialoogvenster.

* Open Hallo **eigenschappen** dialoogvenster van uw Azure-project.

Wanneer u een nieuw project in de Azure-implementatie maakt, project Hallo geen externe toegang is standaard ingeschakeld. Echter, u eenvoudig externe toegang kunt inschakelen door het Hallo-gebruikersnaam en wachtwoord opgeven in Hallo **tooAzure publiceren** dialoogvenster. Hallo RAS-wachtwoord is versleuteld met behulp van x.509-certificaten. Als u geen gebruik geeft u uw eigen certificaat Hallo versleuteling is afhankelijk van een zelfondertekend certificaat met hello Azure Eclipse-invoegtoepassing verzonden. Dit zelfondertekende certificaat is in Hallo **cert** map van uw Azure-project opgeslagen beide als een openbaar certificaat-bestand (SampleRemoteAccessPublic.cer) en als een persoonlijke informatie Exchange (PFX)-certificaat (bestand SampleRemoteAccessPrivate.pfx). laatste Hallo Hallo persoonlijke sleutel voor Hallo certificaat bevat en heeft deze een standaardwachtwoord **Wachtwoord1**. Echter, omdat dit wachtwoord algemeen bekend is, kan Hallo standaardcertificaat moet worden gebruikt alleen voor het leren van de toepassing wordt niet voor een productie-implementatie. Dus anders dan voor het leren van toepassing als u wilt dat externe sessies tooenabled voor uw implementaties, klikt u Hallo **Geavanceerd** koppeling in Hallo **tooAzure publiceren** dialoogvenster toospecify uw eigen certificaat. Houd er rekening mee dat u tooupload Hallo PFX-versie van Hallo certificaat tooyour gehoste service binnen hello Azure Management Portal moet zodanig dat Azure Hallo gebruikerswachtwoord kan ontsleutelen.

Hallo overige Hallo zelfstudie ziet u hoe tooenable van RAS voor een Azure-implementatie-project die aanvankelijk is gemaakt met externe toegang uitgeschakeld. Voor deze zelfstudie maken we een nieuw zelfondertekend certificaat en het pfx-bestand heeft een wachtwoord van uw keuze. U hebt bovendien de optie Hallo van het gebruik van een certificaat zijn uitgegeven door een certificeringsinstantie.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>Hoe tooenable RAS nadat u tooAzure hebt geïmplementeerd
tooenable externe toegang nadat u hebt geïmplementeerd tooAzure, gebruik Hallo stappen te volgen:

1. Meld u aan bij hello Azure management portal met behulp van uw Azure-account

2. In de lijst met **Cloudservices**, selecteer uw geïmplementeerde cloudservice

3. Klik in de Hallo cloud service webpagina op Hallo **configureren** koppeling

4. Klik op Hallo onderaan configuratiepagina Hallo Hallo **externe** koppeling

5. Wanneer de pop-updialoogvenster hello wordt weergegeven:
   
   * Geef Hallo rol u waarvoor u wilt dat externe toegang tooenable

   * Klik op tooselect hello **extern bureaublad inschakelen** selectievakje
   
   * Geef een gebruikersnaam en wachtwoord die u wilt dat toouse voor externe toegang
   
   * Hallo certificaat toouse selecteren

6. Klik op **OK** 

U ziet een bericht weergegeven dat de wijziging in de configuratie is gemaakt, maar dit kan enkele minuten toocomplete. Nadat de configuratiewijziging Hallo is voltooid, volgt u de stappen Hallo in Hallo **toolog in op afstand** verderop in dit artikel.

## <a name="how-tooenable-remote-access-in-your-package"></a>Hoe tooenable externe toegang in het pakket
1. Binnen de Eclipse-Project Explorer deelvenster met de rechtermuisknop op uw Azure-project en klik op **eigenschappen**.

2. In Hallo **eigenschappen** dialoogvenster Vouw **Azure** in het linkerdeelvenster Hallo en klik op **RAS**.

3. In Hallo **RAS** dialoogvenster, zorg ervoor dat **inschakelen van alle rollen tooaccept extern bureaublad-verbindingen met deze aanmeldingsreferenties** is ingeschakeld.

4. Geef een gebruikersnaam voor verbinding met extern bureaublad Hallo.

5. Geef en Bevestig het wachtwoord voor gebruiker Hallo Hallo. Hallo waarden gebruikersnaam en het wachtwoord instellen in dit dialoogvenster wordt gebruikt wanneer u een extern bureaublad-verbinding maakt. (Houd er rekening mee dat dit een afzonderlijk wachtwoord van het PFX-wachtwoord is.)

6. Hallo verloopdatum voor Hallo gebruikersaccount opgeven.

7. Klik op **nieuw** toocreate een nieuw zelfondertekend certificaat. (U kunt ook kunt u een certificaat selecteren van uw systeem werkruimte of het bestand via Hallo **werkruimte** of **bestandssysteem** respectievelijk, maar voor deze zelfstudie we een nieuwe maken knoppen certificaat.)

   * In Hallo **nieuw certificaat** dialoogvenster Geef en Bevestig Hallo wachtwoord dat u hebt gebruikt voor het PFX-bestand.

   * Hallo-waarde opgegeven voor het accepteren **naam (CN)**, of gebruik een aangepaste naam.

   * Hallo pad en de naam aangegeven waarin Hallo nieuw certificaat in cer-vorm moet worden opgeslagen. Voor deze stap en de volgende stap hello, kunt u Hallo **cert** map van uw Azure-project, maar u bent gratis toochoose een andere locatie. Voor deze zelfstudie gebruiken we **c:\mycert\mycert.cer**. (Hallo maken **c:\mycert** map voorafgaande tooproceeding of gebruik een bestaande map, indien gewenst.)

   * Hallo pad en de naam aangegeven waarin Hallo nieuw certificaat en de persoonlijke sleutel, PFX-indeling moeten worden opgeslagen. Voor deze zelfstudie gebruiken we **c:\mycert\mycert.pfx**. Uw **nieuw certificaat** dialoogvenster ziet er vergelijkbare toohello volgende (Hallo mappaden bijwerken als u niet gebruikt **c:\mycert**):
     
      ![][ic712275]

   * Klik op **OK** tooclose hello **nieuw certificaat** dialoogvenster.

8. Uw **RAS** dialoogvenster ziet er vergelijkbare toohello volgende:</p>
   
   ![][ic719495]

9. Klik op **OK** tooclose hello **RAS** dialoogvenster.

Uw toepassing opnieuw bouwt, hello set voor implementatie toocloud samenstellen.

## <a name="toolog-in-remotely"></a>toolog in op afstand
Zodra uw rolinstantie gereed is, kunt u extern aanmelden toohello virtuele machine die als host voor uw toepassing fungeert.

* Als Eclipse op Windows en geselecteerde Hallo **Start extern bureaublad op implementeren** optie tijdens uw tooAzure implementatie u krijgt een verbinding met extern bureaublad-aanmeldingsscherm wanneer uw implementatie wordt gestart. Wanneer u wordt gevraagd om het Hallo-gebruikersnaam en wachtwoord, Voer Hallo-waarden die u hebt opgegeven voor de externe gebruiker Hallo en kunnen toolog in.

* Een andere manier toolog in op afstand is via Hallo <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:
  
  * Binnen Hallo **Cloudservices** weergave van hello Azure Management portal op uw cloudservice, klik op **exemplaren**, klikt u op een specifiek exemplaar en klik vervolgens op Hallo **Connect**knop. Hallo **Connect** knop wordt weergegeven als in de opdrachtbalk Hallo Hallo volgende:
    
      ![][ic659273]

  * Wanneer u op Hallo **Connect** knop, kunt u zich na vragen aan gebruiker tooopen een RDP-bestand. Hallo-bestand openen en volg de aanwijzingen Hallo. (U kan ook Sla dit bestand tooyour lokale computer, en Voer Hallo-bestand door erop te dubbelklikken tooremote log in tooyour virtuele machine zonder toofirst Hallo-beheerportal gaat.)

  * Wanneer u wordt gevraagd om het Hallo-gebruikersnaam en wachtwoord, Voer Hallo-waarden die u hebt opgegeven voor de externe gebruiker Hallo en kunnen toolog in.

> [!NOTE]
> Als u op een niet-Windows-besturingssysteem, u moet een extern bureaublad-client die compatibel is met uw besturingssysteem toouse en volg Hallo stappen tooconfigure dat de client met Hallo-instellingen in Hallo RDP-bestand dat u hebt gedownload.
> 
> 

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse] 

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
