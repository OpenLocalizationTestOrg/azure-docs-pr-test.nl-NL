---
title: Verificatie met Amazon Web Services aaaConfigure | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate en een AWS-referentie voor runbooks in Azure Automation beheren van AWS-resources te valideren.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: AWS-verificatie, AWS configureren
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1e312df2422d9da3cd3331fe01aeaa3a43c8b9d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>Runbooks met Amazon Web Services verifiëren
Het automatiseren van algemene taken met resources in Amazon Web Services (AWS) kan worden bewerkstelligd met Automation-runbooks in Azure.  U kunt vele taken in AWS automatiseren met Automation-runbooks, net zoals u dit kunt met resources in Azure.  U hebt slechts twee dingen nodig:

* Een AWS-abonnement en een set referenties.  Het gaat dan met name om uw AWS-toegangssleutel en de geheime sleutel.  Raadpleeg voor meer informatie artikel Hallo [AWS-referenties](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).
* Een Azure-abonnement en een Automation-account.  Raadpleeg voor meer informatie over het instellen van een Azure Automation-account Hallo artikel [configureren Azure uitvoeren als-Account](automation-sec-configure-azure-runas-account.md).  

tooauthenticate met AWS, moet u een set AWS-referenties tooauthenticate uw runbooks die worden uitgevoerd van Azure Automation. Als u al een Automation-account gemaakt hebt en u wilt dat toouse die tooauthenticate met AWS, kunt u de stappen in de volgende sectie Hallo Hallo volgen.  Als u een account toodedicated voor runbooks gericht op AWS-resources wilt, moet eerst maakt u een nieuw [Automation-account](automation-offering-get-started.md) (overslaan Hallo optie toocreate een service-principal) en volgt u onderstaande stappen voor Hallo.

## <a name="configure-automation-account"></a>Automation-account configureren
Voor Azure Automation toocommunicate met AWS, u eerst uw AWS-referenties voor tooretrieve nodig en deze opslaan als assets in Azure Automation.  Uitvoeren van de volgende stappen uit die worden beschreven in AWS-document Hallo Hallo [toegangssleutels beheren voor uw AWS-Account](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate een toegangssleutel en kopieer Hallo **toegangssleutel-ID** en **geheime toegangssleutel** (download desgewenst uw sleutelbestand toostore het ergens veilig).

Nadat u hebt gemaakt en uw AWS-beveiligingssleutels gekopieerd, moet u een referentieasset met een Azure Automation-account toosecurely toocreate slaan en ernaar te verwijzen met uw runbooks.  Hallo stappen in de sectie Hallo **toocreate een nieuwe referentie** in Hallo [Referentieassets in Azure Automation](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) artikel en Voer Hallo volgende informatie:

1. In Hallo **naam** Voer **AWScred** of een geschikte waarde uw naamgevingsstandaarden.  
2. In Hallo **gebruikersnaam** type vak uw **toegangs-ID** en uw **geheime toegangssleutel** in Hallo **wachtwoord** en **bevestigen wachtwoord** vak.   

## <a name="next-steps"></a>Volgende stappen
* Bekijken Hallo oplossing artikel [implementatie van een virtuele machine in Amazon Web Services automatiseren](automation-scenario-aws-deployment.md) toolearn hoe toocreate runbooks tooautomate in AWS taken.

