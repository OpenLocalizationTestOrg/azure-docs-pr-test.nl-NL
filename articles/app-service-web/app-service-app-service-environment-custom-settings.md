---
title: aaaCustom-instellingen voor App Service-omgevingen
description: Aangepaste configuratie-instellingen voor App Service-omgevingen
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a>Aangepaste configuratie-instellingen voor App Service-omgevingen
## <a name="overview"></a>Overzicht
Omdat App Service-omgevingen geïsoleerd tooa één klant zijn, zijn er bepaalde configuratie-instellingen die kunnen worden toegepast uitsluitend tooApp Service-omgevingen. Dit artikel worden Hallo diverse specifieke aanpassingen die beschikbaar voor App Service-omgevingen zijn.

Als u geen App Service-omgeving, Zie [hoe tooCreate een App-serviceomgeving](app-service-web-how-to-create-an-app-service-environment.md).

U kunt de App Service-omgeving aanpassingen opslaan met behulp van een matrix in Hallo nieuwe **clusterSettings** kenmerk. Dit kenmerk is gevonden in de woordenlijst van Hallo 'Eigenschappen' Hallo *hostingEnvironments* Azure Resource Manager-entiteit.

Hallo volgende afgekorte Resource Manager sjabloon fragment toont Hallo **clusterSettings** kenmerk:

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

Hallo **clusterSettings** kenmerk kan worden opgenomen in een Resource Manager sjabloon tooupdate Hallo App Service-omgeving.

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a>Gebruik Azure Resource Explorer tooupdate een App-serviceomgeving
U kunt ook Hallo App Service-omgeving bijwerken met behulp van [Azure Resource Explorer](https://resources.azure.com).  

1. Ga in de Resource Explorer toohello knooppunt voor Hallo App Service-omgeving (**abonnementen** > **resourceGroups** > **providers**  >  **Microsoft.Web** > **hostingEnvironments**). Klik vervolgens op Hallo specifieke App Service-omgeving die u wilt tooupdate.
2. Klik in het rechterdeelvenster hello, **lezen/schrijven** in Hallo bovenste werkbalk tooallow interactieve bewerken in Resource Explorer.  
3. Klik op de blauwe Hallo **bewerken** knop toomake Hallo Resource Manager-sjabloon worden bewerkt.
4. Schuif toohello onder in het rechter deelvenster Hallo. Hallo **clusterSettings** kenmerk onderin Hallo zeer, kunt u opgeven of werk de waarde is.
5. Type (of kopiëren en plakken) Hallo-matrix van configuratiewaarden die u in Hallo wilt **clusterSettings** kenmerk.  
6. Klik op Hallo groen **plaatsen** knop die bovenaan Hallo Hallo rechterdeelvenster toocommit Hallo wijziging toohello App Service-omgeving heeft gevonden.

Maar u Hallo wijziging indient, duurt het ongeveer 30 minuten vermenigvuldigd met het aantal front-ends in Hallo App Service-omgeving voor Hallo wijziging tootake effect Hallo.
Bijvoorbeeld, als een App Service-omgeving vier front-ends heeft, duurt het ongeveer twee uur voor Hallo configuratie update toofinish. Tijdens het Hallo-configuratiewijziging uitgerold, kunnen geen andere bewerkingen vergroten/verkleinen of wijziging configuratiebewerkingen plaatsvinden in Hallo App Service-omgeving.

## <a name="disable-tls-10"></a>TLS 1.0 uitschakelen
Een terugkerende vraag van klanten, met name de klanten die zijn betreft de PCI-naleving audits, is hoe tooexplicitly TLS 1.0 uitschakelen voor hun apps.

TLS 1.0 kan worden uitgeschakeld via de volgende Hallo **clusterSettings** post:

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a>Volgorde van wijziging TLS-coderingssuites
Een andere vraag van klanten is als ze Hallo lijst met door de server onderhandeld coderingen wijzigen en dit kan worden gerealiseerd kunnen door het wijzigen van Hallo **clusterSettings** zoals hieronder wordt weergegeven. Hallo-overzicht van coderingssuites die beschikbaar kan worden opgehaald uit [deze MSDN-artikel](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> Als onjuiste waarden zijn ingesteld voor Hallo coderingssuite die geen inzicht in SChannel krijgen, alle tooyour server van de TLS-communicatie mogelijk functioneert. In dat geval moet u tooremove hello *FrontEndSSLCipherSuiteOrder* vermelding uit **clusterSettings** en het verzenden van Hallo Resource Manager sjabloon toorevert back toohello standaard cipher bijgewerkt Suite-instellingen.  Wees voorzichtig met deze functionaliteit gebruik.
> 
> 

## <a name="get-started"></a>Aan de slag
Hello Azure Quickstart-Resource Manager-sjabloonsite bevat een sjabloon met de basisdefinitie Hallo voor [maken van een App-serviceomgeving](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).

<!-- LINKS -->

<!-- IMAGES -->
