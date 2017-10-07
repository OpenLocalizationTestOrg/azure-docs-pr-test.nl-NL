---
title: aaaTroubleshooting hello Azure-hulpprogramma voor importeren/exporteren | Microsoft Docs
description: Meer informatie over van Hallo voorkomende problemen die worden weergegeven wanneer u hello Azure-hulpprogramma voor importeren/exporteren en hoe toohandle ze.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 5445cefe2703edf4d9d285f761433b7b66d8cb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren
Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren retourneert foutberichten worden weergegeven als deze wordt uitgevoerd in de problemen. Dit onderwerp worden enkele veelvoorkomende problemen die gebruikers kunnen uitvoeren in.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Een kopieersessie is mislukt, wat ik moet nemen?  
 Wanneer een sessie kopiëren is mislukt, zijn er twee opties:  
  
 Als het Hallo-fout is een herstelbare, bijvoorbeeld als de netwerkshare Hallo offline was voor een korte periode en nu weer online is, kunt u Hallo kopieersessie hervatten. Als het Hallo-fout is geen herstelbare, bijvoorbeeld als u verkeerde bronmap bestand Hallo opgegeven in de opdrachtregelparameters Hallo, moet u tooabort Hallo kopieersessie. Zie [harde schijven voorbereiden voor een Import-taak](storage-import-export-tool-preparing-hard-drives-import-v1.md) voor meer informatie over wordt hervat en wordt afgebroken sessies kopiëren.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>Ik kan hervatten of afbreken van een kopieersessie.  
 Als Hallo kopieersessie Hallo eerste kopieersessie voor een station, wordt fout het Hallo-bericht moet status: "hello eerste kopieersessie kan niet worden hervat of afgebroken." In dit geval kunt u Hallo oude journaalbestand verwijderen en Voer Hallo opdracht opnieuw uit.  
  
 Als een kopieersessie is de eerste is voor een station niet hello, kan altijd hervat of afgebroken.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>Hallo journal-bestand is verbroken, kan ik nog steeds Hallo taak maken?  
 Hallo journal-bestand voor een station Hallo volledige informatie van het kopiëren van schijf toothis bevat en dit is nodig tooadd meer bestanden toohello station en gebruikte toocreate een import-taak kan worden. Als Hallo journal-bestand verloren gegaan is, hebt u tooredo alle Hallo kopie-sessies voor Hallo-station.  
  
## <a name="next-steps"></a>Volgende stappen
 
* [Instellen van hello azure import/export-hulpprogramma](storage-import-export-tool-setup-v1.md)   
* [Harde schijven voorbereiden voor een importtaak](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [De taakstatus controleren met kopielogboekbestanden](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Een importtaak herstellen](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Een exporttaak herstellen](storage-import-export-tool-repairing-an-export-job-v1.md)
