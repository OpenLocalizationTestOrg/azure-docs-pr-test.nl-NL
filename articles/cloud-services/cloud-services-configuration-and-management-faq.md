---
title: Configureren en beheren van problemen voor veelgestelde vragen over Microsoft Azure Cloud Services | Microsoft Docs
description: Dit artikel worden de veelgestelde vragen over het configureren en beheren voor Microsoft Azure Cloud Services.
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
ms.openlocfilehash: 42b5d2947df92b4486fe149d046168208083dde2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="configuration-and-management-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Configureren en beheren van problemen voor Azure Cloud Services: veelgestelde vragen (FAQ's)

Dit artikel bevat veelgestelde vragen over het configureren en beheren van problemen voor [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). U kunt ook raadpleegt u de [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="how-do-i-add-nosniff-to-my-website"></a>Hoe kan ik 'nosniff' naar mijn website toevoegen
Voeg een instelling in om te voorkomen dat clients de MIME-typen voor het bewaken van netwerken voor uw *web.config* bestand.

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

U kunt dit ook toevoegen als een instelling in IIS. Gebruik de volgende opdracht met de [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

## <a name="how-do-i-customize-iis-for-a-web-role"></a>Hoe pas IIS voor een Webrol?
Het script voor het opstarten van IIS uit de [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.

## <a name="i-cannot-scale-beyond-x-instances"></a>Ik kan niet worden uitgebreid dan X exemplaren
Uw Azure-abonnement heeft een limiet van het aantal kernen dat u kunt gebruiken. Schalen werkt niet als u de beschikbare kernen hebt gebruikt. Bijvoorbeeld, als er een limiet van 100 kernen, betekent dit dat u exemplaren van de virtuele machine 100 A1 grootte voor de cloudservice kunnen hebben, of 50 A2 grootte exemplaren van de virtuele machine.

## <a name="how-can-i-implement-role-based-access-for-cloud-services"></a>Hoe implementeer ik toegang op basis van rollen voor Cloudservices
Cloud-Services biedt geen ondersteuning voor het model op rollen gebaseerde toegangsbeheer (RBAC), omdat dit geen een op basis van Azure Resource Manager-service.

Zie [Azure RBAC versus klassieke abonnementbeheerders](../active-directory/role-based-access-control-what-is.md#azure-rbac-vs-classic-subscription-administrators).

## <a name="how-do-i-set-the-idle-timeout-for-azure-load-balancer"></a>Hoe stel de time-out voor inactiviteit voor Azure load balancer?
U kunt de time-out opgeven in uw programma servicedefinitiebestand (csdef) als volgt:

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

## <a name="can-microsoft-internal-engineers-rdp-to-cloud-service-instances-without-permission"></a>Kan Microsoft interne engineers RDP naar cloud service-exemplaren zonder toestemming?
Microsoft volgt een strikte proces dat niet toe interne engineers voor RDP in uw cloudservice zonder schriftelijke toestemming (e-mailadres of andere geschreven communicatie dat staat) uit de eigenaar of de door hun benoemde persoon.

## <a name="why-is-the-certificate-chain-of-my-cloud-service-ssl-certificate-incomplete"></a>Waarom is de certificaatketen van mijn SSL-certificaat van cloud-service onvolledig?
Het is raadzaam om de volledige certificaatketen (leaf-certificaat, tussenliggende certificaten en hoofdmap cert) in plaats van het leaf-certificaat te installeren. Wanneer u het leaf-certificaat installeert, wordt u op Windows de certificaatketen bouwen door roulatie van de CTL vertrouwen. Als onregelmatige netwerk- of DNS-problemen in Azure of Windows Update optreden wanneer Windows probeert het certificaat te valideren, kan het certificaat ongeldig worden beschouwd. Als u de volledige certificaatketen installeert, kunt u dit probleem voorkomen. Het blog op [een keten SSL-certificaat installeren](https://blogs.msdn.microsoft.com/azuredevsupport/2010/02/24/how-to-install-a-chained-ssl-certificate/) ziet u hoe u dit doet.

## <a name="how-do-i-associate-a-static-ip-address-to-my-cloud-service"></a>Hoe koppel ik een statisch IP-adres naar Mijn cloudservice
Als u een statisch IP-adres instelt, moet u een gereserveerde IP-adres maken. Dit gereserveerde IP-adres kan worden gekoppeld aan een nieuwe cloudservice of aan een bestaande implementatie. Zie de volgende documenten voor meer informatie:
* [Het maken van een gereserveerd IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md#manage-reserved-vips)
* [Het IP-adres van een bestaande cloudservice reserveren](../virtual-network/virtual-networks-reserved-public-ip.md#reserve-the-ip-address-of-an-existing-cloud-service)
* [Koppelen van een gereserveerd IP-adres op een nieuwe cloudservice](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-new-cloud-service)
* [Koppelen van een gereserveerd IP-adres aan een actieve implementatie](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-running-deployment)
* [Koppelen van een gereserveerd IP-adres op een cloudservice met behulp van een service-configuratiebestand](../virtual-network/virtual-networks-reserved-public-ip.md#associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file)

## <a name="what-is-the-quota-limit-for-my-cloud-service"></a>Wat is de quotalimiet voor mijn cloudservice?
Zie [servicespecifieke beperkt](../azure-subscription-service-limits.md#subscription-limits).

## <a name="why-does-the-drive-on-my-cloud-service-vm-show-very-little-free-disk-space"></a>Waarom wordt het station van mijn cloudservice-VM weinig vrije schijfruimte weergegeven?
Dit is verwacht gedrag en mag niet een probleem voor uw toepassing leiden. Logboekregistratie is ingeschakeld voor de % echt % station in Azure PaaS-virtuele machines, die in wezen verbruikt dubbele de hoeveelheid schijfruimte die bestanden wordt normaal gesproken in beslag nemen. Er zijn echter enkele dingen te weten dat in wezen kunt u deze uitschakelen in een niet-probleem.

De schijfgrootte % approot % als < grootte van .cspkg + maximale logboekgrootte > + marge vrije ruimte wordt berekend of 1,5 GB, afhankelijk van wat is groter. De grootte van uw virtuele machine heeft geen gevolgen voor deze berekening. (De VM-grootte geldt alleen voor de grootte van het tijdelijke station C:.) 

Dit wordt niet ondersteund voor het schrijven naar het station % approot %. Als u naar de virtuele machine van Azure schrijft, moet u doen in een tijdelijke LocalStorage resource (of een andere optie, zoals de Blob-opslag, Azure-bestanden, enz.). De hoeveelheid vrije ruimte op de map % approot % is dus niet relevant. Als u niet zeker weet of uw toepassing naar het station van de approot schrijft, kunt u altijd gebruiken om uw service een paar dagen uitvoeren en vergelijk de "voor" en "na' grootten. 

Azure wordt niet schrijven naar het station % approot %. Als de VHD is gemaakt op basis van uw .cspkg en in de Azure VM gekoppeld, is het enige dat dat naar dit station kan schrijven uw toepassing. 

De wijzigingslogboek-instellingen zijn niet-configureerbare, zodat u niet uitschakelen.

## <a name="what-are-the-features-and-capabilities-that-azure-basic-ipsids-and-ddos-provides"></a>Wat zijn de functies en mogelijkheden die Azure basic IP-Adressen/id's en DDOS biedt?
Azure heeft IP-Adressen/id's in het datacenter fysieke servers om te beschermen tegen bedreigingen. Klanten kunnen bovendien beveiligingsoplossingen voor de van derden, zoals web application firewalls, netwerkfirewalls anti-malware, inbraakdetectie, preventie systemen (id's / IP-Adressen) en meer implementeren. Zie voor meer informatie [beveiligen van uw gegevens en activa en voldoen aan de globale beveiligingsstandaarden](https://www.microsoft.com/en-us/trustcenter/Security/AzureSecurity).

Microsoft controleert doorlopend servers, netwerken en toepassingen voor het detecteren van bedreigingen. Azure multipronged threat-management benadering gebruikt inbraakdetectie, gedistribueerde denial-of-service (DDoS) aanvallen voorkomen, binnendringen testen, gebruikersgedrag analytics, afwijkingsdetectie en machine learning-om voortdurend de beveiliging te versterken en risico's te verminderen. Microsoft Antimalware voor Azure beveiligt Azure-cloudservices en virtuele machines. U hebt de optie voor het implementeren van oplossingen van derden bovendien zoals web application fire wanden netwerkfirewalls, anti-malware, inbraakdetectie detectie en preventie van systemen (id's / IP-Adressen) en meer.

## <a name="why-does-iis-stop-writing-to-the-log-directory"></a>Waarom stopt IIS schrijven naar de logboekmap?
Het quotum voor lokale opslag voor het schrijven naar de logboekmap is verbruikt. Om dit te corrigeren, kunt u een van drie dingen doen:
* Diagnostische gegevens inschakelen voor IIS en de diagnostische gegevens periodiek wordt verplaatst naar de blob storage.
* Logboekbestanden handmatig verwijderen uit de map voor logboekregistratie.
* Verhoog de quotalimiet voor lokale bronnen.

Zie de volgende documenten voor meer informatie:
* [Diagnostische gegevens opslaan en weergeven in Azure Storage](cloud-services-dotnet-diagnostics-storage.md)
* [IIS-logboeken stopt met het schrijven in de cloudservice](https://blogs.msdn.microsoft.com/cie/2013/12/21/iis-logs-stops-writing-in-cloud-service/)

## <a name="what-is-the-purpose-of-the-windows-azure-tools-encryption-certificate-for-extensions"></a>Wat is het doel van de 'Windows Azure hulpprogramma's voor versleuteling voor certificaatuitbreidingen'?
Deze certificaten worden automatisch gemaakt wanneer er wordt een extensie toegevoegd aan de cloudservice. Meestal betreft dit is de extensie af of de RDP-uitbreiding, maar het anderen, zoals de extensie Antimalware of Logboekverzamelaar mogelijk. Deze certificaten worden alleen gebruikt voor het versleutelen en ontsleutelen van de persoonlijke configuratie voor de extensie. De verloopdatum wordt nooit gecontroleerd, het maakt niet uit als het certificaat is verlopen. 

U kunt deze certificaten negeren. Als u wilt om de certificaten op te schonen, kunt u proberen deze alle worden verwijderd. Azure genereert een fout als u probeert te verwijderen van een certificaat dat wordt gebruikt.

## <a name="how-can-i-generate-a-certificate-signing-request-csr-without-rdp-ing-in-to-the-instance"></a>Hoe kan ik een Certificate Signing Request (CSR) zonder 'RDP-ing' met het exemplaar genereren?
Zie de volgende richtlijnen-document:

>[Verkrijgen van een certificaat voor gebruik met Windows Azure websites (WAWS)](https://azure.microsoft.com/blog/obtaining-a-certificate-for-use-with-windows-azure-web-sites-waws/)

Houd er rekening mee dat een certificaataanvraag een tekstbestand is. Dit hoeft niet te worden gemaakt van de machine waarop het certificaat uiteindelijk zal worden gebruikt. Hoewel dit document is geschreven voor een App Service, wordt het maken van de CSR is algemeen en geldt ook voor Cloud-Services.
