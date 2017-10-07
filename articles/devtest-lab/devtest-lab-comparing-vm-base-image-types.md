---
title: "aaaComparing aangepaste installatiekopieën en formules in DevTest Labs | Microsoft Docs"
description: "Meer informatie over Hallo verschillen tussen aangepaste installatiekopieën en formules als VM baseert zodat u kunt beslissen welke beste past bij uw omgeving."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a>Vergelijking van aangepaste installatiekopieën en formules in DevTest Labs
Beide [aangepaste installatiekopieën](devtest-lab-create-template.md) en [formules](devtest-lab-manage-formulas.md) kan worden gebruikt als basis voor [gemaakt van de nieuwe virtuele machines](devtest-lab-add-vm-with-artifacts.md). Hallo belangrijkste onderscheid tussen aangepaste installatiekopieën en formules is echter dat een aangepaste installatiekopie is gewoon een op basis van een VHD, terwijl een formule een installatiekopie op basis van een VHD is *naast* vooraf geconfigureerde instellingen - zoals VM-grootte, virtueel netwerk subnet en artefacten. Deze vooraf geconfigureerde instellingen zijn ingesteld met de standaardwaarden die gelijktijdig Hallo met maken van VM's kunnen worden genegeerd. Dit artikel worden enkele voordelen hello (professionals) en nadelen (nadelen) toousing aangepaste installatiekopieën ten opzichte van formules.

## <a name="custom-image-pros-and-cons"></a>Aangepaste installatiekopie voor- en nadelen
Aangepaste installatiekopieën bieden een statische, niet-wijzigbaar manier toocreate VM's van een gewenste-omgeving. 

**Professionals**

* VM-inrichting van een aangepaste installatiekopie is snelle als niets na Hallo die VM wordt ingezet wordt gewijzigd van Hallo-installatiekopie. Met andere woorden, zijn er geen instellingen tooapply Hallo aangepaste installatiekopie wordt alleen maar een afbeelding zonder de instellingen. 
* Virtuele machines die zijn gemaakt op basis van één aangepaste installatiekopie zijn identiek.

**Nadelen**

* Als u een bepaald aspect van de aangepaste installatiekopie Hallo tooupdate moet, Hallo installatiekopie moet opnieuw worden gemaakt.  

## <a name="formula-pros-and-cons"></a>Formule voor- en nadelen
Formules bieden een dynamische manier toocreate VM's van Hallo gewenste instellingen.

**Professionals**

* Wijzigingen in Hallo-omgeving kunnen worden vastgelegd op Hallo snel via artefacten. Bijvoorbeeld, als u een virtuele machine is geïnstalleerd met de meest recente bits Hallo vanuit de pipeline release of meest recente code op Hallo van uw opslagplaats bijschrijven, kunt u gewoon opgeven een artefact die de meest recente bits Hallo implementeert of zich aanmeldt Hallo meest recente code in Hallo formule samen met een doel basisinstallatiekopie. Telkens wanneer deze formule gebruikte toocreate VM's en zijn Hallo nieuwste bits/code geïmplementeerd/aangemeld toohello VM. 
* Formules kunnen standaardinstellingen die aangepaste installatiekopieën niet - zoals instellingen voor virtuele netwerken en VM-grootten biedt definiëren. 
* Hallo-instellingen opgeslagen in een formule als standaardwaarden worden weergegeven, maar kunnen worden gewijzigd wanneer Hallo VM wordt gemaakt. 

**Nadelen**

* Een VM maken van een formule kan langer duren dan het maken van een virtuele machine van een aangepaste installatiekopie.

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a>Verwante blogberichten
* [Aangepaste installatiekopieën of formules?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a>Volgende stappen
- [DevTest Labs Veelgestelde vragen](devtest-lab-faq.md)