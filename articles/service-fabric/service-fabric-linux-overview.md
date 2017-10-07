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
# <a name="service-fabric-on-linux"></a><span data-ttu-id="01c4b-103">Service Fabric op Linux</span><span class="sxs-lookup"><span data-stu-id="01c4b-103">Service Fabric on Linux</span></span>
<span data-ttu-id="01c4b-104">Hallo-evaluatieversie van Service Fabric op Linux kunt u toobuild, implementeren en beheren van maximaal beschikbare, sterk schaalbare toepassingen op Linux, net zoals u zou in Windows doen.</span><span class="sxs-lookup"><span data-stu-id="01c4b-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="01c4b-105">Hallo Service Fabric frameworks (Reliable Services en Reliable Actors) zijn beschikbaar in Java op Linux in toevoeging tooC # (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="01c4b-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="01c4b-106">U kunt ook samenstellen [uitvoerbare gastservices](service-fabric-deploy-existing-app.md) met elke taal of elk framework.</span><span class="sxs-lookup"><span data-stu-id="01c4b-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="01c4b-107">Bovendien ondersteunt Hallo preview Docker-containers organiseren.</span><span class="sxs-lookup"><span data-stu-id="01c4b-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="01c4b-108">Docker-containers kunnen worden uitgevoerd Gast uitvoerbare bestanden of systeemeigen Service Fabric-services, die Service Fabric-frameworks hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="01c4b-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="01c4b-109">Service Fabric op Linux is conceptueel gezien equivalent tooService Fabric in Windows (met uitzondering van OS-specificaties en programmeertalen).</span><span class="sxs-lookup"><span data-stu-id="01c4b-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="01c4b-110">Dus de meeste van onze [bestaande documentatie](http://aka.ms/servicefabricdocs) geldt helpen u met het Hallo-technologie raken.</span><span class="sxs-lookup"><span data-stu-id="01c4b-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="01c4b-111">Ondersteunde besturingssystemen en programmeertalen</span><span class="sxs-lookup"><span data-stu-id="01c4b-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="01c4b-112">Hallo beperkte preview ondersteunt Hallo maken van een vak ontwikkeling clusters bovendien clusters toomulti-machine in Azure, Ubuntu Server 16.04 uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="01c4b-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="01c4b-113">Hallo preview ondersteunt Hallo Reliable Actors en Hallo betrouwbare Stateless Services frameworks in Java en C# in toevoeging tooguest uitvoerbare bestanden en de Docker-containers te organiseren.</span><span class="sxs-lookup"><span data-stu-id="01c4b-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="01c4b-114">Betrouwbare verzamelingen worden nog niet ondersteund in Linux.</span><span class="sxs-lookup"><span data-stu-id="01c4b-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="01c4b-115">Standaard alleen clusters worden niet ondersteund - ofwel slechts één selectievakje en meerdere machines Azure Linux-clusters worden ondersteund in Hallo preview.</span><span class="sxs-lookup"><span data-stu-id="01c4b-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="01c4b-116">Ondersteunde tooling</span><span class="sxs-lookup"><span data-stu-id="01c4b-116">Supported tooling</span></span>
<span data-ttu-id="01c4b-117">Hallo preview biedt ondersteuning voor interactie met Hallo-cluster via Service Fabric CLI.</span><span class="sxs-lookup"><span data-stu-id="01c4b-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="01c4b-118">Integratie met Eclipse en Yeoman is opgegeven voor Java-ontwikkelaars met Eclipse ondersteund op Linux en OS x.</span><span class="sxs-lookup"><span data-stu-id="01c4b-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="01c4b-119">Hallo OSX integratie maakt gebruik van een Linux-VM achter de schermen Hallo via vagrant.</span><span class="sxs-lookup"><span data-stu-id="01c4b-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="01c4b-120">Voor C#-ontwikkelaars, is de integratie met Yeoman toogenerate Toepassingssjablonen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="01c4b-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01c4b-121">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01c4b-121">Next steps</span></span>

* <span data-ttu-id="01c4b-122">Raken met de Hallo [Reliable Actors](service-fabric-reliable-actors-introduction.md) en [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span><span class="sxs-lookup"><span data-stu-id="01c4b-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="01c4b-123">Uw ontwikkelomgeving voorbereiden in Linux</span><span class="sxs-lookup"><span data-stu-id="01c4b-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="01c4b-124">Uw ontwikkelomgeving voorbereiden in OSX</span><span class="sxs-lookup"><span data-stu-id="01c4b-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="01c4b-125">Uw eerste Service Fabric-Java-toepassing op Linux maken</span><span class="sxs-lookup"><span data-stu-id="01c4b-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="01c4b-126">Setup van Service Fabric continue integratie en implementatie met Jenkins en GitHub</span><span class="sxs-lookup"><span data-stu-id="01c4b-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="01c4b-127">Verschillen tussen Service Fabric in Windows en Linux</span><span class="sxs-lookup"><span data-stu-id="01c4b-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
