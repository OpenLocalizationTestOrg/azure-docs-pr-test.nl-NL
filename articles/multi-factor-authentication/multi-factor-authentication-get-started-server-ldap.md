---
title: aaaLDAP verificatie en Azure MFA-Server | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina die u helpt bij het implementeren van LDAP-verificatie en Azure multi-factor Authentication-Server.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: e1a68568-53d1-4365-9e41-50925ad00869
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 17a26b57dbf6afa2fcfdb3d19c5b5ba2987a9f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ldap-authentication-and-azure-multi-factor-authentication-server"></a>LDAP-verificatie en Azure multi-factor Authentication-Server
Standaard hello Azure multi-factor Authentication-Server is geconfigureerd tooimport of gebruikers van Active Directory synchroniseren. Kan het echter, de geconfigureerde toobind toodifferent LDAP-adreslijsten, zoals een ADAM-adreslijst of een specifieke Active Directory-domeincontroller zijn. Wanneer verbonden tooa directory via LDAP, hello Azure multi-factor Authentication-Server kan fungeren als een LDAP-proxy tooperform-verificaties. Daarnaast kunt u Hallo gebruik van LDAP-binding als een RADIUS-doel voor verificatie van gebruikers met IIS-verificatie vooraf, of voor primaire verificatie in hello Azure MFA-gebruikersportal.

Azure multi-factor Authentication als een LDAP-proxy toouse invoegen hello Azure multi-factor Authentication-Server tussen Hallo LDAP-client (bijvoorbeeld VPN-apparaat, toepassing) en Hallo LDAP-adreslijstserver. Hello Azure multi-factor Authentication-Server moet geconfigureerde toocommunicate met Hallo clientservers en Hallo LDAP-adreslijst. In deze configuratie hello Azure multi-factor Authentication-Server accepteert LDAP-aanvragen van clientservers en toepassingen en stuurt ze toohello doel LDAP directory server toovalidate Hallo primaire referenties. Als Hallo LDAP-adreslijst de primaire referenties hello verifieert, wordt Azure multi-factor Authentication wordt een tweede ID-verificatie wordt uitgevoerd en stuurt een reactie terug toohello LDAP-client. Hallo gehele verificatie slaagt alleen als zowel Hallo LDAP-serververificatie en verificatie van de tweede stap Hallo slaagt.

## <a name="configure-ldap-authentication"></a>LDAP-verificatie configureren
tooconfigure LDAP-verificatie, installatie hello Azure multi-factor Authentication-Server op een WindowsServer. Gebruik Hallo procedure te volgen:

### <a name="add-an-ldap-client"></a>Een LDAP-client toevoegen

1. Selecteer in hello Azure multi-factor Authentication-Server, Hallo LDAP-verificatie-pictogram in het linkermenu Hallo.
2. Controleer de Hallo **LDAP-verificatie inschakelen** selectievakje.

   ![LDAP-verificatie](./media/multi-factor-authentication-get-started-server-ldap/ldap2.png)

3. Op tabblad Clients Hallo Hallo TCP-poort en wijzigen SSL-poort als hello Azure multi-factor Authentication LDAP-service verbinding voor toonon standaard poorten toolisten voor LDAP-aanvragen maken moet.
4. Als u van plan LDAPS toouse van Hallo client toohello Azure multi-factor Authentication-Server bent, een SSL-certificaat moet worden geïnstalleerd op Hallo dezelfde server als de MFA-Server. Klik op **Bladeren** volgende toohello SSL vak van het certificaat en selecteer een certificaat toouse voor Hallo beveiligde verbinding.
5. Klik op **Add**.
6. Voer Hallo LDAP-Client toevoegen in het dialoogvenster Hallo IP-adres van het toestel hello, server of toepassing die toohello Server en een toepassingsnaam in (optioneel verifieert). de naam van de toepassing Hello wordt weergegeven in de Azure multi-factor Authentication-rapporten en kan worden weergegeven in verificatieberichten via SMS of mobiele App.
7. Controleer de Hallo **gebruikersovereenkomst vereist Azure multi-factor Authentication** vak als alle gebruikers zijn of worden geïmporteerd in Hallo Server en onderwerp tootwo stap verificatie. Als een groot aantal gebruikers nog niet is geïmporteerd in Hallo Server en/of vrijgesteld van verificatie in twee stappen zijn, laat u Hallo vakje uitgeschakeld. Zie Hallo MFA-Server help-bestand voor meer informatie over deze functie.

Herhaal deze stappen tooadd extra LDAP-clients.

### <a name="configure-hello-ldap-directory-connection"></a>Hallo LDAP-directory-verbinding configureren

Wanneer hello Azure multi-factor Authentication geconfigureerde tooreceive LDAP-verificaties is, moet deze als proxy die verificaties toohello LDAP-adreslijst. Tabblad Hallo-doel geeft daarom alleen één optie toouse grijs met een LDAP-doel.

1. tooconfigure hello LDAP-directory verbinding, klikt u op Hallo **Adreslijstintegratie** pictogram.
2. Selecteer op het tabblad Instellingen Hallo Hallo **Gebruik specifieke LDAP-configuratie** keuzerondje.
3. Selecteer **Bewerken...**
4. Vul in Hallo LDAP-configuratie bewerken in het dialoogvenster Hallo velden met Hallo vereiste informatie op tooconnect toohello LDAP-adreslijst. Beschrijvingen van Hallo velden zijn opgenomen in hello Azure multi-factor Authentication-Server help-bestand.

    ![Adreslijstintegratie](./media/multi-factor-authentication-get-started-server-ldap/ldap.png)

5. Hallo LDAP-verbinding testen door te klikken op Hallo **Test** knop.
6. Als Hallo LDAP-verbindingstest geslaagd is, klikt u op Hallo **OK** knop.
7. Klik op Hallo **Filters** tabblad Hallo Server is vooraf geconfigureerd tooload containers, beveiligingsgroepen en gebruikers van Active Directory. Als u verbinding tooa andere LDAP-adreslijst, moet u waarschijnlijk tooedit Hallo filters weergegeven. Klik op Hallo **Help** koppeling voor meer informatie over filters.
8. Klik op Hallo **kenmerken** tabblad Hallo Server is vooraf geconfigureerd toomap kenmerken van Active Directory.
9. Als u bent tooa verschillende LDAP directory of toochange Hallo vooraf geconfigureerde kenmerktoewijzingen binding, klikt u op **bewerken...**
10. Hallo kenmerken bewerken in het dialoogvenster wijzigen Hallo LDAP-kenmerktoewijzingen voor uw directory. Kenmerknamen kunnen worden getypt of geselecteerd door te klikken op Hallo **...** knop volgende tooeach veld. Klik op Hallo **Help** koppeling voor meer informatie over de kenmerken.
11. Klik op Hallo **OK** knop.
12. Klik op Hallo **Bedrijfsinstellingen** pictogram en selecteer Hallo **omzetting van gebruikersnaam** tabblad.
13. Als u tooActive Directory verbinding van een domein-server, laat u Hallo **gebruik Windows beveiligings-id's (SID's) voor overeenkomende gebruikersnamen** keuzerondje geselecteerd. Anders, selecteer Hallo **LDAP gebruiken kenmerk unieke id voor overeenkomende gebruikersnamen** keuzerondje. 

Wanneer Hallo **LDAP gebruiken kenmerk unieke id voor overeenkomende gebruikersnamen** keuzerondje is ingeschakeld, hello Azure multi-factor Authentication-Server probeert tooresolve elke gebruikersnaam tooa unieke id in Hallo LDAP-adreslijst. Een LDAP-zoekopdracht wordt uitgevoerd op Hallo gebruikersnaam kenmerken zijn gedefinieerd in Active Directory-integratie Hallo -> tabblad kenmerken. Wanneer een gebruiker zich verifieert, is Hallo gebruikersnaam omgezet toohello unieke id in Hallo LDAP-adreslijst. Hallo unieke id wordt gebruikt voor de overeenkomende Hallo gebruiker hello Azure multi-factor Authentication-gegevensbestand. Hierdoor kunnen niet-hoofdlettergevoelige vergelijkingen en lange en korte gebruikersnaamnotaties worden gebruikt.

Nadat u deze stappen hebt voltooid, geconfigureerd Hallo MFA-Server luistert op Hallo geconfigureerd poorten voor LDAP-aanvragen van Hallo-clients en besluiten als proxy voor die toohello LDAP-adreslijst voor verificatie aanvragen.

## <a name="configure-ldap-client"></a>LDAP-client configureren
tooconfigure hello LDAP-client gebruikt Hallo richtlijnen:

* Configureer uw toestel, server of toepassing tooauthenticate via LDAP toohello Azure multi-factor Authentication-Server alsof het uw LDAP-adreslijst. Gebruik Hallo dezelfde instellingen die u normaal gesproken tooconnect gebruikt rechtstreeks tooyour LDAP-adreslijst, met uitzondering van Hallo-servernaam of IP-adres van hello Azure multi-factor Authentication-Server.
* Hallo LDAP time-out too30 tot 60 seconden zo configureren dat er tijd toovalidate Hallo de referenties van gebruiker met de LDAP-adreslijst hello, Hallo tweede stap verificatie uitvoeren en hun reactie ontvangen reageren toohello LDAP-toegangsaanvraag.
* Als LDAPS wordt gebruikt, hello apparaat of de server Hallo LDAP-query's maken Hallo SSL-certificaat vertrouwen op Hallo Azure multi-factor Authentication-Server geïnstalleerd.

