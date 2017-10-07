---
title: aaaCustomize stijlen in de ontwikkelaarsportal Hallo in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toomodify Hallo stijlen gebruikt voor alle pagina's in Azure API Management Hallo developer-Portal.
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Hallo-stijl van de ontwikkelaarsportal Hallo in Azure API Management aanpassen
Er zijn drie manieren Hallo toocustomize ontwikkelaarsportal in Azure API Management:

* [Hallo-inhoud van statische pagina's en pagina-elementen voor lay-out bewerken][modify-content-layout]
* [Hallo-stijlen worden gebruikt voor pagina-elementen over Hallo-portal voor ontwikkelaars werken] [ customize-styles] (uitgelegd in deze handleiding)
* [Hallo-sjablonen die worden gebruikt voor pagina's die worden gegenereerd door Hallo portal wijzigen] [ portal-templates] (bijvoorbeeld API docs, producten, gebruikersverificatie, enz.)

## <a name="change-headers-styling"></a>Hallo-stijl van pagina-elementen wijzigen

Hallo worden kleuren, lettertypen, grootten, afstanden en andere stijlelementen van pagina's in de portal Hallo gedefinieerd met stijlregels. 

Het bewerken van stijlregels Hallo is uitgevoerd van Hallo **ontwikkelaarsportal** tijdens wordt aangemeld als beheerder. tooget er eerst hello Azure Portal openen en op **publicatieportal** van Hallo service werkbalk van uw exemplaar van API Management.

![Publicatieportal][api-management-management-console]

Klik vervolgens op **ontwikkelaarsportal** op Hallo rechtsboven. 

![Developer portal-koppeling op Hallo publicatieportal][api-management-pp-dp-link]

werkbalk voor aanpassing van tooopen Hallo Beweeg de muis over Hallo aanpassing pictogram (of selecteert u het) en vervolgens klikken op 'stijlen' hello werkbalk van.

![Werkbalkknop Aanpassen][api-management-customization-toolbar-button]

Er zijn twee belangrijkste methode voor het bewerken van stijlregels van - kunt u bekijkt hello-lijst van alle Hallo stijlregels die ergens worden gebruikt die wordt standaard weergegeven en zo nodig een stijl wijzigen of u kunt kiezen **selecteren van een element op de pagina Hallo** en vervolgens Klik ergens op Hallo pagina toosee alleen Hallo stijlen voor dat element.

![Werkbalk voor aanpassing][api-management-customization-toolbar]

Klik op Hallo **selecteren van een element op de pagina Hallo** optie voor dit voorbeeld.  Elementen worden nu gemarkeerd als u de muisaanwijzer met Hallo muis toosignify stijlen van het welke element u zou gaan bewerken als u hebt geklikt. Verplaatsing Hallo muis over Hallo tekst in het Hallo-header (doorgaans moet u de bedrijfsnaam Hallo hier) en klik vervolgens op het. Een set benoemde en gecategoriseerde stijlregels wordt weergegeven in de stijleditor Hallo. Elke regel geeft een stijleigenschap van het geselecteerde element Hallo. Bijvoorbeeld: voor Hallo koptekst hierboven hebt geselecteerd, Hallo grootte van de tekst hello wordt @font-size-h1 terwijl Hallo-naam van Hallo lettertype met alternatieven in @headings-font-family.

> Als u bekend met bent [bootstrap][bootstrap], deze regels zijn in feite [LESS-variabelen] [ LESS variables] binnen Hallo bootstrapthema dat wordt gebruikt door Hallo portal voor ontwikkelaars.
> 
> 

Laten we Hallo kleur van de koptekst Hallo wijzigen. Selecteer Hallo vermelding in Hallo  **@headings-color**  veld en type **#000000**. Dit is de hexadecimale code Hallo voor Hallo kleur zwart. Als u dit doet, ziet u dat er een vierkante kleurenindicator wordt weergegeven aan einde van het tekstvak Hallo Hallo. Als u deze indicator klikt, kunt een kleurenkiezer een kleur u toochoose.

![Kleurenkiezer][api-management-customization-toolbar-color-picker]

Wijzigingen worden weergegeven in realtime, zoals u ze, maar zichtbaar alleen tooadministrators zijn. toomake deze wijzigingen zichtbaar tooeveryone, klikt u op Hallo **publiceren** knop in Hallo stijleditor en bevestigt u Hallo wijzigingen.

![Het menu Publish][api-management-customization-toolbar-publish-form]

> de toochange Hallo stijl regels die van toepassing tooany ander element op de pagina hello, volg Hallo dezelfde procedure als u gedaan voor Hallo-header. Klik op **selecteren van een element op de pagina Hallo** van Hallo stijleditor, selecteer Hallo element u geïnteresseerd bent in en start wijzigen Hallo waarden van Hallo stijlregels weergegeven op het welkomstscherm.
> 
> 


## <a name="next-steps"> </a>Volgende stappen
* Meer informatie over hoe toocustomize Hallo inhoud van developer-portal-pagina's met behulp van [Developer portal sjablonen](api-management-developer-portal-templates.md).

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
