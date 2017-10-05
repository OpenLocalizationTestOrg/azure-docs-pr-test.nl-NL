---
title: Ondersteuning van Azure Virtual machines toevoegen aan de bestaande beschikbaarheidsset instellen | Microsoft Docs
description: Ondersteuning van Azure Virtual machines toevoegen aan een bestaande beschikbaarheidsset.
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: 3ce9b8a79108cb9e57df14bcb3354cc637193233
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="supportability-of-adding-azure-vms-to-an-existing-availability-set"></a>Ondersteuning van Azure Virtual machines toevoegen aan een bestaande beschikbaarheidsset

Van tijd tot tijd kan verschijnen beperkingen wanneer u nieuwe virtuele machines (VM's) toevoegen aan een bestaande beschikbaarheidsset. Het volgende diagram details over welke VM-reeks u in dezelfde beschikbaarheidsset mengen kunt.

Dit is de matrix ondersteuningsmogelijkheden mix van verschillende typen van virtuele machines:

Reeks & Beschikbaarheidsset|Tweede VM|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Eerste VM|||||||
|A||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Alle andere reeks kan niet worden in dezelfde beschikbaarheidsset omdat ze een specifieke hardware vereist.