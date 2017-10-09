---
title: problemen met aaaConfiguration en beheer voor veelgestelde vragen over Microsoft Azure Cloud Services | Microsoft Docs
description: Dit artikel worden Hallo Veelgestelde vragen over het configureren en beheren voor Microsoft Azure Cloud Services.
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 62ece142ac0ef5d45081cab333375b1a0a8f0ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Configureren en beheren van problemen voor Azure Cloud Services: veelgestelde vragen (FAQ's)

Dit artikel bevat veelgestelde vragen over het configureren en beheren van problemen voor [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). U kunt ook contact opnemen met Hallo [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-toomy-website"></a>Hoe kan ik 'nosniff' toomy website toevoegen
tooprevent-clients vanuit het bekijken van MIME-typen zijn hello, Voeg een instelling in uw *web.config* bestand.

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

U kunt dit ook toevoegen als een instelling in IIS. Gebruik Hallo volgende opdracht Hello [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a>Hoe pas IIS voor een Webrol?
Gebruik Hallo IIS opstartscript van Hallo [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.

## <a name="i-cannot-scale-beyond-x-instances"></a>Ik kan niet worden uitgebreid dan X exemplaren
Uw Azure-abonnement heeft een limiet op Hallo aantal kernen dat u kunt gebruiken. Schalen werkt niet als u alle Hallo kernen beschikbaar hebt gebruikt. Bijvoorbeeld, als er een limiet van 100 kernen, betekent dit dat u exemplaren van de virtuele machine 100 A1 grootte voor de cloudservice kunnen hebben, of 50 A2 grootte exemplaren van de virtuele machine.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Hoe implementeer ik toegang op basis van rollen voor Cloudservices
Cloud-Services biedt geen ondersteuning voor Hallo op rollen gebaseerde toegangsbeheer (RBAC)-model, omdat dit geen een op basis van Azure Resource Manager-service.

Zie [Azure RBAC versus klassieke abonnementbeheerders](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-hello-idle-timeout-for-azure-load-balancer"></a>Hoe stel ik Hallo inactiviteit voor Azure load balancer
U kunt Hallo time-out opgeven in uw programma servicedefinitiebestand (csdef) als volgt:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="mgVS2015Worker" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2015-04.2.6">
  <WorkerRole name="WorkerRole1" vmsize="Small">
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10100"   idleTimeoutInMinutes="30" />
    </Endpoints>
  </WorkerRole>
```
Zie [nieuw: configureerbare Idle Timeout voor Azure Load Balancer](https://azure.microsoft.com/blog/new-configurable-idle-timeout-for-azure-load-balancer/) voor meer informatie.

## <a name="can-microsoft-internal-engineers-rdp-toocloud-service-instances-without-permission"></a>Kan Microsoft interne engineers RDP toocloud service-exemplaren zonder toestemming?
Microsoft volgt een strikte proces waarmee geen interne supporttechnici tooRDP in uw cloudservice zonder schriftelijke toestemming (e-mailadres of andere geschreven communicatie) van Hallo eigenaar of de door hun benoemde persoon.

## <a name="why-is-hello-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Waarom is de certificaatketen Hallo van mijn SSL-certificaat van cloud-service onvolledig?
We raden klanten Hallo volledige certificaatketen (leaf-certificaat, tussenliggende certificaten en hoofdmap cert) in plaats van alleen Hallo leaf-certificaat installeren. Wanneer u alleen Hallo leaf certificaat installeert, wordt u door het Hallo CTL roulatie afgaan op Windows toobuild Hallo certificaatketen. Als onregelmatige netwerk- of DNS-problemen in Azure of Windows Update optreden wanneer Windows toovalidate Hallo certificaat probeert, kan Hallo certificaat ongeldig worden beschouwd. Als u de volledige certificaatketen Hallo installeert, kunt u dit probleem voorkomen. blog op Hallo [hoe tooinstall een keten SSL-certificaat](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) ziet u hoe toodo dit.

## <a name="how-do-i-associate-a-static-ip-address-toomy-cloud-service"></a>Hoe ik een statische IP-adres toomy cloudservice koppelen?
tooset een statische IP-adres, moet u toocreate een gereserveerde IP-adres. Dit gereserveerde IP-adres kan worden gekoppeld tooa nieuwe cloud service of tooan bestaande implementatie. Hallo volgende documenten voor meer informatie Zie:
* [Hoe toocreate een gereserveerd IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Reserveer Hallo IP-adres van een bestaande cloudservice](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Koppelen van een gereserveerd IP-tooa nieuwe cloudservice](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Koppelen van een gereserveerd IP-tooa waarop implementatie wordt uitgevoerd](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Een gereserveerd IP-tooa cloudservice koppelen via een configuratiebestand voor de service](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-hello-quota-limit-for-my-cloud-service"></a>Wat is de quotalimiet Hallo voor mijn cloudservice?
Zie [servicespecifieke beperkt](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-hello-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>Waarom wordt Hallo station op mijn cloudservice-VM weinig vrije schijfruimte weergegeven?
Dit is verwacht gedrag en mag niet een probleem tooyour toepassing leiden. Logboekregistratie is ingeschakeld voor % Hallo echt % station in Azure PaaS-virtuele machines, die in wezen verbruikt dubbele Hallo hoeveelheid schijfruimte die bestanden wordt normaal gesproken in beslag nemen. Maar er zijn verschillende dingen toobe rekening houden met die in wezen dit inschakelen in een niet-probleem.

Hallo % approot % schijfgrootte berekend als < grootte van .cspkg + maximale logboekgrootte > + marge vrije schijfruimte, of 1,5 GB, afhankelijk van wat is groter. Hallo-grootte van uw virtuele machine heeft geen gevolgen voor deze berekening. (VM-grootte Hallo alleen van invloed op Hallo-grootte van het station voor tijdelijke C: Hallo.) 

Is het niet-ondersteunde toowrite toohello % approot % station. Als u Azure VM toohello schrijft, moet u doen in een tijdelijke LocalStorage resource (of een andere optie, zoals de Blob-opslag, Azure-bestanden, enz.). Hallo en de hoeveelheid vrije schijfruimte op Hallo % approot % de map is dus niet relevant. Als u niet zeker weet of uw toepassing toohello % approot % station wordt geschreven, kunt u altijd uw service uitvoeren voor een paar dagen en vervolgens vergelijken Hallo "voor" en "na' grootten. 

Azure worden geschreven iets toohello % approot % station. Zodra hello VHD is gemaakt op basis van uw .cspkg en gekoppeld in hello Azure VM, heeft Hallo dat toothis station kan schrijven alleen uw toepassing. 

Hallo journaalinstellingen zijn niet-configureerbare, zodat u niet uitschakelen.

## <a name="what-are-hello-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Wat zijn Hallo functies en mogelijkheden die Azure basic IP-Adressen/id's en DDOS biedt?
Azure heeft IP-Adressen/id's in het datacenter fysieke servers toodefend tegen bedreigingen. Klanten kunnen bovendien beveiligingsoplossingen voor de van derden, zoals web application firewalls, netwerkfirewalls anti-malware, inbraakdetectie, preventie systemen (id's / IP-Adressen) en meer implementeren. Zie voor meer informatie [beveiligen van uw gegevens en activa en voldoen aan de globale beveiligingsstandaarden](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).

Microsoft controleert doorlopend toodetect bedreigingen voor servers, netwerken en toepassingen. Azure multipronged threat-management benadering wordt inbraakdetectie, gedistribueerde denial-of-service (DDoS) aanvallen te voorkomen, binnendringen testen, gedragsanalyse, afwijkingsdetectie en machine learning tooconstantly versterken de verdediging en risico's verminderen. Microsoft Antimalware voor Azure beveiligt Azure-cloudservices en virtuele machines. U hebt Hallo optie toodeploy van derden beveiligingsoplossingen bovendien zoals web application fire wanden netwerkfirewalls, anti-malware, inbraakdetectie detectie en preventie van systemen (id's / IP-Adressen) en meer.

## <a name="why-does-iis-stop-writing-toohello-log-directory"></a>Waarom stopt IIS toohello logboekmap schrijven?
Hallo lokale opslagquotum voor het schrijven van toohello logboekmap is verbruikt. Om dit te corrigeren, kunt u een van drie dingen doen:
* Diagnostische gegevens inschakelen voor IIS en Hallo diagnostische gegevens periodiek verplaatst tooblob opslag hebben.
* Verwijder handmatig de logboekbestanden van Hallo directory logboekregistratie.
* Verhoog de quotalimiet voor lokale bronnen.

Zie voor meer informatie Hallo documenten te volgen:
* [Diagnostische gegevens opslaan en weergeven in Azure Storage](cloud-services-dotnet-diagnostics-storage.md)
* [IIS-logboeken stopt met het schrijven in de cloudservice](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-hello-purpose-of-hello-windows-azure-tools-encryption-certificate-for-extensions"></a>Wat is Hallo doel van 'Windows Azure hulpprogramma's voor versleuteling voor certificaatuitbreidingen' Hallo?
Deze certificaten worden automatisch gemaakt wanneer een uitbreiding toohello-cloudservice wordt toegevoegd. Meestal betreft dit Hallo af extensie of Hallo RDP-extensie is, maar wordt anderen, zoals Hallo Antimalware of Logboekverzamelaar-extensie. Deze certificaten worden alleen gebruikt voor het versleutelen en ontsleutelen van Hallo persoonlijke configuratie voor Hallo-extensie. Hallo-vervaldatum is nooit ingeschakeld, zodat het maakt niet uit als Hallo-certificaat is verlopen. 

U kunt deze certificaten negeren. Als u opruimen Hallo certificaten wilt, kunt u proberen deze alle worden verwijderd. Azure genereert een fout als u toodelete probeert een certificaat dat wordt gebruikt.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-toohello-instance"></a>Hoe kan ik een Certificate Signing Request (CSR) zonder 'RDP-ing' in toohello exemplaar genereren?
Zie Hallo document richtlijnen te volgen:

>[Verkrijgen van een certificaat voor gebruik met Windows Azure websites (WAWS)](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

Houd er rekening mee dat een certificaataanvraag een tekstbestand is. Dit heeft geen toobe gemaakt op basis van het Hallo-machine waarop Hallo certificaat uiteindelijk zal worden gebruikt. Hoewel dit document is geschreven voor een App Service, Hallo CSR maken is algemeen en geldt ook voor Cloud-Services.
