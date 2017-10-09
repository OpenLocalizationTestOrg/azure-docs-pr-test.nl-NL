---
title: "een geïmplementeerde StorSimple-apparaat aaaTroubleshoot | Microsoft Docs"
description: "Hierin wordt beschreven hoe toodiagnose en los fouten die optreden op een StorSimple-apparaat dat momenteel is geïmplementeerd en operationele."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>Een operationele StorSimple-apparaat oplossen
## <a name="overview"></a>Overzicht
Dit artikel bevat nuttige richtlijnen voor probleemoplossing voor het oplossen van problemen met de configuratie die u tegenkomen kunt nadat uw StorSimple-apparaat geïmplementeerd en operationele is. Hierin worden veelvoorkomende problemen, mogelijke oorzaken en aanbevolen stappen toohelp oplossen van problemen die u ervaren kunt wanneer u Microsoft Azure StorSimple uitvoert. Deze informatie is van toepassing tooboth Hallo lokale fysieke StorSimple-apparaat en Hallo virtuele StorSimple-apparaat.

Aan het einde van de Hallo van dit artikel vindt u een lijst met foutcodes die u tijdens de bewerking van de Microsoft Azure StorSimple tegenkomen kunt, evenals stappen kunt u nemen tooresolve Hallo fouten. 

## <a name="setup-wizard-process-for-operational-devices"></a>Wizard configuratieproces voor operationele apparaten
Gebruik van de wizard setup hello ([Invoke-HcsSetupWizard][1]) toocheck Hallo apparaatconfiguratie en los de problemen indien nodig.

Wanneer u de wizard setup Hallo op een apparaat eerder geconfigureerde en operationele uitvoert, verschilt Hallo processtroom. U kunt alleen Hallo na vermeldingen wijzigen:

* IP-adres, subnetmasker en gateway
* Primaire DNS-server
* Primaire NTP-server
* Optionele webproxyconfiguratie

Hallo-installatiewizard voert geen Hallo operations gerelateerde toopassword verzamelen en registreren van apparaten.

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Fouten die tijdens de daaropvolgende wordt uitgevoerd van de wizard setup Hallo optreden
Hallo volgende tabel beschrijft Hallo fouten die optreden mogelijk wanneer u de wizard setup Hallo uitgevoerd op een operationele apparaat, mogelijke oorzaken voor Hallo fouten en aanbevolen acties tooresolve ze. 

| Nee. | Foutbericht of voorwaarde | Mogelijke oorzaken | Aanbevolen actie |
|:--- |:--- |:--- |:--- |
| 1 |Fout 350032: Dit apparaat is al uitgeschakeld. |U ziet deze fout als u de wizard setup Hallo uitvoert op een apparaat dat wordt gedeactiveerd. |[Neem contact op met Microsoft Support](storsimple-contact-microsoft-support.md) voor volgende stappen. Een gedeactiveerde apparaat kan niet worden geplaatst in de service. Hallo-apparaat kan opnieuw worden geactiveerd als fabrieksinstellingen mogelijk vereist. |
| 2 |Invoke-HcsSetupWizard: ERROR_INVALID_FUNCTION (uitzondering van HRESULT: 0x80070001) |Hallo-update voor DNS-server is mislukt. DNS-instellingen zijn algemene instellingen en worden toegepast op alle netwerkinterfaces van Hallo ingeschakeld. |Hallo interface inschakelen en toepassing hello DNS-instellingen opnieuw. Omdat deze instellingen globale zijn, kan dit Hallo netwerk voor andere ingeschakelde interfaces verstoren. |
| 3 |Hallo apparaat toobe online in Hallo StorSimple Manager-serviceportal wordt weergegeven, maar wanneer u toocomplete Hallo minimale instelling probeert en Hallo-configuratie op te slaan, Hallo-bewerking is mislukt. |Tijdens de eerste configuratie is Hallo webproxy niet geconfigureerd, zelfs als er een werkelijke proxyserver aanwezig is. |Gebruik Hallo [cmdlet Test-HcsmConnection] [ 2] toolocate Hallo-fout. [Neem contact op met Microsoft Support](storsimple-contact-microsoft-support.md) bent u toocorrect Hallo probleem. |
| 4 |Invoke-HcsSetupWizard: Waarde ligt niet binnen het bereik van Hallo verwacht. |Een onjuist subnetmasker produceert deze fout. Mogelijke oorzaken zijn: <ul><li> Hallo-subnetmasker is ontbreekt of is leeg.</li><li>Hallo Ipv6-voorvoegselindeling is onjuist.</li><li>Hallo-interface is ingeschakeld voor de cloud, maar Hallo-gateway is ontbreekt of is onjuist.</li></ul>Houd er rekening mee dat de DATA 0 automatisch ingeschakeld voor de cloud is als geconfigureerd via de wizard setup Hallo. |toodetermine hello probleem subnet 0.0.0.0 of 256.256.256.256 gebruik en vervolgens bekijkt hello uitvoer. Geef juiste waarden voor subnetmasker hello, gateway en Ipv6-voorvoegsel, indien nodig. |

## <a name="error-codes"></a>Foutcodes
Fouten worden in de juiste volgorde weergegeven.

| Foutnummer | Fouttekst of beschrijving | Aanbevolen in te grijpen |
|:--- |:--- |:--- |
| 10502 |Er is een fout opgetreden tijdens het openen van uw opslagaccount. |Wacht een paar minuten en probeer het opnieuw. Als het Hallo-fout zich blijft voordoen, neemt u contact opnemen met Microsoft ondersteuning voor de volgende stappen. |
| 40017 |Hallo back-upbewerking is mislukt omdat een volume dat is opgegeven in de back-upbeleid Hallo niet op Hallo-apparaat gevonden is. |Probeer de back-upbewerking hello, als hello fout zich blijft voordoen, neem contact op met Microsoft Support. voor de volgende stappen. |
| 40018 |Hallo back-upbewerking is mislukt omdat geen van de opgegeven in de back-upbeleid Hallo Hallo-volumes op Hallo-apparaat is gevonden. |Probeer de back-upbewerking hello, als hello fout zich blijft voordoen, neem contact op met Microsoft Support. voor de volgende stappen. |
| 390061 |Hallo systeem is bezet of niet beschikbaar. |Wacht een paar minuten en probeer het opnieuw. Als het Hallo-fout zich blijft voordoen, neemt u contact opnemen met Microsoft ondersteuning voor de volgende stappen. |
| 390143 |Er is een fout opgetreden met foutcode 390143. (Onbekende fout.) |Als het Hallo-fout zich blijft voordoen, neem contact met Microsoft Support voor de volgende stappen. |

## <a name="next-steps"></a>Volgende stappen
Als u tooresolve Hallo probleem [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) voor hulp. 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
