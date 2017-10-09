---
title: aaaProtect persoonlijke gegevens die onderweg met versleuteling in Azure | Microsoft Docs
description: Met behulp van versleuteling in Azure tooprotect persoonlijke gegevens
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 218ad3f49326e8dec299a6d92b18116da65eae71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-in-transit-with-encryption"></a>Azure versleutelingstechnologieën: beveiligen van persoonlijke gegevens die onderweg met versleuteling

In dit artikel helpt u begrijpen en gebruiken van Azure versleuteling technologieën toosecure gegevens onderweg. 

Beschermen Hallo privacy van persoonlijke gegevens is als ze via Hallo-netwerk een essentieel onderdeel van een meerlaagse defense-in-depth beveiligingsstrategie. Versleuteling onderweg is ontworpen tooprevent een aanvaller die gegevensoverdrachten kunnen tooview of gebruik Hallo gegevens wordt onderschept.

## <a name="scenario"></a>Scenario

Een grote cruise bedrijf, gevestigd in Hallo Verenigde Staten, wordt de bewerkingen toooffer routes in Hallo Middellandse, Adriatische, Baltische veiligheid ook Hallo Florida uitbreiden. toosupport deze inspanningen, heeft deze meerdere kleinere cruise regels op basis van Italië, verkregen Duitsland, Denemarken en Hallo Verenigd Koninkrijk 

Hallo bedrijf maakt gebruik van Microsoft Azure toostore bedrijfsgegevens Hallo cloud. Dit omvat persoonlijk gegevens zoals namen, adressen, telefoonnummers en creditcardgegevens van globale klantendatabase. Dit omvat ook traditionele Human Resource informatie zoals adressen, telefoonnummers, BTW-id's en medische informatie over de werknemers van het bedrijf op alle locaties. Hallo cruise regel onderhoudt ook een grote database van derden en loyaliteit voor leden die persoonlijke gegevens tootrack relaties met de huidige en eerdere klanten bevat.

Persoonlijke gegevens van klanten wordt ingevoerd in de database Hallo uit van het bedrijf Hallo externe kantoren en reizen agents zich Hallo wereld. Documenten met klantgegevens overgebracht over Hallo tooAzure netwerkopslag.

## <a name="problem-statement"></a>Probleemformulering

Hallo bedrijf dient Hallo privacy van klanten te beschermen en persoonlijke gegevens van de werknemers terwijl het onderweg tooand van Azure-services is.

## <a name="company-goal"></a>Bedrijf-doel

Hallo bedrijf doel tooensure dat persoonlijke gegevens van de harde schijf worden versleuteld. Als niet-geautoriseerde personen Hallo uitschakelen schijf persoonlijke gegevens Intercept, moet deze in een formulier dat het onleesbaar verschijnt. Versleuteling toepassen, moet eenvoudig of volledig transparant voor gebruikers en beheerders.

## <a name="solutions"></a>Oplossingen

Azure-services bieden meerdere hulpprogramma's en technologieën toohelp beveiligen van persoonlijke gegevens die onderweg.

### <a name="azure-storage"></a>Azure Storage

Gegevens die zijn opgeslagen in de cloud Hallo moet getransporteerd van Hallo-client, die zich fysiek bevinden overal op kan Hallo wereld, toohello Azure-Datacenter. Wanneer er gegevens worden opgehaald door gebruikers, overdracht opnieuw in Hallo tegengestelde richting. Gegevens die onderweg via Hallo openbare Internet is altijd risico worden onderschept door kwaadwillende personen. Het is belangrijk tooprotect Hallo privacy van persoonlijke gegevens met behulp van versleuteling transportniveau toosecure zoals deze tussen locaties verplaatst.

Hallo HTTPS-protocol biedt een kanaal beveiligde, gecodeerde communicatie via Internet Hallo. HTTPS moet gebruikte tooaccess objecten in Azure Storage en bij het aanroepen van REST-API's. U gebruik van HTTPS-protocol Hallo afdwingen wanneer u [Shared Access Signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) (SAS) toodelegate access tooAzure opslag-objecten. Er zijn twee soorten SAS: Service-SAS en Account-SAS.

#### <a name="how-do-i-construct-a-service-sas"></a>Hoe ik een Service-SAS maken?

Een Service-SAS gemachtigden toegang tooa resource in slechts één van de opslagservices hello (blob, queue, tabel of file-service). een Service-SAS tooconstruct Hallo te volgen:

1. Hallo ondertekend Versieveld opgeven

2. Geef Hallo ondertekend Resource (Blob en alleen File-Service)

3. Geef de queryparameters tooOverride antwoordheaders (Blob-Service en alleen File-Service)

4. Geef Hallo tabelnaam (alleen tabel-Service)

5. Hallo toegangsbeleid opgeven

6. Hallo handtekening geldigheidsinterval opgeven

8. Machtigingen opgeven

9. IP-adres of IP-bereik opgeven

10. Hallo HTTP-Protocol opgeven

11. Tabel toegang adresbereiken opgeven

12. Hallo ondertekend-id opgeven

13. Hallo handtekening opgeven

Zie voor meer instructies, [samenstellen van een Service-SAS](https://docs.microsoft.com/rest/api/storageservices/Constructing-a-Service-SAS?redirectedfrom=MSDN).

#### <a name="how-do-i-construct-an-account-sas"></a>Hoe ik een SAS-Account maken?

Een Account-SAS delegeert toegang tooresources in een of meer van de opslagservices Hallo. U kunt ook toegang tooread-, schrijf- en delete-bewerkingen op de blob-containers, tabellen, wachtrijen en bestandsshares die niet zijn toegestaan als een service-SAS delegeren. Bouw van een SAS-Account is vergelijkbaar toothat van een Service-SAS. Zie voor gedetailleerde instructies [samenstellen van een SAS-Account.](https://docs.microsoft.com/rest/api/storageservices/Constructing-an-Account-SAS?redirectedfrom=MSDN)

#### <a name="how-do-i-enforce-https-when-calling-rest-apis"></a>Hoe ik HTTPS afdwingen bij het aanroepen van REST-API's?

tooenforce hello gebruik van HTTPS bij het aanroepen van REST-API's tooaccess objecten in de storage-accounts, kunt u beveiligde overdracht vereist voor het Hallo-opslagaccount. 

1. Selecteer in de Azure-portal Hallo, **Storage-Account maken**, of Selecteer voor een bestaand opslagaccount **instellingen** en vervolgens **configuratie**.

2. Onder **beveiligde overdracht vereist**, selecteer **ingeschakeld**.

![Een opslagaccount maken](media/protect-personal-data-in-transit-encryption/create-storage-account.png)

Voor instructies gedetailleerde, inclusief hoe tooenable beveiligde overdracht vereist via een programma, Zie [vereisen Secure Transfer](https://docs.microsoft.com/azure/storage/storage-require-secure-transfer).

#### <a name="how-do-i-encrypt-data-in-azure-file-storage"></a>Versleutelen gegevens in Azure File Storage?

gegevens die onderweg met tooencrypt [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-file-how-to-use-files-portal), kunt u SMB 3.x met Windows 8, 8.1 en 10 en Windows Server 2012 R2 en Windows Server 2016. Wanneer u hello Azure Files service gebruikt, wordt een verbinding zonder versleuteling mislukt wanneer "Veilig vereiste gegevensoverdracht" is ingeschakeld. Dit geldt ook voor scenario's die gebruikmaken van SMB 2.1, SMB 3.0 zonder versleuteling en bepaalde versies van het Hallo Linux SMB-client.

#### <a name="azure-client-side-encryption"></a>Azure-Client-side '-versleuteling

Een andere optie voor het beveiligen van persoonlijke gegevens, terwijl deze wordt overgebracht tussen een client-toepassing en een Azure Storage is [clientzijde versleuteling](https://docs.microsoft.com/azure/storage/storage-client-side-encryption). Hallo-gegevens worden versleuteld voordat ze worden overgedragen naar de Azure-opslag en wanneer u de Hallo-gegevens uit Azure Storage ophalen, Hallo gegevens worden ontsleuteld nadat het is ontvangen op Hallo-client.

### <a name="azure-site-to-site-vpn"></a>Azure Site-naar-Site-VPN

Een effectieve manier tooprotect persoonlijke gegevens onderweg tussen een bedrijfsnetwerk of de gebruiker en het Hallo virtuele Azure-netwerk is toouse een [site-naar-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal) of [punt-naar-site](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal) virtuele particuliere netwerk (VPN). Een VPN-verbinding wordt gemaakt van een beveiligde tunnel versleutelde via Internet Hallo.

#### <a name="how-do-i-create-a-site-to-site-vpn-connection"></a>Hoe maak ik een site-naar-site VPN-verbinding

Een site-naar-site-VPN-verbinding maakt meerdere gebruikers op Hallo bedrijfsnetwerk tooAzure. een site-naar-site-verbinding in hello Azure-portal toocreate Hallo te volgen:

1. Een virtueel netwerk maken.

2. Geef een DNS-server.

3. Hallo gatewaysubnet maken.

4. Hallo VPN-gateway maken. 

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-01.png)

5. Hallo lokale netwerkgateway maken.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-02.png)

6. Configureer het VPN-apparaat.

7. Hallo VPN-verbinding maken.

    ![](media/protect-personal-data-in-transit-encryption/vpn-step-03.png)

8. Hallo VPN-verbinding controleren.

Voor gedetailleerde instructies over hoe toocreate een site-naar-site-verbinding in hello Azure portal, Zie [maken van een Site-naar-Site-verbinding in hello Azure-Portal.] (https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)

#### <a name="how-do-i-create-a-point-to-site-vpn-connection"></a>Hoe maak ik een punt-naar-site VPN-verbinding

Een punt-naar-Site VPN maakt een beveiligde verbinding van een individuele client computer tooa virtueel netwerk. Dit is handig als u tooconnect tooAzure vanaf een externe locatie, zoals vanaf thuis of een hotel of conferentie center. toocreate een punt-naar-site-verbinding in hello Azure-portal

1. Een virtueel netwerk maken.

2. Voeg een gatewaysubnet.

3. Geef een DNS-server. (optioneel)

4. Maak een virtuele netwerkgateway.

5. Genereren van certificaten.

6. Hallo-clientadresgroep toevoegen.

7. Hallo root certificate openbaar certificaatgegevens uploaden.

8. Genereren en Hallo VPN-clientpakket configuratie installeren.

9. Een geëxporteerde certificaat installeren.

10. Verbinding maken met tooAzure.

11. Controleer de verbinding.

Zie voor meer instructies, [een punt-naar-Site-verbinding tooa VNet configureren met behulp van verificatie via certificaat: Azure Portal.](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)

### <a name="ssltls"></a>SSL/TLS

Microsoft raadt aan dat u altijd SSL/TLS-protocollen tooexchange gegevens op verschillende locaties gebruiken. Organisaties die ervoor toouse kiezen [ExpressRoute](https://docs.microsoft.com/azure/expressroute/) toomove grote gegevenssets toegewezen snelle WAN-koppeling kunt Hallo gegevens op Hallo op toepassingsniveau met SSL/TLS- of andere protocollen voor extra beveiliging ook versleutelen.

### <a name="encryption-by-default"></a>Codering standaard

Microsoft gebruikt codering tooprotect gegevens onderweg tussen klanten en Azure-cloudservices. Als u met Azure Storage via hello Azure Portal communiceert, worden alle transacties plaatsvinden via HTTPS.

[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security) (TLS) is dat Microsoft-datacenters toonegotiate met clientsystemen die verbinding met cloudservices tooMicrosoft zal proberen Hallo-protocol. TLS bevat sterke verificatie, privacy van berichten en integriteit (schakelt u het detecteren van bericht knoeien, onderschept en kunnen worden vervalst), interoperabiliteit, algoritmeflexibiliteit, gebruiksgemak en gebruik.

[Perfect Forward Secrecy](https://en.wikipedia.org/wiki/Forward_secrecy) (PFS) wordt ook gebruikt zodat elke verbinding tussen clientsystemen klanten en cloudservices van Microsoft gebruiken unieke sleutels. Verbindingen tooMicrosoft cloudservices ook te profiteren van op basis van RSA 2048-bits versleuteling sleutellengten. Hallo combinatie van TLS, sleutellengtes RSA 2048-bits, en PFS maakt het moeilijker voor iemand toointercept en toegang tot gegevens die onderweg tussen Microsoft-cloudservices en -klanten.

Gegevens die onderweg is altijd versleuteld in [Data Lake Store] (https://docs.microsoft.com/azure/data-lake-store/data-lake-store-security-overview). Bovendien tooencrypting gegevens voorafgaande toostoring toopersistent media Hallo gegevens is ook altijd onderweg via HTTPS beveiligd. HTTPS is alleen Hallo-protocol dat wordt ondersteund voor Hallo die Data Lake Store REST-interfaces.

## <a name="summary"></a>Samenvatting

Hallo bedrijf kan het doel van persoonlijke gegevens en Hallo privacy van dergelijke gegevens beveiligen met HTTPS-verbindingen tooAzure opslag afdwingen, met behulp van handtekeningen voor gedeelde toegang en inschakelen van beveiligde overdracht vereist op Hallo storage-accounts kunt uitvoeren. Ze kunnen ook persoonlijke gegevens beveiligen met behulp van SMB 3.0-verbindingen en clientzijde codering implementeren. Site-naar-site VPN-verbindingen van Hallo bedrijfsnetwerk toohello virtuele Azure-netwerk en punt-naar-site VPN-verbindingen van afzonderlijke gebruikers maakt een beveiligde tunnel via welke persoonlijke gegevens kan veilig worden verzonden. Microsoft standaard versleuteling procedures nog beter beschermd Hallo privacy van persoonlijke gegevens.

## <a name="next-steps"></a>Volgende stappen

- [Best Practices voor beveiliging van gegevens van Azure en versleuteling](https://docs.microsoft.com/azure/security/azure-security-data-encryption-best-practices)

- [Planning en ontwerp voor VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design)

- [Veelgestelde vragen VPN Gateway](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-vpn-faq)

- [Kopen en configureren van een SSL-certificaat voor uw Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-purchase-ssl-web-site)
