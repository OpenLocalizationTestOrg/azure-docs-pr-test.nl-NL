---
title: aaaCreate een internetgerichte load balancer voor Azure-cloudservices | Microsoft Docs
description: Meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler in het klassieke implementatiemodel voor cloudservices
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>Aan de slag met het maken van een internetgerichte load balancer voor cloudservices

> [!div class="op_single_selector"]
> * [Klassieke Azure Portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model. Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken. U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel. In dit artikel bevat informatie over Hallo klassieke implementatiemodel. U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

Cloud-services worden automatisch geconfigureerd met een load balancer en kunnen worden aangepast via Hallo-ServiceModel.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Een load balancer met behulp van het servicedefinitiebestand Hallo maken

U kunt hello Azure SDK voor .NET 2.5 tooupdate gebruikmaken van de cloudservice. Instellingen voor endpoint voor cloudservices zijn aangebracht in Hallo [definitie](https://msdn.microsoft.com/library/azure/gg557553.aspx) csdef-bestand.

Hallo volgende voorbeeld laat zien hoe een servicedefinition.csdef-bestand voor de implementatie van een cloud is geconfigureerd:

Hallo codefragment voor Hallo csdef-bestand is gegenereerd door de implementatie van een cloud te controleren, kunt u Hallo Extern eindpunt geconfigureerd toouse poorten HTTP op poort 10000, 10001 en 10002 zien.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>De status van een load balancer voor cloudservices controleren

Hallo Hieronder volgt een voorbeeld van een health test:

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

Hallo load balancer combineert Hallo van Hallo eindpunt en Hallo informatie van Hallo test toocreate een URL in de vorm van Hallo `http://{DIP of VM}:80/Probe.aspx` die kunnen worden gebruikt tooquery Hallo status van Hallo-service.

Hallo service detecteert periodieke tests uit Hallo hetzelfde IP-adres. Dit is Hallo health test aanvraag afkomstig is van de host van knooppunt Hallo Hallo waarop Hallo virtuele machine wordt uitgevoerd. Hallo-service heeft toorespond met een HTTP 200-statuscode voor Hallo load balancer tooassume Hallo-service is in orde. Andere HTTP-status code (bijvoorbeeld 503) rechtstreeks vergt Hallo virtuele machine uit de draaihoek.

Hallo test definitie bepaalt ook Hallo frequentie van Hallo test. In ons geval is Hallo load balancer scannen Hallo eindpunt elke 5 seconden. Als er geen positief antwoord wordt ontvangen voor 10 sec (twee test-intervallen), Hallo test wordt aangenomen dat omlaag en Hallo virtuele machine wordt uitgevoerd buiten de draaihoek. Op dezelfde manier als Hallo service buiten het wisselen valt en een positief antwoord wordt ontvangen, Hallo service geplaatst terug toorotation meteen. Als het Hallo-service tussen in orde en slecht veranderen is, besluiten Hallo load balancer toodelay Hallo binnengebracht van Hallo service back toorotation totdat deze is in orde voor een aantal tests.

Controleer Hallo service definitie schema voor Hallo [health test](https://msdn.microsoft.com/library/azure/jj151530.aspx) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

[Aan de slag met het configureren van een interne load balancer](load-balancer-get-started-ilb-arm-ps.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)

