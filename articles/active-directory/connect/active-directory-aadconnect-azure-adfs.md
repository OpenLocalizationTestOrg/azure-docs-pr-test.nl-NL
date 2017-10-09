---
title: aaaActive Directory Federation Services in Azure | Microsoft Docs
description: In dit document wordt uitgelegd hoe toodeploy AD FS in Azure voor hoge beschikbaarheid.
keywords: AD FS implementeren in azure, azure AD FS, azure AD FS, azure ad fs implementeren, AD FS implementeren, ad fs, AD FS in azure implementeren, AD FS in azure implementeert, AD FS implementeren in azure, azure AD FS, inleiding tooAD FS, Azure, AD FS in Azure, iaas, ADFS, adfs tooazure verplaatsen
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Active Directory Federation Services in Azure implementeren
AD FS biedt vereenvoudigde, beveiligde identiteitsfederatie en mogelijkheden voor eenmalige webaanmelding (SSO of Single Sign-on). Federatie met Azure AD of O365 kunnen gebruikers tooauthenticate met on-premises referenties en toegang tot alle bronnen in de cloud. Als gevolg hiervan wordt het belangrijker toohave een maximaal beschikbare AD FS-infrastructuur tooensure tooresources toegang tot zowel on-premises en in de cloud Hallo. AD FS implementeren in Azure kunt Hallo hoge beschikbaarheid vereist met minimale inspanningen bereiken.
De implementatie van AD FS in Azure heeft verschillende voordelen, waaronder de volgende:

* **Hoge beschikbaarheid** -Hallo macht van Beschikbaarheidssets van Azure, u ervoor zorgen voor een maximaal beschikbare infrastructuur.
* **Eenvoudig tooScale** – hogere prestaties nodig? Eenvoudig migreren toomore krachtige machines met een paar muisklikken in Azure
* **Cross-geografische redundantie** – met Azure Geo redundantie die u kunt erop vertrouwen dat uw infrastructuur maximaal beschikbaar is voor alle Hallo wereld
* **Eenvoudig tooManage** – met opties sterk vereenvoudigd beheer in Azure-portal, beheer van uw infrastructuur is zeer eenvoudig en probleemloos 

## <a name="design-principles"></a>Ontwerpprincipes
![Implementatie-ontwerp](./media/active-directory-aadconnect-azure-adfs/deployment.png)

Hallo bovenstaande diagram toont Hallo aanbevolen basistopologie toostart implementeren van uw AD FS-infrastructuur in Azure. Hallo principes achter Hallo verschillende onderdelen van Hallo topologie worden hieronder weergegeven:

* **DC-/ADFS-servers**: als u minder dan 1000 gebruikers hebt, kunt u gewoon de AD FS-rol op uw domeincontrollers installeren. Als u niet dat eventuele gevolgen van de prestaties op Hallo-domeincontrollers wilt of als u meer dan 1000 gebruikers hebt, vervolgens AD FS op afzonderlijke servers te implementeren.
* **WAP-Server** – is noodzakelijk toodeploy Web Application Proxy-servers, zodat gebruikers kunnen Hallo AD FS wanneer ze zich niet in het bedrijfsnetwerk Hallo ook bereiken.
* **DMZ**: Hallo Web Application Proxy-servers worden geplaatst in Hallo DMZ en alleen TCP/443 toegang tussen Hallo DMZ en Hallo interne subnet is toegestaan.
* **Load Balancers**: tooensure hoge beschikbaarheid van AD FS en Webtoepassingsproxy-servers, wordt u aangeraden een interne load balancer voor AD FS-servers en Azure Load Balancer voor Web Application Proxy-servers.
* **Beschikbaarheidssets**: tooprovide redundantie tooyour AD FS-implementatie, het is raadzaam dat u twee of meer virtuele machines in een Beschikbaarheidsset voor vergelijkbare werklasten te groeperen. Deze configuratie zorgt ervoor dat tijdens een geplande of onvoorziene onderhoudsgebeurtenis ten minste één virtuele machine beschikbaar is
* **Storage-Accounts**: het is raadzaam twee toohave storage-accounts. Met een account is één opslag kan leiden toocreation van een potentieel risico en kan leiden tot Hallo implementatie toobecome niet beschikbaar in een onwaarschijnlijke scenario waarbij Hallo opslagaccount uitvalt. Met twee opslagaccounts kan er één opslagaccount worden gekoppeld aan elke storingslijn.
* **Netwerkscheiding**: implementeer webtoepassingsproxyservers in een afzonderlijk DMZ-netwerk. U kunt één virtueel netwerk verdelen over twee subnetten en implementeer vervolgens Hallo Web Application Proxy Server (s) in een geïsoleerde-subnet. U kunt gewoon Hallo netwerk groep beveiligingsinstellingen configureren voor elk subnet en alleen-vereiste communicatie tussen de twee subnetten Hallo toestaan. Meer informatie vindt u hieronder per implementatiescenario

## <a name="steps-toodeploy-ad-fs-in-azure"></a>Stappen toodeploy AD FS in Azure
Hallo stappen in deze sectie Overzicht Hallo handleiding toodeploy Hallo hieronder genoemde afgebeeld AD FS-infrastructuur in Azure.

### <a name="1-deploying-hello-network"></a>1. Hallo netwerk implementeren
Zoals hierboven is beschreven, kunt u twee subnetten in één virtueel netwerk maken, maar ook twee volledig verschillende virtuele netwerken (VNets). Dit artikel gaat over de implementatie van één virtueel netwerk en de verdeling daarvan in twee subnetten. Dit is momenteel een eenvoudiger benadering als twee afzonderlijke VNets een VNet tooVNet gateway voor communicatie vereist.

**1.1 Virtueel netwerk maken**

![Virtueel netwerk maken](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

In hello Azure-portal, kunt Selecteer virtueel netwerk en u implementeren Hallo virtueel netwerk en een subnet onmiddellijk met één klik. INT-subnet wordt ook gedefinieerd en is nu gereed voor virtuele machines toobe toegevoegd.
de volgende stap Hallo tooadd is een ander subnet toohello netwerk, dat wil zeggen Hallo DMZ subnet. toocreate Hallo DMZ subnet, gewoon

* Selecteer nieuw gemaakte Hallo netwerk
* Selecteer in de eigenschappen van Hallo subnet
* In Hallo subnet Configuratiescherm klik op Hallo knop toevoegen
* Hallo subnet naam en adres ruimte informatie toocreate Hallo subnet bieden

![Subnet](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![Subnet-DMZ](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2. Hallo-netwerk maken van beveiligingsgroepen**

Een netwerkbeveiligingsgroep (NSG) bevat een lijst met regels voor lijst ACL (Access Control) toestaan of weigeren netwerkverkeer tooyour VM-exemplaren in een virtueel netwerk. NSG's kunnen worden gekoppeld aan subnetten of afzonderlijke VM-exemplaren in dat subnet. Wanneer een NSG gekoppeld aan een subnet is, toepassing hello ACL-regels tooall Hallo VM-exemplaren in dat subnet.
Voor Hallo doel van deze richtlijnen, maken we twee nsg's: één voor een intern netwerk en een DMZ genoemd. Ze worden respectievelijk NSG_INT en NSG_DMZ genoemd.

![NSG’s maken](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

Na het Hallo die NSG wordt gemaakt, zijn er 0 regels voor binnenkomende en 0 uitgaand. Als de Hallo-functies op Hallo respectieve servers zijn geïnstalleerd en functioneert, kunnen vervolgens hello regels voor binnenkomende en uitgaande worden gemaakt volgens toohello gewenst niveau van beveiliging.

![NSG’s initialiseren](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

Nadat Hallo nsg's zijn gemaakt, koppelen aan NSG_INT subnet INT en NSG_DMZ met subnet DMZ genoemd. Hieronder ziet u een schermafbeelding van het voorbeeld:

![NPS configureren](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* Klik op subnetten tooopen Hallo Configuratiescherm voor subnetten
* Hallo subnet tooassociate Hello NSG selecteren 

Hallo-deelvenster voor subnetten moet na configuratie eruitzien als hieronder:

![Subnetten na NSG](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3. Maken van verbinding tooon-premises**

Er moet een verbinding tooon-on-premises in volgorde toodeploy Hallo-domeincontroller (DC) in azure. Azure biedt verschillende connectiviteit opties tooconnect uw lokale infrastructuur tooyour Azure-infrastructuur.

* Punt-naar-site
* Virtueel netwerk site-naar-site
* ExpressRoute

Het verdient aanbeveling toouse ExpressRoute. Met ExpressRoute kunt u particuliere verbindingen maken tussen Azure-datacenters en infrastructuur on-premises of in een co-locatie-omgeving. ExpressRoute-verbindingen gaan niet via Hallo openbare Internet. Ze bieden meer betrouwbaarheid, sneller en hebben ze lagere latenties en betere beveiliging dan gewone verbindingen via Internet Hallo.
Terwijl het verdient aanbeveling toouse ExpressRoute, kunt u eventuele verbindingsmethode die het meest geschikt voor uw organisatie. meer informatie over ExpressRoute- en Hallo toolearn verschillende connectiviteitsopties met ExpressRoute kunt lezen [technisch overzicht van ExpressRoute](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Opslagaccount maken
In de volgorde toomaintain hoge beschikbaarheid en te voorkomen dat de afhankelijkheid van een enkele storage-account, kunt u twee storage-accounts maken. Hallo-machines in elke beschikbaarheidsset verdelen in twee groepen en vervolgens een afzonderlijke opslagaccount toewijzen elke groep.

![Opslagaccount maken](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Beschikbaarheidssets maken
Maak voor elke rol (DC/AD FS en WAP), beschikbaarheidssets met 2 machines op Hallo minimale. Hiermee kunt u een hogere beschikbaarheid voor elke rol bereiken. Maken Hallo beschikbaarheid wordt ingesteld, zijn maar er essentiële toodecide op Hallo volgende:

* **Fault-domeinen**: virtuele machines in dezelfde fout domein delen Hallo Hallo dezelfde stroombron en fysieke netwerkschakelaar. Minimaal twee foutdomeinen worden aanbevolen. de standaardwaarde Hallo 3 en kunt u deze zo voor Hallo doel van deze implementatie
* **Bijwerken van domeinen**: Machines die horen toohello hetzelfde updatedomein tegelijk opnieuw worden gestart tijdens het bijwerken. Wilt u toohave minimaal 2 update-domeinen. Hallo-standaardwaarde is 5 en kunt u deze zo voor Hallo doel van deze implementatie

![Beschikbaarheidssets](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

Hallo na beschikbaarheidssets maken

| Beschikbaarheidsset | Rol | Foutdomeinen | Updatedomeinen |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Virtuele machines implementeren
de volgende stap Hallo is toodeploy virtuele machines die als Hallo verschillende rollen in uw infrastructuur host. De aanbevolen configuratie is minimaal twee machines per beschikbaarheidsset. Vier virtuele machines voor de eenvoudige implementatie Hallo maken.

| Machine | Rol | Subnet | Beschikbaarheidsset | Storage-account | IP-adres |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |Statisch |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |Statisch |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |Statisch |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |Statisch |

Zoals u misschien al hebt gezien, is er geen NSG opgegeven. Dit is omdat azure kunt u NSG op subnetniveau hello gebruiken. U kunt vervolgens machine netwerkverkeer beheren met behulp van Hallo afzonderlijke NSG die is gekoppeld aan een subnet Hallo anders Hallo NIC-object. Zie [Wat is een netwerkbeveiligingsgroep (NSG)?](https://aka.ms/Azure/NSG) voor meer informatie.
Statisch IP-adres wordt aanbevolen als u Hallo DNS beheert. U kunt Azure DNS gebruiken en in plaats daarvan in Hallo DNS-records voor uw domein, verwijzen toohello nieuwe machines door hun Azure FQDN's.
Het deelvenster van de virtuele machine moet eruitzien als hieronder wanneer Hallo-implementatie is voltooid:

![Virtuele machines geïmplementeerd](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5. Configureren van het Hallo-domeincontroller / AD FS-servers
 In de volgorde tooauthenticate moet elke inkomende aanvraag, AD FS toocontact Hallo-domeincontroller. toosave hello kostbare reis vanaf Azure tooon lokale domeincontroller voor verificatie, wordt aanbevolen toodeploy een replica van de domeincontroller Hallo in Azure. In de volgorde tooattain hoge beschikbaarheid, wordt aangeraden toocreate een van ten minste 2-domeincontrollers beschikbaarheidsset.

| Domeincontroller | Rol | Storage-account |
|:---:|:---:|:---:|
| contosodc1 |Replica |contososac1 |
| contosodc2 |Replica |contososac2 |

* Promoveer Hallo twee servers tot replicadomeincontrollers met DNS
* Hallo AD FS-servers configureren door te installeren met behulp van Serverbeheer Hallo Hallo AD FS-rol.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. Interne load balancer (ILB) implementeren
**6.1. Hallo ILB maken**

toodeploy een ILB, selecteer Load Balancers in hello Azure-portal en klik op toevoegen (+).

> [!NOTE]
> Als er geen **Load Balancers** in het menu, klikt u op **Bladeren** in Hallo linksonder van Hallo-portal en schuif totdat er **Load Balancers**.  Klik vervolgens op Hallo gele ster tooadd het tooyour menu. Nu selecteren Hallo nieuwe pictogram tooopen Hallo Configuratiescherm toobegin taakverdelingsconfiguratie Hallo load balancer.
> 
> 

![Bladeren naar load balancer](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **Naam**: elke load balancer die de naam van de geschikte toohello geven
* **Schema**: omdat deze load balancer wordt geplaatst voor Hallo AD FS-servers en is bedoeld voor interne netwerkverbindingen alleen 'Interne' selecteren
* **Virtueel netwerk**: Kies Hallo virtueel netwerk waar u uw AD FS implementeert
* **Subnet**: Kies Hallo hier interne subnet
* **IP-adrestoewijzing**: statisch

![Interne load balancer](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

Nadat u op maken en Hallo ILB is geïmplementeerd, moet u deze bekijken in de lijst van de load balancers Hallo:

![Load balancers na ILB](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

Volgende stap is tooconfigure Hallo back-endpool en Hallo back-end-test.

**6.2. ILB-back-endpool configureren**

Selecteer hello ILB nieuw wordt gemaakt in Hallo Load Balancers Configuratiescherm. Het wordt paneel met toepassingsinstellingen hello geopend. 

1. Back-endpools van het paneel met toepassingsinstellingen Hallo selecteren
2. Voeg in Hallo Configuratiescherm voor back-end-pool, klik op de virtuele machine toevoegen
3. In het volgende deelvenster kunt u een beschikbaarheidsset kiezen
4. Hallo AD FS-beschikbaarheidsset kiezen

![ILB-back-endpool configureren](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3. Test configureren**

Selecteer in de Hallo ILB paneel met toepassingsinstellingen, tests.

1. Klik op Toevoegen
2. Geef details op voor test a. **Naam**: naam van test b. **Protocol**: TCP c. **Poort**: 443 (HTTPS) d. **Interval**: 5 (standaardwaarde) – dit waarmee ILB Hallo-machines in Hallo back-endpool e wordt probe hello-interval is. **Drempelwaarde voor onjuiste status limiet**: 2 (standaard waarde opnemen ue) – dit Hallo drempelwaarde voor opeenvolgende testfouten waarna ILB een machine wordt gedeclareerd in Hallo back-end van toepassingen niet meer reageert en stoppen verzenden verkeer tooit is.

![Test ILB configureren](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4. Taakverdelingsregels maken**

In de volgorde tooeffectively saldo Hallo verkeer moet Hallo ILB worden geconfigureerd met load-balancingregels. In volgorde toocreate een regel voor taakverdeling 

1. De Load Balancer-regel op basis van het paneel met toepassingsinstellingen Hallo Hallo ILB selecteren
2. Klik op toevoegen in Hallo Load balancing regel Configuratiescherm
3. Hallo toevoegen wordt geladen taakverdeling regel Configuratiescherm een. **Naam**: Geef een naam op voor Hallo regel b. **Protocol**: selecteer TCP c. **Poort**: 443 d. **Back-endpoort**: 443 e. **Back-endpool**: u hebt gemaakt voor hello AD FS cluster eerdere f Hallo-toepassingen te selecteren. **Test**: Selecteer Hallo test eerder hebt gemaakt voor AD FS-servers

![ILB-taakverdelingsregels configureren](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5. DNS bijwerken met ILB**

Ga tooyour DNS-server en maakt een CNAME voor Hallo ILB. Hallo CNAME moet voor de federation-service Hallo met Hallo IP-adres toohello IP-adres van Hallo ILB aan te wijzen. Bijvoorbeeld als Hallo ILB DIP adres 10.3.0.8 en Hallo federation-service geïnstalleerd is fs.contoso.com, maakt u een CNAME voor fs.contoso.com too10.3.0.8 aan te wijzen.
Dit zorgt ervoor dat alle communicatie met betrekking tot uiteindelijk op Hallo ILB fs.contoso.com en zijn op de juiste wijze gerouteerd.

### <a name="7-configuring-hello-web-application-proxy-server"></a>7. Hallo Web Application Proxy server configureren
**7.1. Hallo Web Application Proxy-servers tooreach AD FS-servers configureren**

In de volgorde tooensure of Web Application Proxy-servers kunnen tooreach Hallo AD FS-servers achter Hallo ILB zijn, maakt u een record in Hallo %systemroot%\system32\drivers\etc\hosts voor Hallo ILB. Houd er rekening mee dat Hallo DN-naam (Distinguished Name) moet Hallo federatieve-servicenaam, bijvoorbeeld fs.contoso.com. En Hallo IP-vermelding moet die Hallo ILB van IP-adres (10.3.0.8 zoals in Hallo voorbeeld).

**7.2. Hallo Web Application Proxy-rol installeren**

Nadat u ervoor zorgen dat Web Application Proxy-servers kunnen tooreach Hallo AD FS-servers achter ILB, kunt u naast Hallo Web Application Proxy-servers installeren. Web Application Proxy-servers niet worden gekoppeld toohello domein. Hallo Web Application Proxy rollen op Hallo twee Web Application Proxy-servers installeren door te selecteren van Hallo RAS-functie. Hallo Serverbeheer leidt u toocomplete Hallo WAP-installatie.
Lees voor meer informatie over het toodeploy WAP, [installeren en configureren van Hallo Web Application Proxy Server](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.  Hallo Internet (openbaar) gerichte Load Balancer implementeren
**8.1.  Internetgerichte (openbare) load balancer maken**

In hello Azure-portal, selecteert u Load balancers en klik vervolgens op toevoegen. Geef in Hallo maken load balancer deelvenster Hallo volgende informatie

1. **Naam**: naam voor de Hallo load balancer
2. **Schema**: Openbaar. Met deze optie geeft u aan dat de load balancer een openbaar adres nodig heeft.
3. **IP-adres**: maak een nieuw IP-adres (dynamisch)

![Internetgerichte load balancer](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

Na de implementatie weergegeven Hallo load balancer in Hallo Load balancers lijst.

![Lijst met load balancers](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2. Een DNS-label toohello openbare IP-adres toewijzen**

Klik op Hallo van een nieuw gemaakt load balancer-vermelding in Hallo Load balancers Configuratiescherm toobring up Hallo Configuratiescherm voor de configuratie. Volg onderstaande stappen tooconfigure Hallo DNS-label voor Hallo openbare IP-adres:

1. Klik op Hallo openbaar IP-adres. Hiermee opent u Hallo-deelvenster voor Hallo openbare IP-adres en de bijbehorende instellingen
2. Klik op Configuratie
3. Geef een DNS-label op. Hiermee worden het openbare DNS-label hello, die u vanaf elke locatie, bijvoorbeeld contosofs.westus.cloudapp.azure.com openen kunt. U kunt een vermelding toevoegen in Hallo de externe DNS-server voor Hallo federation-service (zoals fs.contoso.com) die wordt omgezet toohello DNS-label Hallo externe load balancer (contosofs.westus.cloudapp.azure.com).

![Internetgerichte load balancer configureren](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![Internetgerichte load balancer (DNS) configureren](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3. Back-endpool voor internetgerichte (openbare) load balancer configureren** 

Volg Hallo dezelfde stappen als in het maken van Hallo interne load balancer, tooconfigure Hallo back-end-adresgroep voor Load Balancer als Hallo beschikbaarheid Internet Facing (openbaar) ingesteld voor Hallo WAP-servers. Bijvoorbeeld: contosowapset.

![Back-endpool voor internetgerichte (openbare) load balancer configureren](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4. Test configureren**

Volg dezelfde stappen als in Hallo interne load balancer tooconfigure Hallo-test voor Hallo back-endpool van de WAP-servers configureren Hallo.

![Test voor internetgerichte load balancer configureren](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5. Taakverdelingsregel(s) maken**

Volg dezelfde stappen als in ILB tooconfigure Hallo voor de load balancer-regel voor TCP 443 Hallo.

![Taakverdelingsregels van internetgerichte load balancer configureren](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9. Hallo-netwerk te beveiligen
**9.1. Hallo intern subnet beveiligen**

Over het algemeen moet u Hallo volgens de regels voor tooefficiently beveiligen van uw interne subnet (in volgorde van de Hallo onderstaande)

| Regel | Beschrijving | Stroom |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Hallo HTTPS-communicatie van DMZ toestaan |Inkomend |
| DenyInternetOutbound |Er is geen toointernet toegang |Uitgaand |

![INT-toegangsregels (inkomend)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[opmerking]: <> (![INT-toegangsregels (inkomend)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [opmerking]: <> (![INT-toegangsregels (uitgaand)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2. Hallo DMZ subnet beveiligen**

| Regel | Beschrijving | Stroom |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |HTTPS vanaf internet toohello DMZ toestaan |Inkomend |
| DenyInternetOutbound |Alles behalve HTTPS toointernet is geblokkeerd |Uitgaand |

![EXT-toegangsregels (inkomend)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[opmerking]: <> (![EXT-toegangsregels (inkomend)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [opmerking]: <> (![EXT-toegangsregels (uitgaand)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> Als verificatie met certificaat van clientgebruiker (clientTLS-verificatie met X509-gebruikerscertificaten) is vereist, vereist AD FS vervolgens dat TCP-poort 49443 voor inkomende toegang wordt ingeschakeld.
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10. Hallo AD FS-aanmeldingspagina testen
Hallo gemakkelijkst tootest die AD FS is met behulp van Hallo IdpInitiatedSignon.aspx pagina. Hallo in volgorde toobe kunnen toodo dat vereist tooenable is IdpInitiatedSignOn op Hallo AD FS-eigenschappen. Volg onderstaande tooverify Hallo stappen uw AD FS-installatie

1. Voer wordt Hallo hieronder cmdlet op Hallo AD FS-server, met behulp van PowerShell, tooset tooenabled is ingesteld.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. Ga vanaf een externe computer naar https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx  
3. U ziet Hallo AD FS-pagina, zoals hieronder:

![Aanmeldingspagina testen](./media/active-directory-aadconnect-azure-adfs/test1.png)

Bij een geslaagde aanmelding wordt een soortgelijk positief bericht weergegeven:

![Test geslaagd](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Sjabloon voor de implementatie van AD FS in Azure
Hallo sjabloon implementeert een 6-machine-instellingen, 2 voor domeincontrollers, AD FS en WAP.

[Implementatiesjabloon voor AD FS in Azure](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

U kunt een bestaand virtueel netwerk gebruiken of een nieuw VNET maken tijdens het implementeren van deze sjabloon. Hallo verschillende parameters beschikbaar voor het aanpassen van Hallo-implementatie hieronder met de beschrijving van het gebruik van de parameter in het implementatieproces Hallo HALLO hallo weergegeven worden. 

| Parameter | Beschrijving |
|:--- |:--- |
| Locatie |Hallo regio toodeploy Hallo bronnen in, bijvoorbeeld VS-Oost. |
| StorageAccountType |Hallo type Hallo Storage-Account is gemaakt |
| VirtualNetworkUsage |Geeft aan of een nieuw virtueel netwerk wordt gemaakt of een bestaand wordt gebruikt |
| VirtualNetworkName |Hallo-naam van Hallo virtueel netwerk tooCreate, verplicht op bestaande of nieuwe gebruik van virtueel netwerk |
| VirtualNetworkResourceGroupName |Geeft de naam Hallo van resourcegroep Hallo waarin Hallo bestaand virtueel netwerk zich bevindt. Wanneer u een bestaand virtueel netwerk, wordt dit een verplichte parameter dus Hallo implementatie Hallo-ID van een bestaand virtueel netwerk Hallo vindt |
| VirtualNetworkAddressRange |adresbereik van Hallo Hallo nieuwe VNET, verplicht als u een nieuw virtueel netwerk maken |
| InternalSubnetName |Hallo-naam van Hallo intern subnet, verplicht op beide gebruiksopties virtueel netwerk (nieuw of bestaand) |
| InternalSubnetAddressRange |Hallo-adresbereik van de interne subnet hello, Hallo-domeincontrollers en AD FS-servers, verplichte bevat als een nieuw virtueel netwerk maken. |
| DMZSubnetAddressRange |Hallo-adresbereik van Hallo dmz subnet, waardoor Hallo Windows application proxy-servers, verplicht bevat als u een nieuw virtueel netwerk maken. |
| DMZSubnetName |Hallo-naam van Hallo intern subnet, verplicht op beide gebruiksopties virtueel netwerk (nieuw of bestaand). |
| ADDC01NICIPAddress |Hallo interne IP-adres van de eerste domeincontroller hello, dit IP-adres wordt toohello DC statisch toegewezen en moet een geldig IP-adres in het interne subnet Hallo |
| ADDC02NICIPAddress |Hallo interne IP-adres van de tweede domeincontroller hello, dit IP-adres wordt toohello DC statisch toegewezen en moet een geldig IP-adres in het interne subnet Hallo |
| ADFS01NICIPAddress |Hallo interne IP-adres van de eerste AD FS-server hello, dit IP-adres worden statisch toegewezen toohello ADFS-server en moet een geldig IP-adres in het interne subnet Hallo |
| ADFS02NICIPAddress |Hallo interne IP-adres van de tweede ADFS-server hello, dit IP-adres worden statisch toegewezen toohello ADFS-server en moet een geldig IP-adres in het interne subnet Hallo |
| WAP01NICIPAddress |Hallo interne IP-adres van de eerste WAP-server hello, dit IP-adres worden statisch toegewezen toohello WAP-server en moet een geldig IP-adres binnen Hallo DMZ subnet |
| WAP02NICIPAddress |Hallo interne IP-adres van de tweede WAP-server hello, dit IP-adres worden statisch toegewezen toohello WAP-server en moet een geldig IP-adres binnen Hallo DMZ subnet |
| ADFSLoadBalancerPrivateIPAddress |Hallo interne IP-adres van Hallo ADFS de load balancer, dit IP-adres worden statisch toegewezen toohello load balancer en moet een geldig IP-adres in het interne subnet Hallo |
| ADDCVMNamePrefix |Naamvoorvoegsel van virtuele machine voor domeincontrollers |
| ADFSVMNamePrefix |Naamvoorvoegsel van virtuele machine voor ADFS-servers |
| WAPVMNamePrefix |Naamvoorvoegsel van virtuele machine voor WAP-servers |
| ADDCVMSize |Hallo vm-grootte van Hallo-domeincontrollers |
| ADFSVMSize |Hallo vm-grootte van Hallo ADFS-servers |
| WAPVMSize |Hallo vm-grootte van Hallo WAP-servers |
| AdminUserName |Hallo-naam van lokale beheerder van de virtuele machines van Hallo Hallo |
| AdminPassword |Hallo-wachtwoord voor het lokale Administrator-account Hallo Hallo virtuele machines |

## <a name="additional-resources"></a>Aanvullende bronnen
* [Beschikbaarheidssets](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [Interne load balancer](https://aka.ms/Azure/ILB/Internal)
* [Internetgerichte load balancer](https://aka.ms/Azure/ILB/Internet)
* [Opslagaccounts](https://aka.ms/Azure/Storage)
* [Virtuele netwerken van Azure](https://aka.ms/Azure/VNet)
* [Koppelingen voor AD FS en webtoepassingsproxy](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Volgende stappen
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)
* [De AD FS configureren en beheren met Azure AD Connect](active-directory-aadconnectfed-whatis.md)
* [AD FS-implementaties in meerdere regio’s in Azure, met maximale beschikbaarheid dankzij Azure Traffic Manager](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

