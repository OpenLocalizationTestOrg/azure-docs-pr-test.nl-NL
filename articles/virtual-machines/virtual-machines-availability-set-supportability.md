---
title: aaaSupportability van het toevoegen van Azure Virtual machines tooan bestaande beschikbaarheidsset | Microsoft Docs
description: Ondersteuning voor het toevoegen van Azure Virtual machines tooan bestaande beschikbaarheidsset.
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
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Ondersteuning voor het toevoegen van Azure Virtual machines tooan bestaande beschikbaarheidsset

Beperkingen kan van tijd tot tijd verschijnen wanneer u nieuwe virtuele machines (VM's) tooan bestaande beschikbaarheidsset toevoegt. Hallo volgende grafiekdetails welke VM-reeks kunt u mengen in dezelfde beschikbaarheidsset Hallo.

Hier volgt Hallo ondersteuningsmogelijkheden matrix toomix verschillende typen virtuele machines:

Reeks & Beschikbaarheidsset|Tweede VM|A|Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Eerste VM|||||||
|A||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Alle andere reeks kan niet worden in dezelfde beschikbaarheidsset omdat ze een specifieke hardware vereist Hallo.
