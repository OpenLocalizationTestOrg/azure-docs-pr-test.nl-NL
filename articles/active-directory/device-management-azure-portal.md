---
title: aaaManaging apparaten met behulp van Azure portal - Hallo preview | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure portal toomanage apparaten.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>Apparaten beheert met Azure-portal Hallo - voorbeeld

>[!NOTE]
>Deze mogelijkheid is momenteel in de openbare preview. Toorevert worden voorbereid op of verwijder eventuele wijzigingen. Hallo-functie is beschikbaar in een abonnement voor Azure Active Directory (Azure AD) tijdens de openbare preview. Wanneer het Hallo-functie in het algemeen beschikbaar wordt, mogelijk bepaalde aspecten van de functie Hallo echter een Azure Active Directory premium-abonnement nodig.


Met Apparaatbeheer in Azure Active Directory (Azure AD), kunt u ervoor zorgen dat uw gebruikers toegang hebben tot de bronnen vanaf apparaten die voldoen aan uw standaarden voor beveiliging en naleving. 

Dit onderwerp:

- Wordt ervan uitgegaan dat u bekend met Hallo bent [inleiding toodevice management in Azure Active Directory](device-management-introduction.md)

- Biedt u informatie over het beheren van uw apparaten met behulp van Azure-portal Hallo


toomanage apparaten in hello Azure-portal, moet u tooclick **apparaten** in Hallo **beheren** sectie Hallo Hallo **Azure Active Directory** blade.

![Een apparaat met Intune beheren](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>Apparaatinstellingen configureren

uw apparaten met behulp van hello Azure-portal, moeten toobe toomanage ingeschreven of die lid zijn van tooAzure AD. Als beheerder, kunt u aanpassen Hallo proces van registreren en door apparaten te koppelen door het Hallo-apparaatinstellingen configureren.

![Een apparaat met Intune beheren](./media/device-management-azure-portal/22.png)


blade Hallo apparaat-instellingen kunt u tooconfigure:

- **Gebruikers kunnen apparaten tooAzure AD join** - deze instellingen kunt u tooselect Hallo gebruikers die deel kunnen nemen aan apparaten tooAzure AD. Hallo standaardwaarde is **alle**.

- **Aanvullende lokale beheerders op Azure AD die lid zijn van de apparaten** -kunt u Hallo-gebruikers die lokale beheerdersrechten op een apparaat krijgen. Gebruikers die zijn toegevoegd, worden toegevoegd toohello *Apparaatbeheerders* rol in Azure AD. Globale beheerders in Azure AD en eigenaren van de apparaten zijn lokale beheerdersrechten standaard toegekend. Deze optie is een premium edition-functie beschikbaar via producten zoals Azure AD Premium of Enterprise Mobility Suite (EMS) Hallo. 

- **Gebruikers kunnen hun apparaten registreren met Azure AD** -moet u deze instelling tooallow apparaten toobe geregistreerd in Azure AD tooconfigure. Als u selecteert **geen**, apparaten zijn niet toegestaan tooregister wanneer ze niet Azure AD zijn toegevoegd of hybride die lid zijn van Azure AD. Registratie bij Microsoft Intune of Mobile Device Management (MDM) voor Office 365 moet worden geregistreerd. Als u een van deze services hebt geconfigureerd **alle** is geselecteerd en **** is niet beschikbaar...

- **Multi-factor Auth toojoin apparaten vereisen** -kunt u kiezen of gebruikers zijn vereiste tooprovide een verificatie met tweede factor toojoin hun apparaat tooAzure AD. Hallo standaardwaarde is **Nee**. Het is raadzaam om meervoudige verificatie vereisen wanneer een apparaat wordt geregistreerd. Voordat u multi-factor authentication voor deze service inschakelt, moet u ervoor zorgen dat multi-factor authentication-server is geconfigureerd voor het Hallo-gebruikers die hun apparaten registreren. Zie voor meer informatie over andere Azure multi-factor authentication-services [aan de slag met Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md). 

- **Maximum aantal apparaten** -deze instelling kunt u tooselect Hallo maximum aantal apparaten dat een gebruiker in Azure AD hebben kan. Als een gebruiker dit quotum bereikt, zijn ze niet kunnen tooadd extra apparaten totdat een of meer van de bestaande apparaten Hallo worden verwijderd. Hallo apparaat aanhalingsteken worden geteld voor alle apparaten die Azure AD zijn toegevoegd of Azure AD vandaag geregistreerd. de standaardwaarde Hallo is **20**.

- **Gebruikers kunnen instellingen en app-gegevens synchroniseren via apparaten** -, deze instelling is standaard ingesteld te****. Specifieke gebruikers of groepen of alle selecteren die u kan de instellingen en toosync van app-gegevens van de gebruiker Hallo over hun Windows 10-apparaten. Meer informatie over de werking van synchronisatie in Windows 10.
Deze optie is een premium-functie beschikbaar via producten zoals Azure AD Premium of Enterprise Mobility Suite (EMS) Hallo.
 
    ![Een apparaat met Intune beheren](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>Apparaten zoeken

Als een beheerder hebt in hello Azure-portal u twee opties toolocate geregistreerd en die lid zijn van apparaten:

- **Alle apparaten** in Hallo **beheren** sectie Hallo **apparaten** blade  

    ![Alle apparaten](./media/device-management-azure-portal/41.png)


- **Apparaten** in Hallo **beheren** gedeelte van een **gebruiker** blade
 
    ![Alle apparaten](./media/device-management-azure-portal/43.png)



Met beide opties, kun je tooa weergeven die:


- Hiermee kunt u toosearch voor apparaten met de weergavenaam Hallo als filter.

- Biedt u gedetailleerd overzicht van geregistreerde en gekoppelde apparaten

- Hiermee kunt u tooperform algemene taken
   

![Alle apparaten](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>Taken voor het beheer van apparaten

Als beheerder, kunt u beheren Hallo ingeschreven of die lid zijn van apparaten. Deze sectie vindt u informatie over algemene taken.


**Een apparaat met Intune beheren** -als u een Intune-beheerder bent, kunt u beheren met apparaten die zijn gemarkeerd als **Microsoft Intune**. Een beheerder kan aanvullende apparaat zien 

![Een apparaat met Intune beheren](./media/device-management-azure-portal/31.png)


**Inschakelen / uitschakelen van een Azure AD-apparaat**

tooenable of een apparaat uitschakelen, moet u een globale beheerder toobe in Azure AD. Als u een apparaat wordt voorkomen dat een apparaat toegang tot uw Azure AD-resources.  toodisable Hallo-apparaat, kunt u klikken op *...* Klik op Hallo-apparaat voor meer informatie.

 
![Een apparaat met Intune beheren](./media/device-management-azure-portal/33.png)

Als u een apparaat wijzigt Hallo-status in Hallo **ingeschakeld** kolom te**Nee**.

![Een apparaat uitschakelen](./media/device-management-azure-portal/32.png)


**Een Azure AD-apparaat verwijderen** -toodelete een apparaat, moet u een globale beheerder toobe in Azure AD.  
Een apparaat verwijderen:
 
- Voorkomen dat een apparaat toegang tot uw Azure AD-resources 

- Hiermee verwijdert u alle gegevens die aangesloten toohello van het apparaat, bijvoorbeeld zijn, BitLocker-sleutels voor Windows-apparaten  

- Hiermee geeft u een niet-herstelbare activiteit en wordt niet aanbevolen, tenzij deze vereist is

Als een apparaat wordt beheerd door een andere instantie voor beheer van (bijvoorbeeld Microsoft Intune), zorg dat het Hallo-apparaat is gewist / buiten gebruik gesteld voordat u Hallo-apparaat verwijdert in Azure AD.

U kunt ook selecteren '...' toodelete hello apparaat of klik op het Hallo-apparaat voor aanvullende informatie
 
![Een apparaat verwijderen](./media/device-management-azure-portal/34.png)


**Weergeven of kopiëren van apparaat-ID** -kunt u een apparaat-ID tooverify Hallo apparaat-ID details op Hallo-apparaat of met behulp van PowerShell tijdens het oplossen van problemen. tooaccess Hallo kopie optie, klikt u op Hallo-apparaat.

![Een apparaat-ID weergeven](./media/device-management-azure-portal/35.png)
  

**Weergeven of kopiëren van BitLocker-sleutels** -als u beheerder bent, u bekijken kunt en kopiëren Hallo BitLocker-sleutels toohelp gebruikers toorecover hun versleutelde station. Deze sleutels zijn alleen beschikbaar voor Windows-apparaten die zijn versleuteld en hun sleutels hebt opgeslagen in Azure AD. Bij het openen van de details van Hallo-apparaat, kunt u deze sleutels kopiëren.
 
![BitLocker-sleutels weergeven](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>Controlelogboeken


Hallo apparaat activiteiten zijn beschikbaar via Hallo activiteitenlogboeken. Dit omvat activiteiten die zijn geactiveerd door Hallo device registration-service of door Hallo gebruiker:

- Maken van het apparaat en het toevoegen van eigenaars/gebruikers op Hallo-apparaat

- Wijzigingen toodevice instellingen

- Apparaatbewerkingen zoals het verwijderen of bijwerken van een apparaat
 
De vermelding punt toohello controle van gegevens is **controlelogboeken** in Hallo **activiteit** sectie Hallo **apparaten* blade.

![Controlelogboeken](./media/device-management-azure-portal/61.png)


Een controlelogboek heeft een standaardlijstweergave die het volgende laat zien:

- Hallo-datum en tijd van Hallo-instantie

- Hallo doelen

- Hallo initiator / actor (die) van een activiteit

- Hallo-activiteit (wat)

![Controlelogboeken](./media/device-management-azure-portal/63.png)

U kunt de lijstweergave Hallo aanpassen door te klikken op **kolommen** op Hallo-werkbalk.
 
![Controlelogboeken](./media/device-management-azure-portal/64.png)


toonarrow omlaag Hallo tooa gegevensniveau dat geldt voor u, kunt u Hallo audit gegevens filteren met behulp van de volgende velden Hallo gerapporteerd:

- Catergory
- Resourcetype van activiteit
- Activiteit
- Datumbereik
- doel
- Gestart door (Actor)

Bovendien toohello filters, u kunt zoeken naar specifieke vermeldingen.

![Controlelogboeken](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>Volgende stappen

* [Inleiding toodevice management in Azure Active Directory](device-management-introduction.md)



