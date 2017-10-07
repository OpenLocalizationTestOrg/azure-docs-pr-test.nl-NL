---
title: aaaAzure Cloud Services-functies Veelgestelde vragen | Microsoft Docs
description: Veelgestelde vragen over Azure Cloud Services. Antwoorden op enkele veelgestelde vragen over certificaten, webrollen en werkrollen.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a>Veelgestelde vragen over Cloud Services
Dit artikel worden enkele veelgestelde vragen over Microsoft Azure Cloud Services. U kunt ook Hallo bezoeken [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) voor algemene Azure-prijzen en -ondersteuning voor informatie. U kunt ook contact opnemen met Hallo [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.

## <a name="certificates"></a>Certificaten
### <a name="where-should-i-install-my-certificate"></a>Waar moet ik mijn certificaat installeren?
* **Mijn**  
  Toepassingscertificaat met persoonlijke sleutel (\*.pfx, \*.p12).
* **CA**  
  Alle tussenliggende certificaten gaat u in dit archief (beleid en Sub-CA's).
* **HOOFDMAP**  
  Hallo basis-CA opslaan, zodat uw belangrijkste basis-CA-certificaat hier moet gaan.

### <a name="i-cant-remove-expired-certificate"></a>Ik kan verlopen certificaat niet verwijderen.
Azure voorkomt u dat u een certificaat verwijderen terwijl deze gebruikt wordt. U moet tooeither Hallo implementatie verwijderen die Hallo certificaat gebruikt of Hallo-update-implementatie met een certificaat verschillende of vernieuwd.

### <a name="delete-an-expired-certificate"></a>Een verlopen certificaat verwijderen
Zolang het Hallo-certificaat niet wordt gebruikt, kunt u Hallo [verwijderen AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove een certificaat.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Ik zijn certificaten met de naam Windows Azure-servicebeheer voor uitbreidingen verlopen
Deze certificaten worden gemaakt wanneer een uitbreiding toohello-cloudservice, zoals Hallo extern bureaublad-extensie wordt toegevoegd. Deze certificaten worden alleen gebruikt voor het versleutelen en ontsleutelen van de persoonlijke configuratie Hallo van Hallo-uitbreiding. Het maakt niet uit als deze certificaten verlopen. Hallo-vervaldatum is niet ingeschakeld.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Certificaten die ik hebt verwijderd terugkomen
Deze terugkomen waarschijnlijk vanwege een hulpprogramma dat u gebruikt, zoals Visual Studio. Wanneer u opnieuw verbinding met een hulpprogramma dat een certificaat gebruikt maken, wordt het geüploade tooAzure opnieuw zijn.

### <a name="my-certificates-keep-disappearing"></a>Mijn certificaten houden verdwijnen
Wanneer er wordt een exemplaar van de virtuele machine Hallo gerecycled, gaan alle lokale wijzigingen verloren. Gebruik een [opstarttaak](cloud-services-startup-tasks.md) tooinstall certificaten toohello virtuele machine elke keer Hallo-rol wordt gestart.

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a>Ik kan mijn beheercertificaten niet vinden in Hallo-portal
[Certificaten voor](../azure-api-management-certs.md) zijn alleen beschikbaar in Hallo klassieke Azure-Portal. Hallo huidige Azure-portal gebruikt geen beheercertificaten. 

### <a name="how-can-i-disable-a-management-certificate"></a>Hoe kan ik een beheercertificaat uitschakelen?
[Certificaten voor](../azure-api-management-certs.md) kan niet worden uitgeschakeld. U verwijderen ze via de klassieke Azure-Portal Hallo wanneer u niet dat ze wilt toobe meer gebruikt.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Hoe maak ik een SSL-certificaat voor een specifiek IP-adres
Volg de aanwijzingen Hallo in Hallo [maken van een zelfstudie certificaat](cloud-services-certs-create.md). Hallo IP-adres gebruiken zoals Hallo DNS-naam.

## <a name="security"></a>Beveiliging
### <a name="disable-ssl-30"></a>SSL 3.0 uitschakelen
toodisable SSL 3.0 en TLS-beveiliging gebruiken, op een opstarttaak maken die wordt beschreven in dit blogbericht: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-tooyour-website"></a>Voeg **nosniff** tooyour website
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

### <a name="customize-iis-for-a-web-role"></a>IIS voor een Webrol aanpassen
Gebruik Hallo IIS opstartscript van Hallo [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.

## <a name="scaling"></a>Schalen
### <a name="i-cannot-scale-beyond-x-instances"></a>Ik kan niet worden uitgebreid dan X exemplaren
Uw Azure-abonnement heeft een limiet op Hallo aantal kernen dat u kunt gebruiken. Schalen werkt niet als u alle Hallo kernen beschikbaar hebt gebruikt. Bijvoorbeeld, als er een limiet van 100 kernen, betekent dit dat u exemplaren van de virtuele machine 100 A1 grootte voor de cloudservice kunnen hebben, of 50 A2 grootte exemplaren van de virtuele machine.

## <a name="networking"></a>Netwerken
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Ik kan niet worden gereserveerd een IP-adres in een cloudservice meerdere VIP 's
Controleer eerst of de instantie van die Hallo-virtuele machine die u probeert tooreserve Hallo IP voor is ingeschakeld. Controleer vervolgens of dat u gereserveerde IP-adressen voor bAndere Hallo fasering en productie-implementaties. **Geen** Hallo-instellingen niet wijzigen terwijl het Hallo-implementatie worden geüpgraded.

## <a name="remote-desktop"></a>Extern bureaublad
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Hoe kan ik extern bureaublad wanneer ik een NSG hebben?
Voeg regels toohello NSG waarmee verkeer op poorten **3389** en **20000**.  Extern bureaublad maakt gebruik van poort **3389**.  Cloud Service-exemplaren worden verdeeld, zodat u niet rechtstreeks welke tooconnect exemplaar om te controleren.  Hallo *RemoteForwarder* en *RemoteAccess* agents beheren van RDP-verkeer en Hallo client toosend een RDP-cookie toestaan en opgeven van een afzonderlijke instantie tooconnect aan.  Hallo *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000*** worden geopend die worden geblokkeerd als er een NSG.
