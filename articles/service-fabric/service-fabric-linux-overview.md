---
title: Service Fabric op Linux aaaAzure | Microsoft Docs
description: Service Fabric-clusters ondersteuning voor Linux en Java, wat betekent dat u zult kunnen toodeploy en host-Service Fabric-toepassingen geschreven in Java en C# op Linux.
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a>Service Fabric op Linux
Hallo-evaluatieversie van Service Fabric op Linux kunt u toobuild, implementeren en beheren van maximaal beschikbare, sterk schaalbare toepassingen op Linux, net zoals u zou in Windows doen. Hallo Service Fabric frameworks (Reliable Services en Reliable Actors) zijn beschikbaar in Java op Linux in toevoeging tooC # (.NET Core).  U kunt ook samenstellen [uitvoerbare gastservices](service-fabric-deploy-existing-app.md) met elke taal of elk framework. Bovendien ondersteunt Hallo preview Docker-containers organiseren. Docker-containers kunnen worden uitgevoerd Gast uitvoerbare bestanden of systeemeigen Service Fabric-services, die Service Fabric-frameworks hello gebruiken.

Service Fabric op Linux is conceptueel gezien equivalent tooService Fabric in Windows (met uitzondering van OS-specificaties en programmeertalen). Dus de meeste van onze [bestaande documentatie](http://aka.ms/servicefabricdocs) geldt helpen u met het Hallo-technologie raken.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a>Ondersteunde besturingssystemen en programmeertalen
Hallo beperkte preview ondersteunt Hallo maken van een vak ontwikkeling clusters bovendien clusters toomulti-machine in Azure, Ubuntu Server 16.04 uitgevoerd. Hallo preview ondersteunt Hallo Reliable Actors en Hallo betrouwbare Stateless Services frameworks in Java en C# in toevoeging tooguest uitvoerbare bestanden en de Docker-containers te organiseren.  

> [!NOTE]
> Betrouwbare verzamelingen worden nog niet ondersteund in Linux. Standaard alleen clusters worden niet ondersteund - ofwel slechts één selectievakje en meerdere machines Azure Linux-clusters worden ondersteund in Hallo preview.
>
>


## <a name="supported-tooling"></a>Ondersteunde tooling
Hallo preview biedt ondersteuning voor interactie met Hallo-cluster via Service Fabric CLI. Integratie met Eclipse en Yeoman is opgegeven voor Java-ontwikkelaars met Eclipse ondersteund op Linux en OS x. Hallo OSX integratie maakt gebruik van een Linux-VM achter de schermen Hallo via vagrant. Voor C#-ontwikkelaars, is de integratie met Yeoman toogenerate Toepassingssjablonen opgegeven.

## <a name="next-steps"></a>Volgende stappen

* Raken met de Hallo [Reliable Actors](service-fabric-reliable-actors-introduction.md) en [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks
* [Uw ontwikkelomgeving voorbereiden in Linux](service-fabric-get-started-linux.md)
* [Uw ontwikkelomgeving voorbereiden in OSX](service-fabric-get-started-mac.md)
* [Uw eerste Service Fabric-Java-toepassing op Linux maken](service-fabric-create-your-first-linux-application-with-java.md)
* [Setup van Service Fabric continue integratie en implementatie met Jenkins en GitHub](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [Verschillen tussen Service Fabric in Windows en Linux](service-fabric-linux-windows-differences.md)
