---
title: Azure Cloud Services-functies Veelgestelde vragen | Microsoft Docs
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
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a>Veelgestelde vragen over Cloud Services
Dit artikel worden enkele veelgestelde vragen over Microsoft Azure Cloud Services. U kunt ook de [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) voor algemene Azure-prijzen en -ondersteuning voor informatie. U kunt ook raadpleegt u de [VM-grootte voor Cloud Services-pagina](cloud-services-sizes-specs.md) voor informatie over de grootte.

## <a name="certificates"></a>Certificaten
### <a name="where-should-i-install-my-certificate"></a>Waar moet ik mijn certificaat installeren?
* **Mijn**  
  Toepassingscertificaat met persoonlijke sleutel (\*.pfx, \*.p12).
* **CA**  
  Alle tussenliggende certificaten gaat u in dit archief (beleid en Sub-CA's).
* **HOOFDMAP**  
  De basis-CA opslaan, zodat uw belangrijkste basis-CA-certificaat hier moet gaan.

### <a name="i-cant-remove-expired-certificate"></a>Ik kan verlopen certificaat niet verwijderen.
Azure voorkomt u dat u een certificaat verwijderen terwijl deze gebruikt wordt. U moet aan de implementatie die gebruikmaakt van het certificaat te verwijderen of bijwerken van de implementatie met een andere of vernieuwd certificaat.

### <a name="delete-an-expired-certificate"></a>Een verlopen certificaat verwijderen
Zolang het certificaat niet gebruikt wordt, kunt u de [verwijderen AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell-cmdlet om te verwijderen van een certificaat.

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a>Ik zijn certificaten met de naam Windows Azure-servicebeheer voor uitbreidingen verlopen
Deze certificaten worden gemaakt wanneer een uitbreiding wordt toegevoegd aan de cloudservice, zoals de extern bureaublad-extensie. Deze certificaten worden alleen gebruikt voor het versleutelen en ontsleutelen van de persoonlijke configuratie van de extensie. Het maakt niet uit als deze certificaten verlopen. De verloopdatum is niet ingeschakeld.

### <a name="certificates-i-have-deleted-keep-reappearing"></a>Certificaten die ik hebt verwijderd terugkomen
Deze terugkomen waarschijnlijk vanwege een hulpprogramma dat u gebruikt, zoals Visual Studio. Wanneer u opnieuw verbinding met een hulpprogramma dat een certificaat gebruikt maken, wordt deze opnieuw worden geüpload naar Azure.

### <a name="my-certificates-keep-disappearing"></a>Mijn certificaten houden verdwijnen
Wanneer een exemplaar van de virtuele machine wordt gerecycled, gaan alle lokale wijzigingen verloren. Gebruik een [opstarttaak](cloud-services-startup-tasks.md) om certificaten te installeren op de virtuele machine telkens wanneer de functie wordt gestart.

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a>Ik kan mijn beheercertificaten niet vinden in de portal
[Certificaten voor](../azure-api-management-certs.md) zijn alleen beschikbaar in de klassieke Azure Portal. De huidige Azure-portal gebruikt geen beheercertificaten. 

### <a name="how-can-i-disable-a-management-certificate"></a>Hoe kan ik een beheercertificaat uitschakelen?
[Certificaten voor](../azure-api-management-certs.md) kan niet worden uitgeschakeld. U verwijdert deze via de klassieke Azure-Portal als u niet wilt dat meer worden gebruikt.

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a>Hoe maak ik een SSL-certificaat voor een specifiek IP-adres
Volg de aanwijzingen in de [maken van een zelfstudie certificaat](cloud-services-certs-create.md). Gebruik het IP-adres als de DNS-naam.

## <a name="security"></a>Beveiliging
### <a name="disable-ssl-30"></a>SSL 3.0 uitschakelen
Als u wilt uitschakelen, SSL 3.0 en TLS-beveiliging, op een opstarttaak maken die wordt beschreven in dit blogbericht: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/

### <a name="add-nosniff-to-your-website"></a>Voeg **nosniff** aan uw website
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

### <a name="customize-iis-for-a-web-role"></a>IIS voor een Webrol aanpassen
Het script voor het opstarten van IIS uit de [algemene beheertaken voor opstarten](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) artikel.

## <a name="scaling"></a>Schalen
### <a name="i-cannot-scale-beyond-x-instances"></a>Ik kan niet worden uitgebreid dan X exemplaren
Uw Azure-abonnement heeft een limiet van het aantal kernen dat u kunt gebruiken. Schalen werkt niet als u de beschikbare kernen hebt gebruikt. Bijvoorbeeld, als er een limiet van 100 kernen, betekent dit dat u exemplaren van de virtuele machine 100 A1 grootte voor de cloudservice kunnen hebben, of 50 A2 grootte exemplaren van de virtuele machine.

## <a name="networking"></a>Netwerken
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Ik kan niet worden gereserveerd een IP-adres in een cloudservice meerdere VIP 's
Controleer eerst of de instantie van de virtuele machine die u probeert te reserveren van de IP voor is ingeschakeld. Controleer vervolgens of dat u gereserveerde IP-adressen voor bAndere de fasering en productie-implementaties. **Geen** de instellingen niet wijzigen terwijl het upgraden van de implementatie.

## <a name="remote-desktop"></a>Extern bureaublad
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Hoe kan ik extern bureaublad wanneer ik een NSG hebben?
Regels toevoegen aan het NSG waarmee verkeer op poorten **3389** en **20000**.  Extern bureaublad maakt gebruik van poort **3389**.  Cloud Service-exemplaren worden verdeeld, zodat u direct welk exemplaar verbinding maken met kan niet bepalen.  De *RemoteForwarder* en *RemoteAccess* agents RDP-verkeer te beheren en dat de client verzenden van een cookie RDP en geeft u een afzonderlijk exemplaar verbinding maken met.  De *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000*** worden geopend die worden geblokkeerd als er een NSG.
