---
title: aaaWhat is Azure RemoteApp? | Microsoft Docs
description: Meer informatie over hoe tooshare apps en resources tooany apparaat via Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>Wat is Azure RemoteApp?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp introduceert Hallo-functionaliteit van Hallo lokale Microsoft RemoteApp-programma, gesteund door extern bureaublad-Services tooAzure. Azure RemoteApp kunt u tooapplications uit een groot aantal verschillende Gebruikersapparaten veilige externe toegang te bieden. Azure RemoteApp verzorgt in feite niet-permanente Terminal Server-sessies in de cloud Hallo en u beschikt over toouse ze en ze delen met uw gebruikers.

Met Azure RemoteApp kunt u apps en resources delen met gebruikers op vrijwel elk apparaat. We host uw apps in de cloud hello, wat betekent dat wij zorg dragen Hallo hardware en vereisten van de gebruikers toomeet schalen. Hoeft u deze toodo is Hallo apps u wilt tooshare en vervolgens uw toouse gebruikers deze apps uploadt. [Gebruikers krijgen tookeep hun eigen apparaten](remoteapp-clients.md), terwijl u alles via hello Azure-portal beheert. Ook hebt u Hallo optie van het gebruik van de referenties van uw bedrijf, zodat u Hallo beveiligen van apps en gegevens.

Lees verder voor meer informatie over Azure RemoteApp of [probeer het nu uit](https://azure.microsoft.com/services/remoteapp/) als we u al hebben overtuigd.

Hebt u vragen over Azure RemoteApp? Bekijk onze [veelgestelde vragen](remoteapp-faq.md).

Azure RemoteApp maakt deel uit van Hallo [Microsoft Virtual Desktop Infrastructure](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**Nieuw!** Wilt u meer informatie over Azure RemoteApp toolearn? Of toovalidate Azure RemoteApp op schaal gereed? Deelnemen aan ons wekelijks [vraag Hallo experts webinar](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Azure RemoteApp-verzamelingen
Er zijn twee soorten [Azure RemoteApp verzamelingen](remoteapp-collections.md):

* Een **cloudverzameling** wordt gehost en slaat gegevens voor programma's in de cloud Hallo. Gebruikers hebben toegang tot apps door zich aan te melden met hun Microsoft-account- of bedrijfsreferenties die zijn gesynchroniseerd of verenigd met Azure Active Directory.
  
    Kies een cloudverzameling als gewenste tooshare Hallo-toepassing een verbindingsbron tooany geen vereist particuliere netwerk van uw bedrijf (bijvoorbeeld via een VPN-apparaat). Een cloudverzameling werkt voor u als Hallo toepassing resources op Internet, Hallo OneDrive of Azure gebruikt. Het is ook de snelste toocreate Hallo.
* Een **hybride verzameling** wordt gehost in en slaat gegevens op in hello Azure-cloud, maar ook kiest, kunnen gebruikers toegang tot gegevens en resources die zijn opgeslagen op uw lokale netwerk. Gebruikers hebben toegang tot apps door zich aan te melden met hun bedrijfsreferenties die zijn gesynchroniseerd of verenigd met Azure Active Directory.
  
    Kies een hybride verzameling als u een verbinding tooresources in het particuliere netwerk van uw bedrijf vereist. Bijvoorbeeld, als hello toepassing moet toegang tot tooone van Hallo volgende:
  
  * Bestandsservers op het intranet
  * Quicken
  * Databases achter een firewall
    
    Dit is doorgaans nuttiger voor grote bedrijven met veel resources in hun particuliere netwerken die niet kunnen worden verplaatst toohello cloud.

Hallo verschillende verzamelingen hebben verschillende opties, waaronder netwerken, zoek daarom uit [welke verzameling](remoteapp-collections.md) meest geschikt is voor u. 

### <a name="updating-your-collection"></a>Een verzameling bijwerken
Een van de belangrijke verschillen tussen Hallo hybride en cloud verzamelingen Hallo is hoe software-updates worden verwerkt. Met een cloudverzameling die gebruikmaakt van Hallo vooraf geïnstalleerde Office 365 ProPlus of Office 2013-installatiekopie, hoeft u geen tooworry over updates. Hallo service onderhoudt zichzelf en de updates op voortdurend, tooboth apps en het Hallo-besturingssysteem.

Voor hybride verzamelingen, evenals cloudverzamelingen die gebruikmaken van de installatiekopie van een aangepaste sjabloon, bent u verantwoordelijk onderhouden Hallo installatiekopie en apps. Voor installatiekopieën die lid zijn van een domein kunt u updates beheren met hulpprogramma's als Windows Update, Groepsbeleid of System Center.

Nadat u de installatiekopie van uw aangepaste sjabloon hebt bijgewerkt, kunt u uploaden Hallo nieuwe installatiekopie toohello Azure-cloud en werk vervolgens Hallo verzameling toouse Hallo nieuwe installatiekopie. (U kunt dit doen vanuit hello Azure RemoteApp **Quick Start** pagina of Dashboard Hallo.)

Zie [Een verzameling bijwerken](remoteapp-update.md) voor meer informatie.

## <a name="supported-remoteapp-clients"></a>Ondersteunde RemoteApp-clients
Azure RemoteApp wordt ondersteund op Hallo RemoteApp-client-apps voor Windows en Windows RT, evenals Hallo Microsoft Extern bureaublad-apps voor Mac, iOS en Android. Uw gebruikers kunnen deze apps op hun mobiele apparaat gebruiken of compute apparaten tooaccess Hallo nieuwe Azure RemoteApp-programma's.

Zie [uw apps openen in Azure RemoteApp](remoteapp-clients.md) voor meer informatie over het Hallo-clients.

## <a name="next-steps"></a>Volgende stappen
Aan de slag Probeer het nu! Deze artikelen helpen u op weg met Azure RemoteApp:

* [Wat voor verzameling hebt u nodig voor Azure RemoteApp?](remoteapp-collections.md)
* [Een installatiekopie maken voor Azure RemoteApp](remoteapp-imageoptions.md)
* [Hoe toocreate een cloudverzameling van Azure RemoteApp](remoteapp-create-cloud-deployment.md)
* [Hoe toocreate een hybride verzameling van Azure RemoteApp](remoteapp-create-hybrid-deployment.md)
* [Hoe werkt licentieverlening in Azure RemoteApp?](remoteapp-licensing.md)
* [Aanbevolen procedures voor het gebruik van Azure RemoteApp](remoteapp-bestpractices.md)
* [Veelgestelde vragen over Azure RemoteApp](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Help ons u te helpen
Wist u dat in de toevoeging toorating in dit artikel en het toevoegen van opmerkingen omlaag hieronder, kunt u wijzigingen toohello artikel zelf? Ontbreekt er iets? Is er iets niet juist? Heb ik iets geschreven dat niet duidelijk is? Blader omhoog en klik op **Edit on GitHub** of **bewerken** toomake wijzigingen - deze worden eerst nagekeken toous, en vervolgens wanneer uitgeschakeld op deze, ziet u uw wijzigingen en verbeteringen hier.

