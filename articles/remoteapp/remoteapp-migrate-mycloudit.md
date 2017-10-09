---
title: aaaChange hello facturering voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toostop wordt gefactureerd voor Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Migreren van Azure RemoteApp tooMyCloudIT 

**Momenteel gebruikt u Microsoft Azure RemoteApp?** : MyCloudIT gebouwd een geautomatiseerde hulpprogramma toomigrate uw Azure RemoteApp (ARA) verzameling(en) toohello MyCloudIT beheerplatform terwijl u toorun op Microsoft Azure.

**Profiteren van Azure Resource Manager-portal Hallo**: voltooide migratie in Hallo MyCloudIT platform kunt direct toegang tooAzure van nieuwe Azure Resource Manager-portal. Deze portal bevat alle Hallo nieuwe mogelijkheden en innovaties die worden aangeboden door Microsoft Azure, met inbegrip van toegang tooVirtual Machine grootten tooensure uw implementatie is ingebouwd toosupport Hallo behoeften van uw bedrijf.

**Testen in parallelle tooensure Hallo juiste oplossing voor uw behoeften**: hulpprogramma voor migratie van Hallo MyCloudIT tooinitiate Hallo-migratieproces en testen in parallelle tijdens de huidige ARA-gebruikers blijven toouse ARA is gebouwd.  Uw gebruikers in ARA blijft totdat de migratie en tests zijn voltooid.  hulpprogramma voor migratie van Hallo is gebouwd toohandle Hallo typische ARA-verzameling.  Als u denkt dat u hebt een unieke, niet-standaard-scenario, neem contact op met ons op [ sales@conexlink.com ](mailto:sales@conexlink.com) zodat we een plan op maat gemaakte tooassist in uw migratie voorzien kunnen.

**Bureaublad as a Service mogelijkheden**: Houd er rekening mee dat MyCloudIT biedt niet alleen Hallo RemoteApp-mogelijkheden u gewend bent voor, maar wij ook volledige Desktop-As-A-Service bieden mogelijkheden voor Hallo dezelfde kosten per maand zonder een minimale gebruiker vereisten.

## <a name="what-we-will-do-for-you"></a>Wat wordt gedaan voor u

MyCloudIT automatiseert het Hallo-migratie van uw Azure RemoteApp-sjabloon uit de klassieke Azure-portal Hallo van uw abonnement toohello Azure Resource Manager-Portal van uw abonnement met onze geautomatiseerde Migratiehulpmiddel.  

> [!NOTE]
> Hello Azure RemoteApp-sjabloon in moet blijven Hallo dezelfde Azure-regio als uw oorspronkelijke implementatie van Azure RemoteApp.  Als u tijdens de migratie Hallo toochange Azure-regio's of Azure-abonnementen nodig hebt, neem contact met ons voor aanvullende informatie op [ sales@conexlink.com ](mailto:sales@conexlink.com).

Lees de onderstaande voor gedetailleerde informatie over het migratieproces Hallo geautomatiseerde Hello MyCloudIT-hulpprogramma voor migratie:

1. hulpprogramma voor migratie van Hallo scant uw huidige abonnement(en) voor alle bestaande ARA-implementaties.  
2. Selecteer één ARA verzameling toomigrate tegelijk.  Als er meerdere verzamelingen, meerdere keren uitvoeren onze tool.
3. U hebt Hallo optie toocopy Hallo gebruiker profiel schijven (UDP) tooyour nieuwe implementatie daarom kunt u verouderde gegevens worden opgehaald, of uw nieuwe implementatie van UPDs toohello handmatig toewijzen. Als u op uw UPDs toocopy kiest, wordt Hallo UPDs opslaan en een tekstbestand dat Hallo UPD naam tooeach gebruikers naam wijst bevatten.  Hallo UPDs worden gekopieerde tooa-share op Hallo RDSMGMT server `F:\Shares\LegacyUPD` en zal worden weergegeven via Hallo share `\\RDSmgmt\LegacyUPD`. 
4. De migratie moeten er geen uitvaltijd voor uw huidige ARA-implementatie.  Maar als er wijzigingen toohello UPDs (van ARA) na Hallo kopiëren aangebracht zijn, deze wijzigingen, niet worden weergegeven in Hallo UPDs opgeslagen in hello Azure Resource Manager-portal. 
5. Als u extra virtuele machines zoals domeincontrollers hebt en bestandsservers in de klassieke Azure Virtual Network we tot stand brengen tussen uw bestaande klassieke Azure Virtual Network-peering VNet en hello nieuw virtueel netwerk we voor u maken, in Hallo nieuwe Azure Resource Manager-Portal.
6. Onze geautomatiseerde oplossing wordt alleen VNet-peering tussen uw bestaande klassieke Azure Virtual Network tot stand brengen en Hallo nieuw virtueel netwerk als de implementatie van uw bestaande ARA een hybride implementatie; wat betekent dat verifieert u met een Windows Server Active Directory-domeincontroller in Hallo bestaande klassiek virtueel netwerk. Als er geen tot stand VNet brengen-peering voor uw verzameling, maar u nodig VNet hebt-peering, neem contact met ons als [ sales@conexlink.com ](mailto:sales@conexlink.com) en wij zijn blij tooconfigure VNet-peering zonder extra kosten.
7. Onze geautomatiseerde oplossing zorgt voor de Azure DNS-configuratie is bijgewerkt met Hallo nieuw virtueel netwerk instellingen tooensure uw nieuwe implementatie tooyour bestaande domeincontroller in Hallo kunt aansluiten klassieke VNet.
8. Onze geautomatiseerde oplossing zorgt ervoor dat er geen IP-adresconflicten zijn als we deze nieuw virtueel netwerk maken en tot stand brengen Hallo VNet-peering voor implementaties met een bestaande Windows Server Active Directory-Server.
9. Als u Azure AD alleen voor verificatie gebruikt, wordt MyCloudIT een nieuwe Windows Server Active Directory-domein maken en gebruiken van Azure AD Connect toosynchronize gebruikers tussen Hallo bestaande Azure AD-exemplaar en Hallo die nieuwe Windows Server Active Directory-domein is gemaakt door MyCloudIT.
10. Als u van een Windows Server Active Directory-domein tooauthenticate ARA-gebruikers gebruikmaakt, verbinding onze geautomatiseerde oplossing uw nieuwe MyCloudIT implementatie tooyour bestaande Windows Server Active Directory-domeincontroller via de VNet-peering.
11. Als u van Azure Active Directory Domain Services voor verificatie gebruikmaakt, kunnen we u migreert, maar neem contact met ons zodat we kan voor u een aangepaste migratieplan maken.  Verzend een e-mailbericht te[sales@conexlink.com](mailto:sales@conexlink.com). 
12. Zodra Hallo verzameling toobe gemigreerd is bevestigd, terug zitten en versoepelen terwijl onze geautomatiseerde oplossing uw ARA verzameling en de Gebruikersprofielschijven (optioneel) toohello nieuwe externe Apps MyCloudIT gebaseerde oplossing migreert.
13. Zodra het Hallo-implementatie is voltooid, wordt er opnieuw publiceren dezelfde toepassingen die zijn gepubliceerd in ARA Hallo en na de implementatie kunt u zich kunt toopublish aanvullende toepassingen.

## <a name="post-migration-benefits"></a>Na de migratie voordelen

1. We bieden Hallo-beheerconsole waarmee u toomanage Hallo volledige levenscyclus van uw implementatie van externe Apps.
2. U zult kunnen toomanage uw virtuele Machines van onze portal.  Starten / stoppen en grootte van afzonderlijke virtuele machines, indien nodig.
3. Hallo-beheerconsole biedt een mogelijkheid toocreate Hallo en beheren van gebruikers / groepen vanuit de beheerportal.
4. Hallo-beheerconsole biedt Hallo mogelijkheid toosynchronize gebruikers met Office 365 toocreate dezelfde ervaring eenmalige aanmelding.
5. Hallo-beheerconsole biedt een Hallo mogelijkheid toocreate aanvullende externe App- en bureaublad verzamelingen zonder kosten dubbele gebruiker of minimale gebruikersvereisten. 
6. Hallo-beheerconsole biedt de mogelijkheid Hallo toopublish nieuwe externe Apps toepassingen.
7. Hallo-beheerconsole biedt Hallo mogelijkheid tooschedule Hallo opstarten en afsluiten van uw implementatie van externe Apps als u alleen uw oplossing specifieke kantooruren moet.
8. Hallo-beheerconsole biedt Hallo mogelijkheid tooautomate Hallo installatie en configuratie van hello Azure backup-agent die de geschiedenis van een document bewaren voor uw gegevens van de klant biedt.
9. Hallo-beheerconsole biedt toegang tot tooperformance metrische gegevens van uw implementatie.  Dit biedt u Hallo mogelijkheid tooidentify alle potentiële knelpunten zonder aanvullende prestatie beheerprogramma's te installeren.
10. Als u meerdere sessie-hosts hebt, kunt u zich kunt tooenable automatisch schalen kunnen slechts Hallo sessie hosts die toobe uitgevoerd moeten worden uitgevoerd.
11. MyCloudIT biedt toegang tot toohello RDWeb gateway-server via een domeinnaam MyCloudIT.  We bieden ook Hallo mogelijkheid toore kaart Hallo URL tooa aangepaste URL op voor de huisstijl van de eindgebruiker.

## <a name="prerequisites-for-migration"></a>Vereisten voor migratie

1. U moet toegang toohello Azure-abonnement dat als host fungeert voor uw huidige oplossing met Azure RemoteApp hebben.
2. U moet machtigingen onze portal binnen uw abonnement toomigrate uw sjabloon en toocreate / wijzigen van uw nieuwe MyCloudIT-implementatie.
3. Houd er rekening mee dat vanwege tooa beperking in Azure RemoteApp, elke verzameling kan alleen worden gemigreerd drie keer.  Als u een verzameling toomigrate meer dan drie keer moet, kunt u een ticket tooAzure tooincrease verhoogt het aantal exporteren, of neem contact met ons en we helpt bij het Hallo ARA aanvraag tooincrease Hallo export count.

## <a name="mycloudit-billing"></a>MyCloudIT facturering

Zie [MyCloudIT prijzen voor RemoteApp-oplossingen](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) voor meer informatie over toopredict en beheren van uw algehele Azure kosten.

Als u nog steeds vragen hebt, neem contact op met ons op [ sales@conexlink.com ](mailto:sales@conexlink.com) of bekijkt hello volledige demovideo [Migratiehulpmiddel voor Azure RemoteApp - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

