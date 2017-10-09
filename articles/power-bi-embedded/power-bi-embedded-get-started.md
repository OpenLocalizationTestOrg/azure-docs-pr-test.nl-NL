---
title: aaaGet de slag met Microsoft Power BI Embedded
description: Power BI Embedded, voeg interactieve Power BI-rapporten toe aan uw BI-toepassing (Business Intelligence)
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a>Aan de slag met Microsoft Power BI Embedded

**Power BI Embedded** een Azure-service is dat Hiermee toepassing ontwikkelaars tooadd interactieve Power BI-aan hun eigen toepassingen rapporten. **Power BI Embedded** werkt met bestaande toepassingen zonder te hoeven ontwerpen of wijzigen van Hallo manier waarop gebruikers zich aanmelden.

Bronnen voor **Microsoft Power BI Embedded** zijn ingericht via Hallo [Azure ARM API's](https://msdn.microsoft.com/library/mt712306.aspx). In dit geval Hallo-bron die u inricht is een **Power BI-Werkruimteverzameling**.

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a>Een werkruimteverzameling maken

Een **Werkruimteverzameling** Hallo op het hoogste niveau Azure-resource en een container voor Hallo-inhoud die wordt ingesloten in uw toepassing is. U kunt op twee manieren een **werkruimteverzameling** maken:

* Handmatig met behulp van hello Azure Portal
* Programmatisch met behulp van hello Azure Resource Manager (arm) API 's

We doorlopen Hallo stappen toobuild een **Werkruimteverzameling** met behulp van hello Azure-Portal.

1. Open de **Azure-portal**: [http://portal.azure.com](http://portal.azure.com) en meld u aan.
2. Klik op **+ nieuw** op Hallo boven in het venster.
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. Klik onder **Gegevens en analyse** op **Power BI Embedded**.
4. Op Hallo **Blade Werkruimteverzameling**, Geef informatie op Hallo vereist. Informatie over **prijzen** vindt in [Prijzen van Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. Klik op **Create**.

Hallo **Werkruimteverzameling** duurt enkele ogenblikken tooprovision. Wanneer voltooid, wordt u geleid toohello **Blade Werkruimteverzameling**.

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

Hallo **Blade maken** Hallo-informatie die u nodig hebt toocall Hallo API's die werkruimten maken en implementeren van inhoud toothem bevat.

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a>Toegangssleutels voor Power BI API

Een van de belangrijkste stukjes informatie die nodig is toocall Power BI REST-API's Hallo HALLO hallo zijn **toegangstoetsen**. Dit zijn de gebruikte toogenerate hello **app-tokens** die zijn gebruikt tooauthenticate uw API-aanvragen. tooview uw **toegangssleutels**, klikt u op **toegangssleutels** op Hallo **Instellingenblade**. Voor meer informatie over **app-tokens** verwijzen wij u naar [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md) (Verifiëren en autoriseren met Power BI Embedded).

   ![](media/power-bi-embedded-get-started/access-keys.png)

U ziet dat u twee sleutels hebt.

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

Kopieer deze sleutels en sla ze veilig op in uw toepassing. Het is heel belangrijk dat u deze sleutels behandelen net als een wachtwoord, omdat ze bieden toegang tot tooall Hallo inhoud in uw **Werkruimteverzameling**.

Hoewel er twee sleutels worden vermeld, hebt u er slechts één tegelijk nodig. de tweede sleutel Hallo wordt geboden zodat u de sleutels regelmatig opnieuw genereert kunt zonder dat toohello-access-service wordt onderbroken.

Nu u een exemplaar van Power BI voor uw toepassing en **toegangssleutels** hebt, kunt u een rapport in uw eigen app importeren. Voordat u meer informatie over hoe maken Power BI-gegevenssets en rapporten tooembed in tooimport een verslag Hallo volgende sectie wordt beschreven in een app.

## <a name="working-with-workspaces"></a>Werken met werkruimten

Nadat u uw werkruimteverzameling hebt gemaakt, moet u toocreate een werkruimte die wordt uw rapporten en gegevenssets bevatten. een werkruimte toocreate, moet u toouse hello [Post Worksapce REST-API](https://msdn.microsoft.com/library/azure/mt711503.aspx).

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a>Power BI-gegevenssets en rapporten tooembed maken in een app met behulp van Power BI Desktop

Nu dat u een exemplaar van Power BI voor uw toepassing hebt gemaakt en hebben **toegangstoetsen**, moet u toocreate Hallo Power BI-gegevenssets en rapporten die u tooembed wilt. Gegevenssets en rapporten kunnen worden gemaakt met behulp van **Power BI Desktop**. U kunt [Power BI Desktop gratis](https://go.microsoft.com/fwlink/?LinkId=521662) downloaden. Of, tooquickly aan de slag, kunt u downloaden Hallo [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).

> [!NOTE]
> meer informatie over hoe toolearn toouse **Power BI Desktop**, Zie [aan de slag met Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).

Met **Power BI Desktop**, u verbinding maken met gegevensbron tooyour door het importeren van een kopie van gegevens in Hallo **Power BI Desktop** of toohello gegevens rechtstreeks verbinding maken met behulp van de gegevensbron **DirectQuery**.

Hier volgen Hallo verschillen tussen het gebruik van **importeren** en **DirectQuery**.

| Importeren | DirectQuery |
| --- | --- |
| Tabellen, kolommen *en gegevens* worden geïmporteerd of gekopieerd naar **Power BI Desktop**. Als u met visualisaties werkt, **Power BI Desktop** een kopie van Hallo gegevens opvraagt. toosee eventueel opgetreden toohello onderliggende gegevens wijzigen, moet u vernieuwen of importeren, een volledige, actuele gegevensset opnieuw. |Alleen *tabellen en kolommen* worden geïmporteerd of gekopieerd naar **Power BI Desktop**. Als u met visualisaties werkt, **Power BI Desktop** query's onderliggende gegevensbron, wat betekent dat u altijd actuele gegevens bekijkt hello. |

Zie voor meer informatie over het maken van verbinding tooa gegevensbron [Connect tooa gegevensbron](power-bi-embedded-connect-datasource.md).

Nadat u uw werk in **Power BI Desktop** hebt opgeslagen, wordt een PBIX-bestand gemaakt. Dit bestand bevat het rapport. Bovendien, als u gegevens Hallo PBIX bevat importeert Hallo volledige gegevensset of als u **DirectQuery**, Hallo PBIX bevat een gegevensset-schema. U Hallo PBIX programmatisch implementeren in de werkruimte op basis van Hallo [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).

> [!NOTE]
> **Power BI Embedded** heeft aanvullende API's toochange Hallo-server en database dat uw gegevensset tooand set accountreferenties die Hallo gegevensset wijst tooconnect tooyour database gebruikt. Zie [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) en [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).

## <a name="create-power-bi-datasets-and-reports-using-apis"></a>Power BI-gegevenssets en -rapporten maken met behulp van API's

### <a name="datsets"></a>Gegevenssets

U kunt de gegevenssets in Power BI Embedded met Hallo REST-API maken. Vervolgens kunt u gegevens naar uw gegevensset pushen. Hiermee kunt u toowork met gegevens zonder Hallo van Power BI Desktop. Zie [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Gegevenssets posten) voor meer informatie.

### <a name="reports"></a>Rapporten

U kunt een rapport maken uit een gegevensset rechtstreeks in uw toepassing met behulp van Hallo JavaScript-API. Zie [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Een nieuw rapport maken uit een gegevensset in Power BI Embedded) voor meer informatie.

## <a name="see-also"></a>Zie ook

[Aan de slag met het voorbeeld](power-bi-embedded-get-started-sample.md)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Een rapport insluiten](power-bi-embedded-embed-report.md)  
[Een nieuw rapport maken uit een gegevensset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Rapporten opslaan](power-bi-embedded-save-reports.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)

