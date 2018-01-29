---
title: Azure Security Center-zelfstudie - Reageren op beveiligingsincidenten | Microsoft Docs
description: Azure Security Center-zelfstudie - Reageren op beveiligingsincidenten
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 181e3695-cbb8-4b4e-96e9-c4396754862f
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/07/2018
ms.author: yurid
ms.custom: mvc
ms.openlocfilehash: b6adf4bec2d9f92ee3cde9c73a03beb5a58c3f3f
ms.sourcegitcommit: 6fb44d6fbce161b26328f863479ef09c5303090f
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/10/2018
---
# <a name="tutorial-respond-to-security-incidents"></a>Zelfstudie: Reageren op beveiligingsincidenten
Security Center analyseert voortdurend de werkbelasting van uw hybride cloud met behulp van geavanceerde analysen en bedreigingsinformatie, om u te waarschuwen voor schadelijke activiteiten. Bovendien kunt u waarschuwingen van andere beveiligingsproducten en -services integreren in Security Center en aangepaste waarschuwingen maken op basis van uw eigen indicatoren of informatiebronnen. Wanneer een waarschuwing is gegenereerd, moet onmiddellijk actie worden ondernomen om het probleem te onderzoeken en te herstellen. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Beveiligingswaarschuwingen onderzoeken
> * Verder onderzoek uitvoeren om de oorzaak en het bereik van een beveiligingsincident te bepalen
> * Zoek beveiligingsgegevens die bij het onderzoek kunnen helpen

Als u nog geen abonnement op Azure hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) aan voordat u begint.

## <a name="prerequisites"></a>Vereisten
Om de functies in deze zelfstudie te doorlopen, moet u zich in de Standard-prijscategorie van Security Center bevinden. U kunt Security Center Standard de eerste 60 dagen kosteloos proberen. In de snelstartgids [Onboard your Azure subscription to Security Center Standard](security-center-get-started.md) (Uw Azure-abonnement registreren voor Security Center Standard) wordt u begeleid bij het upgraden naar Standard.

## <a name="triage-security-alerts"></a>Beveiligingswaarschuwingen onderzoeken
Security Center biedt een overkoepelend overzicht van alle beveiligingswaarschuwingen. Beveiligingswaarschuwingen worden gerangschikt op basis van de ernst, en wanneer mogelijke worden gerelateerde waarschuwingen samengevoegd in één beveiligingsincident. Bij het uitsorteren van waarschuwingen en incidenten, gaat u als volgt te werk:

- Negeer waarschuwingen waarvoor geen verdere actie is vereist, bijvoorbeeld als de waarschuwing onterecht is
- Los bekende aanvallen op, bijvoorbeeld wanneer netwerkverkeer wordt geblokkeerd vanuit een schadelijke IP-adres
- Bepaal welke waarschuwingen verder moeten worden onderzocht


1. Selecteer in het hoofdmenu van Security Center onder **DETECTIE** de optie **Beveiligingswaarschuwingen**:

  ![Beveiligingswaarschuwingen](./media/tutorial-security-incident/tutorial-security-incident-fig1.png)  

2. Klik in de lijst met waarschuwingen op een beveiligingsincident, dus een verzameling waarschuwingen, voor meer informatie over dit incident. **Veiligheidsincident gedetecteerd** wordt geopend.

  ![Beveiligingsincident](./media/tutorial-security-incident/tutorial-security-incident-fig2.png)

3. Bovenin dit scherm staat de beschrijving van het incident, met de lijst van waarschuwingen die deel uitmaken van dit incident. Klik op de waarschuwing die u verder wilt onderzoeken, voor meer informatie.

  ![Beveiligingsincident](./media/tutorial-security-incident/tutorial-security-incident-fig3.png)

  Het type waarschuwing kan verschillen. Lees [Beveiligingswaarschuwingen in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) voor meer informatie over het type waarschuwing en mogelijke herstelstappen. Voor waarschuwingen die veilig kunnen worden genegeerd, klikt u met de rechtermuisknop op de waarschuwing en selecteert u de optie **Sluiten**:

  ![Waarschuwing](./media/tutorial-security-incident/tutorial-security-incident-fig4.png)

4. Als de hoofdoorzaak en het bereik van de schadelijke activiteit onbekend is, gaat u verder met de volgende stap om verder onderzoek te doen.

## <a name="investigate-an-alert-or-incident"></a>Een waarschuwing of incident onderzoeken
1. Klik op de pagina **Beveiligingswaarschuwing** op de knop **Onderzoek starten** (als u al bent begonnen, verandert de naam in **Onderzoek voortzetten**).

  ![Onderzoek](./media/tutorial-security-incident/tutorial-security-incident-fig5.png)

  De onderzoekskaart is een grafische weergave van de entiteiten die zijn verbonden met deze beveiligingswaarschuwing of dit incident. Door op een entiteit in de kaart te klikken, toont de informatie over die entiteit nieuwe entiteiten en wordt de kaart uitgebreid. De eigenschappen van de entiteit die in de kaart is geselecteerd, zijn gemarkeerd in het deelvenster aan de rechterkant van de pagina. Welke informatie op elk tabblad beschikbaar is, is afhankelijk van de geselecteerde entiteit. Bekijk tijdens het onderzoek alle relevante informatie om meer inzicht te krijgen in de tactiek van de aanvaller.

2. Als u meer bewijs nodig hebt of meer onderzoek moet verrichten voor entiteiten die tijdens het onderzoek zijn gevonden, gaat u verder met de volgende stap.

## <a name="search-data-for-investigation"></a>Gegevens zoeken voor onderzoek

Met de zoekmogelijkheden van Security Center kunt u meer bewijs van gecompromitteerde systemen zoeken en meer informatie over de entiteiten die deel uitmaken van het onderzoek.

Als u een zoekopdracht wilt uitvoeren, opent u het dashboard van **Security Center**, klikt u in het linkernavigatievenster op **Zoeken**, selecteert u de werkruimte die de entiteiten bevat die u wilt zoeken, typt u de zoekopdracht en klikt u op de zoekknop.

## <a name="clean-up-resources"></a>Resources opschonen
Andere snelstartgidsen en zelfstudies in deze verzameling zijn gebaseerd op deze snelstartgids. Als u de volgende snelstartgidsen en zelfstudies ook wilt doornemen, blijf dan de prijscategorie Standard gebruiken en houd automatische inrichting ingeschakeld. Als u niet wilt doorgaan of wilt terugkeren naar de laag gratis:

1. Ga terug naar het hoofdmenu van Security Center en selecteer **Beveiligingsbeleid**.
2. Selecteer het abonnement of het beleid dat u wilt terugzetten op Gratis. **Beveiligingsbeleid** wordt geopend.
3. Selecteer onder **BELEIDSONDERDELEN** de optie **Prijscategorie**.
4. Selecteer **Gratis** om het abonnement te wijzigen van de Standard-laag in de Gratis laag.
5. Selecteer **Opslaan**.

Als u automatisch inrichten wilt uitschakelen:

1. Ga terug naar het hoofdmenu van Security Center en selecteer **Beveiligingsbeleid**.
2. Selecteer het abonnement waarvoor u automatisch inrichten wilt uitschakelen.
3. Ga naar **Beveiligingsbeleid – Gegevensverzameling** en selecteer onder **Onboarding** de optie **Uit** om automatisch inrichten uit te schakelen.
4. Selecteer **Opslaan**.

>[!NOTE]
> Wanneer u automatische inrichting uitschakelt, wordt MMA niet verwijderd van Azure-VM's waarop de agent is ingericht. Door automatische inrichting uit te schakelen, wordt de beveiligingsbewaking voor uw resources beperkt.
>

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd over Security Center-functies waarmee u kunt reageren op beveiligingsincidenten, zoals:

> [!div class="checklist"]
> * Beveiligingsincident dat een aggregatie is van gerelateerde waarschuwingen voor een resource
> * Onderzoekskaart die een grafische weergave is van de entiteiten die zijn verbonden met een beveiligingswaarschuwing of incident
> * Zoekmogelijkheden om meer bewijs te vinden van gecompromitteerde systemen

Voor meer informatie over de onderzoeksfunctie van het Security Center raadpleegt u:

> [!div class="nextstepaction"]
> [Incidenten analyseren en onderzoeken](security-center-investigation.md)
