---
title: Externe toegang inschakelen voor Azure-implementaties in Eclipse
description: Informatie over het inschakelen van externe toegang voor Azure met de Azure-Toolkit voor Eclipse-implementaties.
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
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Externe toegang inschakelen voor Azure-implementaties in Eclipse
U kunt voor het oplossen van uw implementaties, inschakelen en gebruiken van externe toegang verbinding maken met de virtuele machine die als host fungeert voor uw implementatie. De functionaliteit voor externe toegang is afhankelijk van de Remote Desktop Protocol (RDP). Nadat u deze hebt gepubliceerd naar Azure, of als u Eclipse met een Windows-besturingssysteem gebruikt, u externe toegang configureren kunt voordat u naar Azure publiceert, kunt u externe toegang configureert voor uw implementatie. Houd er rekening mee dat u een extern-bureaubladclient die compatibel is met het besturingssysteem moet om verbinding met uw implementatie virtuele machine in Azure.

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a>Het inschakelen van externe toegang, voordat u naar Azure implementeert
> [!NOTE]
> Om externe toegang inschakelen voordat u uw toepassing in Azure implementeert, moet u Eclipse worden uitgevoerd op Windows.
> 
> 

De volgende afbeelding toont de **RAS** eigenschappenvenster gebruikt om externe toegang.

![][ic719494]

Er zijn twee manieren om weer te geven de **RAS** dialoogvenster met eigenschappen:

* Klik op de **Geavanceerd** koppelen de **RAS** sectie van de **publiceren naar Azure** dialoogvenster.

* Open de **eigenschappen** dialoogvenster van uw Azure-project.

Wanneer u een nieuw project in de Azure-implementatie maakt, is het project heeft geen externe toegang is standaard ingeschakeld. Echter, kunt u eenvoudig externe toegang inschakelen door te geven van de gebruikersnaam en wachtwoord in de **publiceren naar Azure** dialoogvenster. De RAS-wachtwoord is versleuteld met behulp van x.509-certificaten. Als u geen gebruik geeft u uw eigen certificaat de versleuteling is afhankelijk van een zelfondertekend certificaat met de Azure-invoegtoepassing voor Eclipse verzonden. Dit zelfondertekende certificaat bevindt zich in de **cert** map van uw Azure-project opgeslagen als een openbaar certificaat-bestand (SampleRemoteAccessPublic.cer) en als een certificaatbestand Personal Information Exchange (PFX) (SampleRemoteAccessPrivate.pfx). De laatste bevat de persoonlijke sleutel voor het certificaat en heeft deze een standaardwachtwoord **Wachtwoord1**. Echter, omdat dit wachtwoord algemeen bekend is, kan de standaardcertificaat moet worden gebruikt alleen voor het leren van de toepassing wordt niet voor een productie-implementatie. Dus anders dan voor het leren van toepassing wanneer u wilt ingeschakeld externe sessies voor uw implementaties, klikt u de **Geavanceerd** koppelen de **publiceren naar Azure** dialoogvenster om uw eigen certificaat te geven. Houd er rekening mee dat u uploaden van het PFX-versie van het certificaat naar de gehoste service in de Azure-beheerportal wilt, zodat die Azure om het wachtwoord van de gebruiker te ontsleutelen.

De rest van de zelfstudie laat zien hoe u externe toegang inschakelt voor een Azure-implementatie-project die aanvankelijk is gemaakt met externe toegang uitgeschakeld. Voor deze zelfstudie maken we een nieuw zelfondertekend certificaat en het pfx-bestand heeft een wachtwoord van uw keuze. U hebt ook de optie van het gebruik van een certificaat zijn uitgegeven door een certificeringsinstantie.

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a>Het inschakelen van externe toegang nadat u hebt geïmplementeerd naar Azure
Voor externe toegang nadat u hebt geïmplementeerd naar Azure, gebruikt u de volgende stappen uit:

1. Meld u aan bij de Azure-beheerportal met behulp van uw Azure-account

2. In de lijst met **Cloudservices**, selecteer uw geïmplementeerde cloudservice

3. Klik in de cloud service-webpagina op de **configureren** koppeling

4. Klik op de onderkant van de pagina op de **externe** koppeling

5. Wanneer het pop-updialoogvenster wordt weergegeven:
   
   * Geef de rol waarvoor u wilt externe toegang inschakelen

   * Selecteer de **extern bureaublad inschakelen** selectievakje
   
   * Geef een gebruikersnaam en wachtwoord die u wilt gebruiken voor externe toegang
   
   * Selecteer het certificaat te gebruiken

6. Klik op **OK** 

U ziet een bericht weergegeven dat de wijziging in de configuratie is gemaakt, maar dit kan enkele minuten duren. Nadat de wijziging in de configuratie is voltooid, volg de stappen in de **extern aanmelden** verderop in dit artikel.

## <a name="how-to-enable-remote-access-in-your-package"></a>Het inschakelen van externe toegang in het pakket
1. Binnen de Eclipse-Project Explorer deelvenster met de rechtermuisknop op uw Azure-project en klik op **eigenschappen**.

2. In de **eigenschappen** dialoogvenster Vouw **Azure** in het linkerdeelvenster op **RAS**.

3. In de **RAS** dialoogvenster, zorg ervoor dat **alle rollen te accepteren van extern bureaublad-verbindingen met deze aanmeldingsreferenties inschakelen** is ingeschakeld.

4. Geef een naam op voor de extern bureaublad-verbinding.

5. Geef en Bevestig het wachtwoord voor de gebruiker. De waarden gebruikersnaam en het wachtwoord instellen in dit dialoogvenster wordt gebruikt wanneer u een extern bureaublad-verbinding maakt. (Houd er rekening mee dat dit een afzonderlijk wachtwoord van het PFX-wachtwoord is.)

6. De verloopdatum voor het gebruikersaccount opgeven.

7. Klik op **nieuw** een nieuw zelfondertekend certificaat maken. (U kunt ook een certificaat selecteren van uw systeem werkruimte of het bestand via de **werkruimte** of **bestandssysteem** knoppen, respectievelijk, maar voor de doeleinden van deze zelfstudie maken we een nieuw certificaat.)

   * In de **nieuw certificaat** dialoogvenster Geef en Bevestig het wachtwoord dat u voor het PFX-bestand gebruikt.

   * De opgegeven waarde voor accepteren **naam (CN)**, of gebruik een aangepaste naam.

   * Geef het pad en de naam waarin het nieuwe certificaat, in cer-vorm moet worden opgeslagen. Voor deze stap en de volgende stap, u kunt de **cert** map van uw Azure-project, maar u bent een andere locatie kiezen. Voor deze zelfstudie gebruiken we **c:\mycert\mycert.cer**. (Maken de **c:\mycert** map voordat u doorgaat, of gebruik een bestaande map, indien gewenst.)

   * Geef de naam van het pad en bestand waarin het nieuwe certificaat en de persoonlijke sleutel, PFX-indeling moeten worden opgeslagen. Voor deze zelfstudie gebruiken we **c:\mycert\mycert.pfx**. Uw **nieuw certificaat** dialoogvenster ziet er ongeveer als volgt (bijwerken van de paden voor mappen als u niet gebruikt **c:\mycert**):
     
      ![][ic712275]

   * Klik op **OK** sluiten de **nieuw certificaat** dialoogvenster.

8. Uw **RAS** dialoogvenster ziet er ongeveer als volgt:</p>
   
   ![][ic719495]

9. Klik op **OK** sluiten de **RAS** dialoogvenster.

Bouw uw toepassing opnieuw met de build instellen voor implementatie naar cloud.

## <a name="to-log-in-remotely"></a>Om aan te melden op afstand
Zodra uw rolinstantie gereed is, kunt u extern aanmelden bij de virtuele machine die als host voor uw toepassing fungeert.

* Als Eclipse op Windows en u hebt geselecteerd de **Start extern bureaublad op implementeren** optie tijdens de implementatie naar Azure, u krijgt een verbinding met extern bureaublad-aanmeldingsscherm wanneer uw implementatie wordt gestart. Wanneer u wordt gevraagd om de gebruikersnaam en wachtwoord, voer de waarden die u hebt opgegeven voor de externe gebruiker en zich aan te melden.

* Een andere manier om aan te melden op afstand is via de <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:
  
  * Binnen de **Cloudservices** weergeven van de Azure Management portal, klik op de cloudservice, **exemplaren**, klikt u op een specifiek exemplaar en klik op de **Connect** knop. De **Connect** knop wordt weergegeven als het volgende in de opdrachtbalk:
    
      ![][ic659273]

  * Wanneer u op de **Connect** knop, wordt u gevraagd om een RDP-bestand te openen. Open het bestand en volg de aanwijzingen. (U kan dit bestand ook opslaan op uw lokale computer en voer vervolgens het bestand door erop te dubbelklikken op extern aanmelden met uw virtuele machine zonder eerst de beheerportal gaat.)

  * Wanneer u wordt gevraagd om de gebruikersnaam en wachtwoord, voer de waarden die u hebt opgegeven voor de externe gebruiker en zich aan te melden.

> [!NOTE]
> Als u op een niet-Windows-besturingssysteem, moet u een extern bureaublad-client die compatibel is met het besturingssysteem gebruiken en volg de stappen voor het configureren van de client met de instellingen in het RDP-bestand dat u hebt gedownload.
> 
> 

## <a name="see-also"></a>Zie ook
[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]

[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse] 

Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
