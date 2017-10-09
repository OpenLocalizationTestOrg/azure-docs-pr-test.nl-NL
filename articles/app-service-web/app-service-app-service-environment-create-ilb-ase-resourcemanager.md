---
title: aaaHow tooCreate een ILB as-omgeving met behulp van Azure Resource Manager-sjablonen | Microsoft Docs
description: Meer informatie over hoe toocreate een interne load balancer as-omgeving met behulp van Azure Resource Manager-sjablonen.
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>Hoe tooCreate een ILB as-omgeving met behulp van Azure Resource Manager-sjablonen

> [!NOTE] 
> In dit artikel gaat over het Hallo v1 App Service-omgeving. Er is een nieuwere versie van App Service-omgeving die eenvoudiger toouse en wordt uitgevoerd op krachtiger infrastructuur Hallo. meer informatie over de nieuwe versie Hallo met Hallo beginnen toolearn [inleiding toohello App Service-omgeving](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Overzicht
App Service-omgevingen kunnen worden gemaakt met de interne adres van een virtueel netwerk in plaats van een openbare VIP.  Deze interne adres is verstrekt door een Azure-onderdeel Hallo interne load balancer (ILB) genoemd.  Een as ILB-omgeving kunnen worden gemaakt met behulp van hello Azure-portal.  Ook kunnen worden gemaakt met behulp van automatisering in Azure Resource Manager-sjablonen.  In dit artikel leert Hallo en syntaxis nodig toocreate een ILB-as-omgeving met Azure Resource Manager-sjablonen.

Er zijn drie stappen die betrokken zijn bij de automatisering van het maken van een as ILB-omgeving:

1. Eerste, Hallo base as-omgeving wordt gemaakt in een virtueel netwerk met een interne load balancer-adres in plaats van een openbare VIP.  Als onderdeel van deze stap wordt een hoofddomeinnaam toegewezen toohello ILB as-omgeving.
2. Eenmaal Hallo die ILB as-omgeving is gemaakt, een SSL-certificaat is geüpload.  
3. Hallo is geüploade SSL-certificaat expliciet toegewezen toohello ILB as-omgeving als de 'standaard' SSL-certificaat.  Dit SSL-certificaat wordt gebruikt voor SSL-verkeer tooapps op Hallo ILB as-omgeving wanneer Hallo apps worden aangepakt met behulp van Hallo algemene hoofdmap domein toegewezen toohello as-omgeving (bijvoorbeeld https://someapp.mycustomrootcomain.com)

## <a name="creating-hello-base-ilb-ase"></a>Hallo Base ILB as-omgeving maken
Een voorbeeld van Azure Resource Manager-sjabloon en de bijbehorende parameterbestand zijn beschikbaar op GitHub [hier][quickstartilbasecreate].

De meeste van Hallo-parameters in Hallo *azuredeploy.parameters.json* bestand algemene toocreating evenals ASEs gebonden tooa openbare VIP beide ASEs ILB zijn.  Hallo lijst hieronder aanroepen van speciale Opmerking uitvoerparameters, of die zijn uniek, bij het maken van een as ILB-omgeving:

* *interalLoadBalancingMode*: ingesteld In de meeste gevallen deze too3, wat betekent zowel HTTPS-verkeer op poort 80/443 dat, en Hallo controlegegevens/channel-poorten geluisterd tooby Hallo FTP-service op Hallo as-omgeving, wordt gebonden tooan ILB toegewezen virtueel netwerk interne adres.  Als deze eigenschap instelt in plaats daarvan too2, vervolgens alleen Hallo FTP-service gekoppeld poorten (zowel besturings- als kanalen) wordt gebonden wordt tooan ILB adres, terwijl Hallo HTTP/HTTPS-verkeer op Hallo openbare VIP blijft.
* *dnsSuffix*: deze parameter bepaalt Hallo standaard hoofddomein dat wordt toegewezen toohello as-omgeving.  In de openbare variatie op Hallo van Azure App Service, Hallo standaard hoofddomein voor alle web-apps is *azurewebsites.net*.  Maar omdat een ILB-as-omgeving van de klant van de interne tooa virtueel netwerk, niet dat u zin toouse Hallo openbare van de service standaard hoofddomein.  Een as ILB-omgeving moet in plaats daarvan een standaard-hoofddomein die zinvol voor gebruik binnen een bedrijf intern virtueel netwerk hebben.  Bijvoorbeeld, een hypothetische Contoso Corporation gebruiken een hoofddomein standaard van *interne contoso.com* voor apps die bedoeld tooonly zijn worden omgezet en toegankelijk is in het virtuele netwerk van Contoso. 
* *ipSslAddressCount*: deze parameter wordt automatisch opgehaald tooa waarde van 0 in Hallo *azuredeploy.json* bestand omdat ILB ASEs slechts één ILB-adres hebben.  Er zijn geen expliciete SSL IP-adressen voor een as ILB-omgeving, en daarom Hallo SSL IP-adresgroep voor een as ILB-omgeving moet worden ingesteld toozero, anders een inrichting fout zal optreden. 

Eenmaal Hallo *azuredeploy.parameters.json* bestand voor een ILB as-omgeving, Hallo ILB as-omgeving kunnen vervolgens worden gemaakt met de volgende Powershell-codefragment Hallo is ingevuld.  Hallo bestand paden toomatch waar hello Azure Resource Manager-sjabloonbestanden op uw computer bevinden zich wijzigen.  Onthoud toosupply ook uw eigen waarden voor de naam van hello Azure Resource Manager-implementatie en de naam van resourcegroep.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Sjabloon is ingediend duurt het enkele uren Hallo ILB as-omgeving toobe gemaakt na hello Azure Resource Manager.  Zodra het Hallo maken is voltooid, wordt Hallo ILB as-omgeving in Hallo lijst met App Service-omgevingen voor Hallo-abonnement dat Hallo implementatie geactiveerd Hallo Portal UX weergegeven.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Uploaden en configureren van SSL-certificaat 'Default' Hallo
Eenmaal Hallo die ILB as-omgeving wordt gemaakt, een SSL-certificaat moet worden gekoppeld aan Hallo as-omgeving als Hallo 'standaard' SSL-certificaat gebruiken voor het tot stand brengen van tooapps voor SSL-verbindingen.  Hallo hypothetische Contoso Corporation bijvoorbeeld voortzet als Hallo as-omgeving van standaard DNS-achtervoegsel is *interne contoso.com*, klikt u vervolgens een verbinding te*https://some-random-app.internal-contoso.com*vereist een SSL-certificaat is geldig voor **.internal contoso.com*. 

Er zijn tal van manieren tooobtain een geldig SSL-certificaat waaronder interne CA's, het aanschaffen van een certificaat van een externe verlener en met behulp van een zelfondertekend certificaat.  Ongeacht Hallo bron van het SSL-certificaat hello moeten hello volgende kenmerken van het certificaat toobe correct is geconfigureerd:

* *Onderwerp*: dit kenmerk te moet worden ingesteld **.your-hoofdmap-domain-here.com*
* *Alternatieve onderwerpnaam*: dit kenmerk moet bevatten beide **.your-hoofdmap-domain-here.com*, en **.scm.your-hoofdmap-domain-here.com*.  Hallo reden voor het tweede Hallo-vermelding is die SSL-verbindingen toohello SCM/Kudu site die is gekoppeld aan elke app worden gemaakt met behulp van een adres van het formulier Hallo *your-app-name.scm.your-root-domain-here.com*.

Met een geldig SSL-certificaat in de hand, worden twee aanvullende voorbereidende stappen uitgevoerd.  Hallo SSL-certificaat moet toobe geconverteerd en opgeslagen als een .pfx-bestand.  Houd er rekening mee dat Hallo pfx-bestand moet alle tussenliggende tooinclude en basiscertificaten en moet ook toobe met een wachtwoord beveiligd.

Hallo resulterende pfx-bestand moet toobe geconverteerd naar een base64-tekenreeks omdat Hallo SSL-certificaat worden geüpload met een Azure Resource Manager-sjabloon.  Aangezien Azure Resource Manager-sjablonen tekstbestanden zijn, moet Hallo pfx-bestand toobe geconverteerd naar een base64-tekenreeks, zodat deze opgenomen als een parameter van het Hallo-sjabloon worden kan.

Hallo Powershell onderstaande codefragment toont een voorbeeld van een zelfondertekend certificaat genereren, Hallo certificaat exporteren als een .pfx-bestand Hallo pfx-bestand converteren naar een base64-gecodeerde tekenreeks en vervolgens opslaan Hallo base64 gecodeerde tekenreeks tooa afzonderlijk bestand.  Hallo Powershell-code voor base64-codering gebaseerd op Hallo is [Powershell-Scripts Blog][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Zodra de Hallo SSL-certificaat heeft gegenereerd en geconverteerde tooa met base64 gecodeerde tekenreeks, hello Azure Resource Manager-sjabloon van het voorbeeld op GitHub voor [Hallo standaard SSL-certificaat configureren] [ configuringDefaultSSLCertificate] kan worden gebruikt.

Hallo-parameters in Hallo *azuredeploy.parameters.json* bestand worden hieronder weergegeven:

* *appServiceEnvironmentName*: naam Hallo Hallo ILB as-omgeving wordt geconfigureerd.
* *existingAseLocation*: string met tekst hello Azure-regio waar hello ILB as-omgeving is geïmplementeerd.  Bijvoorbeeld: 'Zuid-centraal VS'.
* *pfxBlobString*: Hallo based64 gecodeerd tekenreeksweergave van Hallo pfx-bestand.  Met behulp van Hallo codefragment eerder weergegeven, zou u tekenreeks in 'exportedcert.pfx.b64' Hallo kopiëren en plakken in als waarde Hallo Hallo *pfxBlobString* kenmerk.
* *wachtwoord*: Hallo serverwachtwoord toosecure Hallo pfx-bestand.
* *certificateThumbprint*: Hallo vingerafdruk van het certificaat.  Als u deze waarde wordt opgehaald uit Powershell (bijvoorbeeld *$certificate. Vingerafdruk* van Hallo eerdere codefragment), kunt u Hallo-waarde als-is.  Als u Hallo-waarde van Hallo Windows certificaat dialoogvenster kopieert, moet u echter toostrip uit Hallo overbodige spaties.  Hallo *certificateThumbprint* moet als volgt uitzien: AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *Certificaatnaam*: een beschrijvende tekenreeks-id van uw eigen keuze tooidentity Hallo certificaat gebruikt.  Hallo-naam wordt gebruikt als onderdeel van Hallo unieke Azure Resource Manager-id voor Hallo *Microsoft.Web/certificates* entiteit geeft Hallo SSL-certificaat.  de naam van de Hallo **moet** eindigen met het volgende achtervoegsel Hallo: \_yourASENameHere_InternalLoadBalancingASE.  Dit achtervoegsel wordt gebruikt door Hallo-portal, zoals een indicator die Hallo certificaat wordt gebruikt voor het beveiligen van een as ingeschakeld met een ILB-omgeving.

Een afgekorte voorbeeld van *azuredeploy.parameters.json* worden hieronder weergegeven:

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Eenmaal Hallo *azuredeploy.parameters.json* bestand is ingevuld, Hallo standaard SSL-certificaat kan worden geconfigureerd met behulp van de volgende Powershell-codefragment Hallo.  Hallo bestand paden toomatch waar hello Azure Resource Manager-sjabloonbestanden op uw computer bevinden zich wijzigen.  Onthoud toosupply ook uw eigen waarden voor de naam van hello Azure Resource Manager-implementatie en de naam van resourcegroep.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Sjabloon is ingediend dat het duurt ongeveer 40 minuten minuten per as-omgeving front-tooapply Hallo wijziging na hello Azure Resource Manager.  Bijvoorbeeld, met een standaard duurt grootte as-omgeving met behulp van twee front-ends Hallo sjabloon om één uur en twintig minuten toocomplete.  Tijdens het Hallo-sjabloon wordt uitgevoerd worden Hallo as-omgeving kunnen tooscaled niet.  

Zodra het Hallo-sjabloon is voltooid, apps op Hallo ILB as-omgeving kunnen worden geopend via HTTPS en Hallo verbindingen worden beveiligd met behulp van Hallo standaard SSL-certificaat.  Hallo standaard SSL-certificaat wordt gebruikt wanneer de apps op Hallo ILB as-omgeving met een combinatie van naam van de toepassing hello plus Hallo standaard hostnaam worden aangepakt.  Bijvoorbeeld *https://mycustomapp.internal-contoso.com* Hallo standaard SSL-certificaat voor zou gebruiken **.internal contoso.com*.

Echter, net als bij apps die worden uitgevoerd op Hallo openbare multitenant-service, ontwikkelaars kunnen ook aangepaste hostnamen voor afzonderlijke apps configureren, en configureer vervolgens unieke SNI-SSL-certificaatbindingen voor afzonderlijke apps.  

## <a name="getting-started"></a>Aan de slag
tooget de slag met App Service-omgevingen, Zie [inleiding tooApp Service-omgeving](app-service-app-service-environment-intro.md)

Alle artikelen en hoe-aan de voor App Service-omgevingen beschikbaar in Hallo zijn [Leesmij-bestand voor Toepassingsserviceomgevingen](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

