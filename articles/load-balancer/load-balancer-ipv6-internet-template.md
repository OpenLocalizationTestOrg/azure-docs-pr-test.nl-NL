---
title: aaaDeploy load balancer in een internetgerichte met IPv6 - Azure-sjabloon | Microsoft Docs
description: Hoe toodeploy IPv6 ondersteuning bieden voor Azure Load Balancer en taakverdeling virtuele machines.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
keywords: IPv6-, azure load balancer, dual-stack, openbare IP-adres, systeemeigen ipv6, mobiele, iot
ms.assetid: 2998e943-13fc-4ea9-a68c-875e53a08db3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2016
ms.author: kumud
ms.openlocfilehash: 68b9ba874a50161243577b64c4a6d9c76b39156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-internet-facing-load-balancer-solution-with-ipv6-using-a-template"></a>Een internetgerichte load balancer-oplossing met IPv6 met een sjabloon implementeren

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [Azure CLI](load-balancer-ipv6-internet-cli.md)
> * [Sjabloon](load-balancer-ipv6-internet-template.md)

Azure Load Balancer is een Layer-4 (TCP, UDP) load balancer. Hallo load balancer biedt hoge beschikbaarheid door het distribueren van inkomend verkeer tussen orde service-exemplaren in cloudservices of virtuele machines in een load balancer-set. Azure Load Balancer kan deze services ook toepassen op meerdere poorten, meerdere IP-adressen of allebei.

## <a name="example-deployment-scenario"></a>Voorbeeldscenario voor implementatie

Hallo volgende diagram illustreert Hallo-oplossing voor taakverdeling wordt geïmplementeerd met behulp van Hallo voorbeeld van de sjabloon die in dit artikel wordt beschreven.

![Load balancer-scenario](./media/load-balancer-ipv6-internet-template/lb-ipv6-scenario.png)

In dit scenario maakt u hello Azure-resources te volgen:

* de virtuele netwerkinterface voor elke virtuele machine met zowel IPv4 als IPv6-adressen die zijn toegewezen
* een internetgerichte Load Balancer met een IPv4 en IPv6-openbare IP-adres
* twee laden taakverdeling regels toomap Hallo openbare VIP's toohello persoonlijke eindpunten
* een Beschikbaarheidsset met Hallo twee virtuele machines
* twee virtuele machines (VM's)

## <a name="deploying-hello-template-using-hello-azure-portal"></a>Met behulp van Azure-portal Hallo Hallo-sjabloon implementeren

In dit artikel wordt verwezen naar een sjabloon die is gepubliceerd in Hallo [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/201-load-balancer-ipv6-create/) galerie. U kunt Hallo sjabloon downloaden uit de galerie Hallo of Hallo-implementatie in Azure rechtstreeks vanuit het Hallo-galerie starten. In dit artikel wordt ervan uitgegaan dat u hebt gedownload Hallo sjabloon tooyour lokale computer.

1. Open hello Azure-portal en meld u aan met een account met machtigingen toocreate VM's en netwerkresources binnen een Azure-abonnement. Tenzij u van bestaande bronnen gebruikmaakt, Hallo-account moet ook machtiging toocreate een resourcegroep en een opslagaccount.
2. Klik op '+ Nieuw' van 'sjabloon' in het zoekvak Hallo uit en Hallo menu. Selecteer 'Sjabloonimplementatie' in de zoekresultaten Hallo.

    ![lb-ipv6-portal-stap 2](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step2.png)

3. Hallo alles in blade, klik op 'Sjabloonimplementatie'.

    ![lb-ipv6-portal-stap 3](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step3.png)

4. Klik op 'Maken'.

    ![lb-ipv6-portal-step4](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step4.png)

5. Klik op 'Sjabloon bewerken'. Verwijder de bestaande inhoud Hallo en kopiëren en plakken in de volledige inhoud van het sjabloonbestand Hallo Hallo (tooinclude Hallo begin en einde {}), klik op 'Opslaan'.

    > [!NOTE]
    > Als u Microsoft Internet Explorer, wanneer u u plakt verschijnt een dialoogvenster waarin u wordt gevraagd tooallow toegang toohello Windows Klembord. Klik op 'Toegang toestaan'.

    ![lb-ipv6-portal-step5](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step5.png)

6. Klik op 'Parameters bewerken'. In de blade Parameters Hallo Hallo-waarden per Hallo richtlijnen in Hallo sjabloonsectie parameters opgeven en klik vervolgens op 'Opgeslagen' blade tooclose Hallo-Parameters. Selecteer uw abonnement, met een bestaande resourcegroep of maak een Hallo aangepaste implementatie blade. Als u een resourcegroep maken wilt, selecteert u een locatie voor resourcegroep Hallo. Klik vervolgens op **juridische voorwaarden**, klikt u vervolgens op **aankoop** voor Hallo juridische voorwaarden. Azure begint Hallo resources implementeren. Het duurt enkele minuten toodeploy alle Hallo-resources.

    ![lb-ipv6-portal-step6](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step6.png)

    Zie voor meer informatie over deze parameters Hallo [sjabloonparameters en variabelen](#template-parameters-and-variables) verderop in dit artikel.

7. toosee hello resources gemaakt door de sjabloon hello, klik op Bladeren, schuif omlaag Hallo lijst totdat u overzicht 'Resourcegroepen' en klik vervolgens op het.

    ![lb-ipv6-portal-step7](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step7.png)

8. Klik op Hallo-resourceblade groepen Hallo-naam van Hallo-resourcegroep die u in stap 6 hebt opgegeven. U ziet een lijst met alle Hallo-resources die zijn geïmplementeerd. Als alles goed is gegaan, moet er 'Geslaagd' onder "Laatste implementatie". Als dat niet het geval is, zorg ervoor dat u Hallo-account machtigingen toocreate Hallo benodigde resources.

    ![lb-ipv6-portal-step8](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step8.png)

    > [!NOTE]
    > Als u uw resourcegroepen bladert onmiddellijk na het voltooien van stap 6, wordt 'Laatste implementatie' Hallo status van 'Implementatie' weergegeven tijdens het Hallo-resources worden geïmplementeerd.

9. Klik op 'myIPv6PublicIP' in hello lijst met resources. U ziet dat er een IPv6-adres onder IP-adres is en of de DNS-naam Hallo-waarde die u hebt opgegeven voor Hallo dnsNameforIPv6LbIP parameter in stap 6. Deze resource wordt Hallo openbare IPv6-adres en hostnaam naam die is toegankelijk tooInternet-clients.

    ![lb-ipv6-portal-step9](./media/load-balancer-ipv6-internet-template/lb-ipv6-portal-step9.png)

## <a name="validate-connectivity"></a>Connectiviteit valideren

Wanneer het Hallo-sjabloon is geïmplementeerd, kunt u connectiviteit valideren door te voeren Hallo taken te volgen:

1. Toohello aanmelden met Azure-portal en tooeach van virtuele machines die zijn gemaakt door de sjabloonimplementatie Hallo Hallo verbinding. Als u een Windows Server-VM ipconfig uitvoeren geïmplementeerd/alle vanaf een opdrachtprompt. U ziet dat Hallo VMs zowel IPv4 als IPv6-adressen hebben. Als u virtuele Linux-machines hebt geïmplementeerd, moet u tooconfigure Hallo Linux-besturingssysteem tooreceive dynamische IPv6-adressen met Hallo-instructies voor uw Linux-distributie.
2. Start een verbinding toohello openbare IPv6-adres van Hallo load balancer van een client verbonden met een IPv6-Internet. tooconfirm die Hallo load balancer is balancing tussen Hallo twee virtuele machines, kan u een webserver zoals Microsoft Internet Information Services (IIS) installeren op elk van de VM Hallo. Hallo standaardwebpagina op elke server kunnen bevatten tekst hello 'Server0' of 'Server1' toouniquely worden geïdentificeerd. Vervolgens opent u een Internet-browser op een client verbonden met een IPv6-Internet en toohello hostnaam die u hebt opgegeven voor Hallo dnsNameforIPv6LbIP parameter van Hallo load balancer tooconfirm end-to-end IPv6-connectiviteit tooeach VM bladeren. Als u alleen de webpagina Hallo van slechts één server, moet u mogelijk tooclear uw browser-cache. Open meerdere persoonlijke browsersessies. U ziet een reactie van elke server.
3. Start een verbinding toohello openbaar IPv4-adres van Hallo load balancer van een client verbonden met een IPv4-Internet. tooconfirm die Hallo load balancer is voor de load balancer Hallo twee virtuele machines, kan u testen met behulp van IIS, zoals beschreven in stap 2.
4. Starten van elke virtuele machine, een uitgaande verbinding tooan IPv6 of verbonden met een IPv4-Internet-apparaat. In beide gevallen is Hallo bron-IP gezien door Bestemmingsapparaat Hallo Hallo openbare IPv4- of IPv6-adres van Hallo load balancer.

> [!NOTE]
> ICMP voor zowel IPv4 als IPv6 wordt geblokkeerd in hello Azure-netwerk. ICMP-hulpprogramma's zoals altijd pingen mislukt als gevolg hiervan. tootest connectiviteit, gebruikt u een alternatieve TCP zoals TCPing of Hallo Test-NetConnection van PowerShell-cmdlet. Houd er rekening mee dat Hallo IP-adressen in Hallo diagram ziet u voorbeelden van waarden die u ziet mogelijk zijn. Aangezien Hallo IPv6-adressen dynamisch toegewezen worden, wordt Hallo-adressen die u ontvangt, verschillen en kunnen verschillen per regio. Bovendien is het gebruikelijk Hallo openbare IPv6-adres op Hallo load balancer toostart met een ander voorvoegsel dan Hallo persoonlijke IPv6-adressen in Hallo back-end-pool.

## <a name="template-parameters-and-variables"></a>Sjabloonparameters en variabelen

Een Azure Resource Manager-sjabloon bevat meerdere variabelen en parameters die u tooyour behoeften kunt aanpassen. Variabelen worden gebruikt voor vaste waarden dat u niet dat een gebruiker toochange wilt. Parameters worden gebruikt voor waarden dat een gebruiker tooprovide bij het implementeren van Hallo-sjabloon. Hallo-voorbeeldsjabloon is geconfigureerd voor het Hallo-scenario dat wordt beschreven in dit artikel. U kunt deze tooneeds van uw omgeving aanpassen.

Voorbeeld van de sjabloon die wordt gebruikt in dit artikel bevat de volgende Hallo Hallo parameters en variabelen:

| De parameter / Variable | Opmerkingen |
| --- | --- |
| adminUsername |Geef op Hallo-naam van het Hallo-beheerdersaccount toosign in toohello virtuele machines met gebruikt. |
| adminPassword |Geef op Hallo-wachtwoord voor Hallo beheeraccount toosign in toohello virtuele machines met gebruikt. |
| dnsNameforIPv4LbIP |Hallo DNS-hostnaam u tooassign wilt gebruiken als de openbare naam Hallo Hallo load balancer opgeven. Deze naam wordt omgezet toohello load balancer openbaar IPv4-adres. Hallo-naam moet worden kleine letters en overeen met reguliere expressie Hallo: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. |
| dnsNameforIPv6LbIP |Hallo DNS-hostnaam u tooassign wilt gebruiken als de openbare naam Hallo Hallo load balancer opgeven. Deze naam wordt omgezet toohello load balancer openbare IPv6-adres. Hallo-naam moet worden kleine letters en overeen met reguliere expressie Hallo: ^ [a-z][a-z0-9-]{1,61}[a-z0-9]$. Dit kan zijn Hallo dezelfde naam als Hallo IPv4-adres. Wanneer een client verzendt retourneren een DNS-query voor deze naam Azure zowel Hallo A en AAAA-records wanneer Hallo naam wordt gedeeld. |
| vmNamePrefix |Hallo VM voorvoegsel opgeven. Hallo sjabloon voegt een nummer (0, 1, enzovoort) toohello naam wanneer hello virtuele machines worden gemaakt. |
| nicNamePrefix |Geef Hallo network interface-voorvoegsel. Hallo sjabloon voegt een nummer (0, 1, enzovoort) toohello naam wanneer Hallo netwerkinterfaces worden gemaakt. |
| storageAccountName |Voer Hallo-naam van een bestaand opslagaccount of Hallo-naam van een nieuwe één toobe gemaakt door Hallo sjabloon opgeven. |
| availabilitySetName |Voer de naam van de beschikbaarheid van Hallo toobe gebruikt met virtuele machines Hallo instellen |
| addressPrefix |Hallo-adresvoorvoegsel gebruikt toodefine Hallo-adresbereik van Hallo virtueel netwerk |
| subnetName |Hallo-naam van Hallo subnet in voor Hallo VNet gemaakt |
| subnetPrefix |Hallo-adresvoorvoegsel toodefine Hallo-adresbereik van Hallo subnet gebruikt |
| vnetName |Geef de naam Hallo voor Hallo VNet die wordt gebruikt door Hallo virtuele machines. |
| ipv4PrivateIPAddressType |Hallo-toewijzingsmethode gebruikt voor Hallo particuliere IP-adres (statisch of dynamisch) |
| ipv6PrivateIPAddressType |Hallo toewijzingsmethode gebruikt voor Hallo particuliere IP-adres (dynamisch). IPv6 biedt alleen ondersteuning voor dynamische toewijzing. |
| numberOfInstances |Hallo-nummer van load balanced instanties zijn geïmplementeerd door Hallo-sjabloon |
| ipv4PublicIPAddressName |Hallo DNS-naam die u wilt dat toouse toocommunicate met openbare IPv4-adres Hallo Hallo load balancer opgeven. |
| ipv4PublicIPAddressType |Hallo toewijzingsmethode gebruikt voor Hallo openbaar IP-adres (statisch of dynamisch) |
| Ipv6PublicIPAddressName |Hallo DNS-naam die u wilt dat toouse toocommunicate met openbare IPv6-adres Hallo Hallo load balancer opgeven. |
| ipv6PublicIPAddressType |Hallo toewijzingsmethode voor Hallo openbaar IP-adres (dynamisch). IPv6 biedt alleen ondersteuning voor dynamische toewijzing. |
| lbName |Geef de naam Hallo Hallo load balancer. Deze naam wordt weergegeven in de portal Hallo of gebruikt wanneer tooit met CLI of PowerShell-opdracht wordt verwezen. |

Hallo resterende variabelen in de sjabloon Hallo bevatten afgeleide waarden die worden toegewezen wanneer Azure Hallo bronnen maakt. Deze variabelen niet wijzigen.
