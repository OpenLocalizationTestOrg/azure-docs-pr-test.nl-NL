---
title: aaaHigh beschikbaarheid cross-geografische AD FS-implementatie in Azure met Azure Traffic Manager | Microsoft Docs
description: In dit document wordt uitgelegd hoe toodeploy AD FS in Azure voor hoge beschikbaarheid.
keywords: AD fs met Azure traffic manager, AD FS met Azure Traffic Manager, geografische, multi datacenter, geografische datacenters, meerdere geografische datacenters, AD FS implementeren in azure, azure AD FS, azure AD FS, azure ad fs implementeren, AD FS implementeren, ad fs, AD FS in azure implementeren AD FS implementeren in azure, AD FS implementeren in azure, azure AD FS, inleiding tooAD FS, Azure, AD FS in Azure, iaas, ADFS, adfs tooazure verplaatsen
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>AD FS-implementaties in meerdere regio’s in Azure, met maximale beschikbaarheid dankzij Azure Traffic Manager
[AD FS-implementatie in Azure](active-directory-aadconnect-azure-adfs.md) biedt stapsgewijze richtlijnen als toohow kunt u een eenvoudige AD FS-infrastructuur implementeren voor uw organisatie in Azure. Dit artikel bevat de volgende stappen Hallo toocreate een geografische cross-implementatie van AD FS in Azure met behulp [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). Azure Traffic Manager helpt een geografisch verspreid hoge beschikbaarheid en hoge prestaties AD FS-infrastructuur voor uw organisatie doordat maken gebruik van het bereik van methoden beschikbaar toosuit verschillende in Hallo-infrastructuur behoeften.

Met een maximaal beschikbare AD FS-infrastructuur in meerdere regio’s kunt u:

* **Afschaffing van storingspunt:** met failover-mogelijkheden van Azure Traffic Manager, kunt u een maximaal beschikbare AD FS-infrastructuur bereiken, zelfs wanneer een van Hallo-datacenters in een gedeelte van de hele wereld Hallo uitvalt
* **Verbeterde prestaties:** kunt u Hallo voorstel voor de implementatie in dit artikel tooprovide een krachtige AD FS-infrastructuur die kan helpen bij gebruikers sneller te verifiëren. 

## <a name="design-principles"></a>Ontwerpprincipes
![Algemeen ontwerp](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

Hallo basic principes wordt niet hetzelfde zijn als die worden vermeld in de ontwerp-beginselen in Hallo artikel AD FS-implementatie in Azure. Hallo bovenstaande diagram ziet u een eenvoudige uitbreiding van Hallo basisimplementatie tooanother geografische regio. Hieronder vindt u enkele tooconsider punten bij het uitbreiden van uw implementatie toonew geografische regio

* **Virtueel netwerk:** moet u een nieuw virtueel netwerk maken in de geografische regio Hallo gewenste toodeploy extra AD FS-infrastructuur. In bovenstaande Hallo diagram ziet u Geo1 VNET en Geo2 VNET als Hallo twee virtuele netwerken in elke geografische regio.
* **Domeincontrollers en AD FS-servers in de nieuwe geografische VNET:** verdient toodeploy domeincontrollers in nieuw geografische regio Hallo zodat Hallo AD FS-servers in de nieuwe regio Hallo geen toocontact een domeincontroller in een andere ver opslag netwerk toocomplete verificatie en waardoor betere Hallo prestaties.
* **Opslagaccounts:** opslagaccounts worden gekoppeld aan een regio. Omdat u computers in een nieuw geografisch gebied implementeren wilt, hebt u toocreate nieuwe opslagaccounts toobe in Hallo regio gebruikt.  
* **Netwerkbeveiligingsgroepen:** net als opslagaccounts kunnen netwerkbeveiligingsgroepen die in een bepaalde regio zijn gemaakt, niet in een andere geografische regio worden gebruikt. Daarom moet u toocreate nieuwe netwerk beveiliging groepen vergelijkbare toothose in Hallo eerste geografische regio voor INT en DMZ subnet in Hallo nieuwe geografische regio.
* **DNS-Labels voor openbare IP-adressen:** Azure Traffic Manager kunt verwijzen tooendpoints alleen via DNS-labels. Daarom bent u vereiste toocreate DNS-labels voor Hallo externe Load Balancers de openbare IP-adressen.
* **Azure Traffic Manager:** Microsoft Azure Traffic Manager kunt u toocontrol Hallo distributie van de gebruiker verkeer tooyour service eindpunten in verschillende datacenters Hallo wereld. Azure Traffic Manager werkt op Hallo DNS-niveau. DNS-antwoorden toodirect eindgebruiker verkeer tooglobally gedistribueerd eindpunten wordt gebruikt. Clients vervolgens rechtstreeks verbinding gemaakt toothose eindpunten. Met verschillende routering opties van prestaties, gewogen en prioriteit, kunt u eenvoudig hello routingoptie het meest geschikt voor de behoeften van uw organisatie te kiezen. 
* **V net tooV-net connectiviteit tussen twee regio's:** hoeft u geen toohave connectiviteit tussen virtuele netwerken Hallo zelf. Omdat elke virtueel netwerk toegang tot toodomain domeincontrollers heeft en AD FS en WAP-server zelf is, kunnen ze werken zonder een verbinding tussen virtuele netwerken Hallo in verschillende regio's. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Stappen toointegrate Azure Traffic Manager
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>AD FS implementeren in de nieuwe geografische regio Hallo
Ga als volgt Hallo stappen en richtlijnen in [AD FS-implementatie in Azure](active-directory-aadconnect-azure-adfs.md) toodeploy Hallo dezelfde topologie in Hallo nieuwe geografische regio.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>DNS-labels voor openbare IP-adressen (openbare) Load Balancers Internet Facing Hallo
Zoals eerder vermeld, hello Azure Traffic Manager tooDNS labels als eindpunten kan alleen verwijzen en daarom is het belangrijk toocreate DNS-labels voor Hallo externe Load Balancers de openbare IP-adressen. Onderstaande schermafbeelding ziet u hoe u uw DNS-label voor het openbare IP-adres Hallo kunt configureren. 

![DNS-label](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Azure Traffic Manager implementeren
Hallo stappen hieronder toocreate een traffic manager-profiel. Voor meer informatie vindt u ook te[een Azure Traffic Manager-profiel beheren](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Een Traffic Manager-profiel maken:** geef uw Traffic Manager-profiel een unieke naam. Deze naam van profiel Hallo maakt deel uit van Hallo DNS-naam en fungeert als een voorvoegsel voor Hallo Traffic Manager-domeinnaamlabel. de naam van de Hallo voorvoegsel too.trafficmanager.net toocreate een DNS-label voor uw traffic manager wordt toegevoegd. Hallo onderstaande schermafbeelding ziet u DNS-voorvoegsel wordt ingesteld zoals mysts en de resulterende DNS-label mysts.trafficmanager.net worden Hallo traffic manager. 
   
    ![Een Traffic Manager-profiel maken](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Routeringsmethode voor verkeer:** er zijn drie routeringsopties beschikbaar in Traffic Manager:
   
   * Prioriteit 
   * Prestaties
   * Gewogen
     
     **Prestaties** hello wordt aanbevolen optie tooachieve uiterst responsieve AD FS-infrastructuur. U kunt echter kiezen voor de routeringsmethode die het beste aansluit op uw implementatiebehoeften. Hallo AD FS-functionaliteit wordt niet beïnvloed door Hallo routering optie is geselecteerd. Zie [Verkeersrouteringsmethoden voor Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md) voor meer informatie. Schermafdruk voorbeeld hierboven u ziet in Hallo Hallo **prestaties** methode geselecteerd.
3. **Eindpunten configureren:** Hallo traffic manager pagina eindpunten op en selecteer toevoegen. Hiermee opent u een Add-eindpunt pagina vergelijkbaar toohello onderstaande schermafbeelding
   
   ![Eindpunten configureren](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Voor andere invoer hello, voert u Hallo richtlijn hieronder:
   
   **Type:** Azure-eindpunt als we tooan Azure openbaar IP-adres verwijzen selecteert.
   
   **Naam:** maken een naam die u tooassociate met Hallo-eindpunt wilt. Dit is geen Hallo DNS-naam en heeft geen gevolgen voor DNS-records.
   
   **Resource doeltype:** Selecteer de openbare IP-adres als Hallo waarde toothis eigenschap. 
   
   **Doelresource:** Hiermee krijgt u een optie toochoose van Hallo andere DNS-labels er beschikbaar zijn in uw abonnement. Kies Hallo die DNS-label bijbehorende toohello eindpunt dat u configureert.
   
   Eindpunt voor elke geografische regio die u wilt dat hello Azure Traffic Manager tooroute verkeer naar toevoegen.
   Voor meer informatie en gedetailleerde stapsgewijze instructies voor het tooadd / -eindpunten configureren in het traffic manager, raadpleeg dan te[eindpunten toevoegen, uitschakelen, inschakelen of verwijderen](../traffic-manager/traffic-manager-endpoints.md)
4. **Test configureren:** Hallo traffic manager-pagina, klik op configuratie. In de configuratiepagina hello moet u de toochange Hallo monitor instellingen tooprobe op HTTP-poort 80 en relatief pad /adfs/probe
   
    ![Test configureren](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Zorg ervoor dat Hallo status van Hallo eindpunten ONLINE wanneer het Hallo-configuratie is voltooid**. Als alle eindpunten 'verslechterde' status, doet Azure Traffic Manager een beste poging tooroute Hallo-verkeer ervan uitgaande dat Hallo diagnostische gegevens is onjuist en alle eindpunten bereikbaar zijn.
   > 
   > 
5. **Wijzigen van DNS-records voor Azure Traffic Manager:** uw federation-service moet een CNAME-toohello Azure Traffic Manager-DNS-naam. Maak een CNAME in Hallo openbare DNS-records zodat degene die tooreach Hallo federation-service probeert daadwerkelijk hello Azure Traffic Manager is bereikt.
   
    Bijvoorbeeld, toopoint Hallo federation service fs.fabidentity.com toohello Traffic Manager, moet u tooupdate uw DNS-resource record toobe hello te volgen:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Hallo Routering en AD FS-aanmeldingspagina testen
### <a name="routing-test"></a>Routeringstest
Een zeer eenvoudige test voor het doorsturen van Hallo zou worden tootry ping Hallo DNS-naam van federation service vanaf een computer in elke geografische regio. Afhankelijk van het Hallo-routeringsmethode gekozen, worden, deze daadwerkelijk pingt Hallo-eindpunt weergegeven in Hallo ping weergeven. Bijvoorbeeld als u de prestaties Hallo geselecteerd wordt routering vervolgens Hallo eindpunt dichtstbijzijnde toohello gebied van Hallo-client bereikt. Hieronder ziet u Hallo momentopname van de twee pings van twee andere regio-clientcomputers, één in Oost-Aziatische regio en één in VS-West. 

![Routeringstest](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>AD FS-aanmeldingstest
Hallo gemakkelijkste manier tootest AD FS is met behulp van Hallo IdpInitiatedSignon.aspx pagina. Hallo in volgorde toobe kunnen toodo dat vereist tooenable is IdpInitiatedSignOn op Hallo AD FS-eigenschappen. Volg onderstaande tooverify Hallo stappen uw AD FS-installatie

1. Voer wordt Hallo hieronder cmdlet op Hallo AD FS-server, met behulp van PowerShell, tooset tooenabled is ingesteld. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Ga vanaf een externe computer naar https://<yourfederationservicedns>adfs/ls/IdpInitiatedSignon.aspx
3. U ziet Hallo AD FS-pagina, zoals hieronder:
   
    ![AD FS-test - verificatievraag](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    Bij een geslaagde aanmelding wordt een soortgelijk positief bericht weergegeven:
   
    ![AD FS-test - verificatie geslaagd](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Verwante koppelingen
* [AD FS-implementatie in Azure](active-directory-aadconnect-azure-adfs.md)
* [Microsoft Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)
* [Traffic Manager traffic routing methods](../traffic-manager/traffic-manager-routing-methods.md) (Verkeersrouteringsmethoden van Traffic Manager)

## <a name="next-steps"></a>Volgende stappen
* [Azure Traffic Manager-profielen beheren](../traffic-manager/traffic-manager-manage-profiles.md)
* [Eindpunten toevoegen, uitschakelen, inschakelen of verwijderen](../traffic-manager/traffic-manager-endpoints.md) 

