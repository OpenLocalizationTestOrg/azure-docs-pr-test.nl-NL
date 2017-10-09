---
title: een aangepaste aaaCreate probe - Azure Application Gateway - Azure Portal | Microsoft Docs
description: Meer informatie over hoe toocreate een aangepaste test voor Application Gateway met behulp van Hallo-portal
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Een aangepaste test voor de toepassingsgateway maken met behulp van Hallo-portal

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

In dit artikel voegt u een aangepaste test tooan bestaande toepassingsgateway via hello Azure-portal. Aangepaste tests zijn handig voor toepassingen die de pagina controle van een specifieke status hebben, of voor toepassingen die een geslaagde reactie op Hallo standaardwebtoepassing geen bieden.

## <a name="before-you-begin"></a>Voordat u begint

Als u nog geen een application gateway, gaat u naar [een toepassingsgateway maken](application-gateway-create-gateway-portal.md) toocreate een application gateway toowork met.

## <a name="createprobe"></a>Hallo-test maken

Tests worden geconfigureerd in een proces in twee stappen via Hallo-portal. de eerste stap Hallo is toocreate Hallo test. In de tweede stap hello voegt u Hallo test toohello back-end voor HTTP-instellingen van de toepassingsgateway Hallo.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com). Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie van één maand](https://azure.microsoft.com/free)

1. Klik op alle resources in hello Azure-portal venster Favorieten. Klik op Hallo toepassingsgateway in Hallo alle resources blade. Als u hebt geselecteerd al Hallo-abonnement verschillende resources heeft, kunt u partners.contoso.net in Hallo Filter met de naam... vak tooeasily toegang Hallo toepassingsgateway.

1. Klik op **Probes** en klik op Hallo **toevoegen** knop tooadd een test.

  ![Test-blade met informatie is ingevuld toevoegen][1]

1. Op Hallo **toevoegen health test** blade Vul Hallo vereist voor de test Hallo en klikt u op wanneer u klaar **OK**.

  |**Instelling** | **Waarde** | **Details**|
  |---|---|---|
  |**Naam**|customProbe|Deze waarde is een beschrijvende naam toohello-test die toegankelijk is in het Hallo-portal.|
  |**Protocol**|HTTP of HTTPS | Hallo-protocol dat Hallo health test wordt gebruikt.|
  |**Host**|Internet Explorer contoso.com|Deze waarde is Hallo-hostnaam die wordt gebruikt voor de Hallo test. Van toepassing alleen als er meerdere locaties is geconfigureerd op Application Gateway, of gebruik anders '127.0.0.1'. Deze waarde verschilt van de VM-hostnaam Hallo.|
  |**Pad**|/ of een ander pad|Hallo rest van de volledige url voor de aangepaste test Hallo Hallo. Een geldig pad begint met '/'. Gebruik voor het standaardpad Hallo van http://contoso.com alleen '/' |
  |**Interval (sec)**|30|Hoe vaak hello test wordt uitgevoerd toocheck status. Het is niet raadzaam tooset Hallo lager is dan 30 seconden.|
  |**Time-out (sec)**|30|Hallo hoeveelheid tijd Hallo test wacht voordat een time-out optreedt. Hallo time-out interval behoeften toobe hoog genoeg een http-aanroep tooensure Hallo back-end health-pagina kan worden gemaakt, is beschikbaar.|
  |**Drempelwaarde voor onjuiste status**|3|Aantal mislukte pogingen toobe niet in orde beschouwd. Een drempelwaarde 0 betekent dat als een controle mislukt Hallo back-end wordt onmiddellijk bepaald beschadigd.|

  > [!IMPORTANT]
  > Hallo-hostnaam is niet hetzelfde als servernaam Hallo. Deze waarde is Hallo-naam van Hallo virtuele host op Hallo-toepassingsserver wordt uitgevoerd. Hallo-test wordt verzonden toohttp: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>Test toohello gateway toevoegen

Nu hello test is gemaakt, is het tijd tooadd het toohello gateway. Test-instellingen zijn ingesteld op Hallo back-end voor HTTP-instellingen van de toepassingsgateway Hallo.

1. Klik op **HTTP-instellingen** op Hallo application gateway toobring up Hallo configuratie blade klikt u op Hallo huidige back-end HTTP-instellingen die worden vermeld in het Hallo-venster.

  ![venster van de instellingen voor HTTPS][2]

1. Op Hallo **appGatewayBackEndHttpSettings** instellingenblade, selectievakje Hallo **gebruik aangepaste test** selectievakje in en kies Hallo test gemaakt in Hallo [maken Hallo test](#createprobe) sectie op Hallo **aangepaste test** vervolgkeuzelijst...
Wanneer voltooid, klikt u op **opslaan** en het Hallo-instellingen worden toegepast.

Hallo standaard test controleert Hallo toegang toohello standaardwebtoepassing. Nu dat een aangepaste test is gemaakt, gebruikt de toepassingsgateway Hallo Hallo aangepast pad gedefinieerd toomonitor health voor Hallo back-endservers. Op basis van criteria Hallo die is gedefinieerd, controleert toepassingsgateway Hallo Hallo pad dat is opgegeven in Hallo test. Als Hallo toohost:Port aanroepen / pad niet in een HTTP 200-399 statusantwoord resulteert, wordt Hallo-server buiten rotatie genomen als Hallo slecht weergavedrempel is bereikt. Zoeken blijft op Hallo slecht exemplaar toodetermine wanneer deze opnieuw in orde is. Zodra Hallo-exemplaar wordt toegevoegd back toohealthy-servergroep, verkeer begint stromende tooit opnieuw en zoek toohello exemplaar wordt voortgezet met de opgegeven interval als normale gebruiker.

## <a name="next-steps"></a>Volgende stappen

hoe tooconfigure SSL-Offloading met Azure Application Gateway, Zie toolearn [SSL-Offload configureren](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

