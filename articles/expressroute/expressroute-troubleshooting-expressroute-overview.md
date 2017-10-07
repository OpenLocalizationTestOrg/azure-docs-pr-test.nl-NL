---
title: 'Controleren of verbinding: Azure ExpressRoute Troubleshooting Guide | Microsoft Docs'
description: Deze pagina vindt u instructies voor het oplossen van problemen en end tooend verbinding van een ExpressRoute-circuit valideren.
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>ExpressRoute-verbinding controleren
ExpressRoute, die een uitbreiding is een on-premises netwerk via een persoonlijke verbinding die wordt gefaciliteerd door een connectiviteitsprovider in Hallo Microsoft cloud, omvat Hallo drie afzonderlijke netwerkzones te volgen:

-   Klantnetwerk
-   Serviceprovider-netwerk
-   Microsoft-datacentrum

Hallo-doel van dit document is toohelp gebruiker tooidentify waar (of zelfs als) een verbindingsprobleem bestaat en in welke zone, waardoor tooseek hulp van de juiste team tooresolve Hallo probleem. Als de ondersteuning van Microsoft nodig tooresolve een probleem is, opent u een ondersteuningsticket met [Microsoft Support][Support].

> [!IMPORTANT]
> Dit document is bedoeld toohelp opsporen en oplossen van eenvoudige problemen. Het is niet bedoeld toobe vervanging voor ondersteuning van Microsoft. Open een ondersteuningsticket met [Microsoft Support] [ Support] bent u toosolve Hallo probleem op door middel van Hallo richtlijnen.
>
>

## <a name="overview"></a>Overzicht
Hallo toont volgende diagram Hallo logische verbinding van een klant tooMicrosoft netwerk van het netwerk met behulp van ExpressRoute.
[![1]][1]

In Hallo voorgaande diagram, aangeven Hallo cijfers netwerk belangrijke punten. Hallo netwerk punten zijn vaak in dit artikel verwezen door hun bijbehorende nummers.

Afhankelijk van Hallo ExpressRoute connectiviteit mogelijk model (Cloud Exchange CO-locatie, Point-to-Point Ethernet-verbinding of Any-to-any (IPVPN)) Hallo netwerk punten 3 en 4 switches (Layer 2-apparaten). Hallo netwerk belangrijke punten geïllustreerd zijn als volgt:

1.  Klant compute-apparaat (bijvoorbeeld een server of een PC)
2.  CEs: Klant-randrouters 
3.  PEs (CE facing): Provider rand routers/schakelaars waarmee worden geconfronteerd randrouters klant. Tooas PE CEs in dit document wordt verwezen.
4.  PEs (MSEE facing): Provider rand routers/schakelaars waarmee worden geconfronteerd msee's. Tooas PE-msee's in dit document wordt verwezen.
5.  Msee's: Microsoft Enterprise Edge (MSEE) ExpressRoute-routers
6.  De Gateway virtuele netwerk (VNet)
7.  COMPUTE-apparaat op Hallo Azure VNet

Als u connectiviteitsmodellen Hallo Cloud Exchange CO-locatie of Point-to-Point Ethernet-verbinding gebruikt, zou Hallo klant edge router (2) tot stand brengen BGP-peer met msee's (5). Netwerk punten 3 en 4 wordt nog steeds aanwezig zijn, maar enigszins transparant als Layer 2-apparaten.

Als Hallo Any-to-any (IPVPN) connectiviteit model wordt gebruikt, Hallo PEs (MSEE facing) (4) zou tot stand brengen BGP-peer met msee's (5). Routes zou worden doorgegeven aan een netwerk van de klant back toohello via Hallo IPVPN serviceprovider-netwerk.

>[!NOTE]
>Microsoft vereist voor ExpressRoute hoge beschikbaarheid, een paar redundante BGP-sessies tussen de msee's (5) en PE-msee's (4). Een paar redundante netwerkpaden wordt ook aangemoedigd tussen klantnetwerk en PE CEs. Echter, in Any-to-any (IPVPN) verbinding model één CE-apparaat (2) mogelijk verbonden tooone of meer PEs (3).
>
>

toovalidate een ExpressRoute-circuit Hallo stappen te volgen (met Hallo netwerk beheerpunt door Hallo gekoppeld getal aangegeven) worden behandeld:
1. [Valideren van circuitinrichting en status (5)](#validate-circuit-provisioning-and-state)
2. [Valideren van ten minste één ExpressRoute-peering is geconfigureerd (5)](#validate-peering-configuration)
3. [Valideren van ARP tussen Microsoft en Hallo serviceprovider (koppeling tussen 4 en 5)](#validate-arp-between-microsoft-and-the-service-provider)
4. [Valideren van BGP en routes op Hallo MSEE (BGP tussen too5 4 en 5 too6 als een VNet is verbonden)](#validate-bgp-and-routes-on-the-msee)
5. [Selectievakje Hallo verkeer-statistieken (verkeer doorlopen 5)](#check-the-traffic-statistics)

Meer validaties en controles worden toegevoegd in Hallo toekomstige, controle terug maandelijks!

##<a name="validate-circuit-provisioning-and-state"></a>Valideren van circuitinrichting en status
Ongeacht Hallo connectivity-model, heeft een ExpressRoute-circuit toobe gemaakt, en daarom een service sleutel gegenereerd voor het inrichten van het circuit. Een ExpressRoute-circuit inrichten, stelt u een redundante laag-2-verbindingen tussen PE-msee's (4) en de msee's (5). Zie voor meer informatie over hoe toocreate, wijzigen, inrichten en een ExpressRoute-circuit controleren Hallo artikel [maken en een ExpressRoute-circuit wijzigen][CreateCircuit].

>[!TIP]
>Een servicesleutel is een unieke identificatie voor een ExpressRoute-circuit. Deze sleutel is vereist voor de meeste Hallo powershell-opdrachten die in dit document worden vermeld. Bovendien moet u hulp nodig hebt van Microsoft of van een ExpressRoute-partner tootroubleshoot een probleem met ExpressRoute, Hallo service leveren sleutel tooreadily Hallo circuit identificeren.
>
>

###<a name="verification-via-hello-azure-portal"></a>Verificatie via hello Azure-portal
In hello Azure-portal, Hallo status van een ExpressRoute-circuit kan worden gecontroleerd door het selecteren van ![2][2] Hallo ExpressRoute-circuit op Hallo links zijmarge menu en vervolgens te selecteren. Selecteren van een ExpressRoute circuit vermeld onder 'Alle resources' hello ExpressRoute-circuit blade geopend. In Hallo ![3][3] sectie van Hallo blade Hallo ExpressRoute essentials worden vermeld, zoals wordt weergegeven in de volgende schermopname Hallo:

![4][4]    

In Hallo ExpressRoute Essentials *Circuit status* Hallo status van de Hallo circuit op Hallo Microsoft side aangeeft. *Providerstatus* geeft aan of Hallo circuit is *ingericht/niet ingericht* Hallo serviceprovider zijde. 

Voor een ExpressRoute-circuit toobe operationele, Hallo *Circuit status* moet *ingeschakeld* en Hallo *providerstatus* moet *ingericht*.

>[!NOTE]
>Als hello *Circuit status* is niet ingeschakeld, neem contact op met [Microsoft Support][Support]. Als hello *providerstatus* is niet ingericht, neem contact op met uw serviceprovider.
>
>

###<a name="verification-via-powershell"></a>Verificatie via PowerShell
toolist alle Hallo ExpressRoute-circuits in een resourcegroep, Hallo volgende opdracht gebruiken:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>U kunt de naam van uw resourcegroep ophalen via hello Azure-portal. Zie de vorige subsectie Hallo van dit document en houd er rekening mee dat naam resourcegroep Hallo Hallo voorbeeld schermopname wordt vermeld.
>
>

tooselect een bepaalde ExpressRoute-circuit in een resourcegroep of gebruik Hallo volgende opdracht:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

Er is een voorbeeldantwoord:

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm als een ExpressRoute-circuit functioneert, betalen bijzondere aandacht toohello velden te volgen:

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>Als hello *CircuitProvisioningState* is niet ingeschakeld, neem contact op met [Microsoft Support][Support]. Als hello *ServiceProviderProvisioningState* is niet ingericht, neem contact op met uw serviceprovider.
>
>

###<a name="verification-via-powershell-classic"></a>Verificatie via PowerShell (klassiek)
toolist alle Hallo ExpressRoute-circuits voor een abonnement, Hallo volgende opdracht gebruiken:

    Get-AzureDedicatedCircuit

tooselect een bepaalde ExpressRoute-circuit Hallo volgende opdracht gebruiken:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

Er is een voorbeeldantwoord:

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm als een ExpressRoute-circuit functioneert, betaalt u speciale aandacht toohello velden te volgen: ServiceProviderProvisioningState: Status ingericht: ingeschakeld

>[!NOTE]
>Als hello *Status* is niet ingeschakeld, neem contact op met [Microsoft Support][Support]. Als hello *ServiceProviderProvisioningState* is niet ingericht, neem contact op met uw serviceprovider.
>
>

##<a name="validate-peering-configuration"></a>Peeringconfiguratie valideren
Nadat het Hallo-aanbieder heeft voltooide Hallo Hallo ExpressRoute-circuit inrichten, kan een routeringsconfiguratie worden gemaakt via Hallo ExpressRoute-circuit tussen de MSEE-PRs (4) en de msee's (5). Elk ExpressRoute-circuit kan hebben een, twee of drie routing-contexten ingeschakeld: persoonlijke Azure-peering (verkeer tooprivate virtuele netwerken in Azure) en Microsoft-peering (verkeer tooOffice 365 openbare Azure-peering (verkeer toopublic IP-adressen in Azure) (en Dynamics 365). Voor meer informatie over het toocreate en routeringsconfiguratie wijzigen, Zie het artikel Hallo [maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering].

###<a name="verification-via-hello-azure-portal"></a>Verificatie via hello Azure-portal
>[!IMPORTANT]
>Er is een bekend probleem in hello Azure-portal ExpressRoute peerings zijn, waarbij de *niet* wordt weergegeven in het Hallo-portal als geconfigureerd door Hallo-provider. Toevoegen van ExpressRoute-peerings via Hallo portal of PowerShell *overschrijft Hallo service Providerinstellingen*. Deze actie wordt verbroken Hallo routering op Hallo ExpressRoute-circuit en vereist ondersteuning van Hallo service toorestore Hallo Providerinstellingen Hallo en herstellen van de normale routering. Hallo ExpressRoute peerings alleen wijzigen als deze bepaalde dat die Hallo serviceprovider biedt alleen een layer 2-services!
>
>

<p/>
>[!NOTE]
>Als laag 3 is opgegeven door Hallo service provider en Hallo peerings leeg in Hallo-portal zijn, zijn PowerShell gebruikte toosee Hallo service-instellingen voor provider geconfigureerd.
>
>

In hello Azure-portal, de status van een ExpressRoute-circuit kan worden gecontroleerd door te selecteren ![2][2] Hallo ExpressRoute-circuit op Hallo links zijmarge menu en vervolgens te selecteren. Selecteren van een ExpressRoute zou circuit vermeld onder 'Alle resources' Hallo ExpressRoute-circuit blade geopend. In Hallo ![3][3] sectie van Hallo blade Hallo ExpressRoute essentials zou worden weergegeven, zoals wordt weergegeven in de volgende schermopname Hallo:

![5][5]

In de Hallo voorgaande voorbeeld, als vermelde Azure is persoonlijke peering routering context ingeschakeld, terwijl Azure openbare en Microsoft peering routing-contexten zijn niet ingeschakeld. Een context die peering is ingeschakeld, moet ook Hallo primaire en secundaire point-to-point (vereist voor BGP)-subnetten die worden vermeld. Hallo /30 subnetten worden gebruikt voor het Hallo-interface IP-adres Hallo msee's en PE-msee's. 

>[!NOTE]
>Als een peering niet is ingeschakeld, controleert u als Hallo primaire en secundaire subnetten toegewezen overeenkomen Hallo-configuratie op PE-msee's. Als geen toochange Hallo configuratie op MSEE-routers, raadpleeg dan te[maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>Verificatie via PowerShell
tooget hello Azure persoonlijke peering configuratiedetails Hallo volgende opdrachten gebruiken:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

Een antwoord voorbeeld voor een correct geconfigureerde persoonlijke peering, is:

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 Een context die is ingeschakeld peering moet Hallo primaire en secundaire adresvoorvoegsels vermeld. Hallo /30 subnetten worden gebruikt voor het Hallo-interface IP-adres Hallo msee's en PE-msee's.

tooget hello Azure openbare peering configuratiedetails Hallo opdrachten na gebruiken:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget hello Microsoft peering configuratiedetails Hallo volgende opdrachten gebruiken:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

Als een peering niet is geconfigureerd, zou er een foutbericht weergegeven. Een voorbeeldantwoord wanneer Hallo vermeld peering (Azure openbare peering in dit voorbeeld) niet is geconfigureerd binnen Hallo circuit:

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>Als een peering niet is ingeschakeld, controleert u of de primaire en secundaire subnetten toegewezen overeen Hallo-configuratie op Hallo Hallo PE MSEE gekoppeld. Ook controleren of hello corrigeren *VlanId*, *AzureASN*, en *PeerASN* op msee's worden gebruikt en als deze waarden worden toegewezen toohello zijn gebruikt op Hallo gekoppeld PE MSEE. Als MD5-hash is gekozen, is Hallo gedeelde sleutel moet hetzelfde zijn op de combinatie van MSEE en PE MSEE. toochange Hallo-configuratie op Hallo MSEE-routers te verwijzen [maken en wijzigen van routering voor een ExpressRoute-circuit] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>Verificatie via PowerShell (klassiek)
tooget hello Azure persoonlijke peering configuratiedetails Hallo volgende opdracht gebruiken:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

Is een reactie voorbeeld voor een persoonlijke peering Prestatietesten zijn geconfigureerd:

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

Een ingeschakeld is, peering context Hallo primaire en secundaire peer subnetten vermeld zou hebben. Hallo /30 subnetten worden gebruikt voor het Hallo-interface IP-adres Hallo msee's en PE-msee's.

tooget hello Azure openbare peering configuratiedetails Hallo opdrachten na gebruiken:

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget hello Microsoft peering configuratiedetails Hallo volgende opdrachten gebruiken:

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>Als laag 3-peerings zijn ingesteld door de serviceprovider hello, overschreven Hallo ExpressRoute peerings via Hallo portal of PowerShell instellen Hallo serviceprovider instellingen. Opnieuw instellen van Hallo side peering Providerinstellingen vereist Hallo-ondersteuning van Hallo-provider. Hallo ExpressRoute peerings alleen wijzigen als deze bepaalde dat die Hallo serviceprovider biedt alleen een layer 2-services!
>
>

<p/>
>[!NOTE]
>Als een peering niet is ingeschakeld, controleert u of Hallo primaire en secundaire peer subnetten toegewezen overeen Hallo-configuratie op Hallo PE MSEE gekoppeld. Ook controleren of hello corrigeren *VlanId*, *AzureAsn*, en *PeerAsn* op msee's worden gebruikt en als deze waarden worden toegewezen toohello zijn gebruikt op Hallo gekoppeld PE MSEE. toochange Hallo-configuratie op Hallo MSEE-routers te verwijzen [maken en wijzigen van routering voor een ExpressRoute-circuit] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>ARP tussen Microsoft en Hallo serviceprovider valideren
Deze sectie wordt gebruikt (klassiek) PowerShell-opdrachten. Als u PowerShell Azure Resource Manager-opdrachten gebruikt hebt, zorg ervoor dat er beheerder/co-beheerder toegang toohello abonnement via de [klassieke Azure-portal][OldPortal]. Voor het oplossen van problemen met Azure Resource Manager opdrachten raadpleegt u toohello [ARP ophalen van tabellen in de Resource Manager-implementatiemodel Hallo] [ ARP] document.

>[!NOTE]
>tooget ARP, zowel hello Azure-portal en Azure Resource Manager PowerShell-opdrachten kan worden gebruikt. Als er fouten optreden met hello Azure Resource Manager PowerShell-opdrachten, klassieke PowerShell-opdrachten gebruiken als klassieke PowerShell opdrachten ook worden gebruikt met Azure Resource Manager ExpressRoute-circuits.
>
>

tooget ARP-tabel uit de primaire MSEE router voor persoonlijke peering Hallo Hallo Hallo, Hallo volgende opdracht gebruiken:

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Een voorbeeld van antwoord voor Hallo-opdracht in Hallo geslaagde scenario:

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

Op deze manier kunt u controleren Hallo ARP-tabel uit Hallo MSEE in Hallo *primaire*/*secundaire* pad voor *persoonlijke* /  *Openbare*/*Microsoft* peerings.

Hallo bestaat volgende voorbeeld toont Hallo respons van Hallo-opdracht voor een peering niet.

    ARP Info:
       
>[!NOTE]
>Als Hallo ARP-tabel geen heeft toegewezen IP-adressen van de interfaces Hallo tooMAC adressen, bekijk Hallo volgende informatie:
>1. Als het eerste IP-adres Hallo van Hallo /30 subnet voor Hallo koppeling tussen toegewezen Hallo MSEE PR en MSEE wordt gebruikt op Hallo-interface van MSEE PR. Azure gebruikt altijd Hallo tweede IP-adres voor de msee's.
>2. Controleer of als Hallo klant (C-code) en VLAN-servicetags (S-Tag) overeenkomt met beide op een combinatie van MSEE PR en MSEE.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>BGP-routes op Hallo MSEE en valideren
Deze sectie wordt gebruikt (klassiek) PowerShell-opdrachten. Als u PowerShell Azure Resource Manager-opdrachten gebruikt hebt, zorg ervoor dat er beheerder/co-beheerder toegang toohello abonnement via de [klassieke Azure-portal][OldPortal]

>[!NOTE]
>tooget BGP gegevens, zowel hello Azure-portal en Azure Resource Manager PowerShell-opdrachten kunnen worden gebruikt. Als er fouten optreden met hello Azure Resource Manager PowerShell-opdrachten, klassieke PowerShell-opdrachten gebruiken als klassieke PowerShell opdrachten ook worden gebruikt met Azure Resource Manager ExpressRoute-circuits.
>
>

tooget Hallo routeringstabel (neighbor BGP) voor een bepaalde routering context samenvatting, Hallo volgende opdracht gebruiken:

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

Er is een voorbeeld van antwoord:

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Zoals u in het voorgaande voorbeeld Hallo, is Hallo opdracht nuttig toodetermine voor hoe lang Hallo routering context is ingesteld. Het aantal route voorvoegsels die worden geadverteerd door de peering router hello wordt tevens aangegeven.

>[!NOTE]
>Als Hallo status in actief of inactief, controleert u of Hallo primaire en secundaire peer subnetten toegewezen overeen Hallo-configuratie op Hallo PE MSEE gekoppeld. Ook controleren of hello corrigeren *VlanId*, *AzureAsn*, en *PeerAsn* op msee's worden gebruikt en als deze waarden worden toegewezen toohello zijn gebruikt op Hallo gekoppeld PE MSEE. Als MD5-hash is gekozen, is Hallo gedeelde sleutel moet hetzelfde zijn op de combinatie van MSEE en PE MSEE. toochange Hallo-configuratie op Hallo MSEE-routers te verwijzen[maken en wijzigen van routering voor een ExpressRoute-circuit][CreatePeering].
>
>

<p/>
>[!NOTE]
>Als bepaalde bestemmingen niet bereikbaar via een bepaalde peering zijn, controleert u de routetabel Hallo van Hallo msee's die horen toohello bepaalde peering context. Als een overeenkomende voorvoegsel (kan worden NATed IP) in de routeringstabel Hallo aanwezig is, moet u controleren als er firewalls / / ACL's voor NSG op Hallo pad, en als ze Hallo verkeer is toegestaan.
>
>

tooget hello volledige routeringstabel van de MSEE op Hallo *primaire* pad voor bepaalde Hallo *persoonlijke* routering context, gebruik Hallo volgende opdracht:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Een geslaagde uitkomst voorbeeld voor Hallo-opdracht is:

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

Op deze manier kunt u de routeringstabel Hallo van Hallo MSEE in Hallo controleren *primaire*/*secundaire* pad voor *persoonlijke* / *Openbare*/*Microsoft* een peering context.

Hallo bestaat volgende voorbeeld toont Hallo respons van Hallo-opdracht voor een peering niet:

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Hallo verkeer statistieken controleren
Hallo tooget gecombineerd primaire en secundaire pad verkeer statistieken--bytes in en uit--van een peering context, gebruik Hallo volgende opdracht:

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Er is een voorbeeld van uitvoer van Hallo-opdracht:

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

Er is een voorbeeld van uitvoer van de opdracht Hallo voor een niet-bestaande peering:

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>Volgende stappen
Bekijk voor meer informatie en hulp Hallo koppelingen te volgen:

- [Microsoft-ondersteuning][Support]
- [Maken en een ExpressRoute-circuit wijzigen][CreateCircuit]
- [Maken en aanpassen van routering voor een ExpressRoute-circuit][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Logische Express Route-verbinding"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Pictogram voor alle resources"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Overzicht-pictogram"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "Schermopname van ExpressRoute Essentials-voorbeeld"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "Schermopname van ExpressRoute Essentials-voorbeeld"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






