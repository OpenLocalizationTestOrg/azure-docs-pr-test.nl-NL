---
title: 'Azure AD Connect: Hallo SSL-certificaat bijwerken voor een farm met Active Directory Federation Services (AD FS) | Microsoft Docs'
description: Dit document details Hallo stappen tooupdate Hallo SSL-certificaat van een AD FS-farm met behulp van Azure AD Connect.
services: active-directory
keywords: Azure ad connect, AD FS ssl-update, adfs-certificaat updates, AD FS-certificaat wijzigen, nieuwe AD FS-certificaat, AD FS-certificaat, update AD FS ssl-certificaat en update ssl-certificaat adfs AD FS ssl-certificaat, AD FS, ssl, certificaat, AD FS-service configureren certificaat voor serviceberichten, update-federation, federatie configureren, aad connect
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>Hallo SSL-certificaat voor een farm met Active Directory Federation Services (AD FS) bijwerken

## <a name="overview"></a>Overzicht
Dit artikel wordt beschreven hoe u Azure AD Connect tooupdate Hallo SSL-certificaat voor een farm met Active Directory Federation Services (AD FS) kunt gebruiken. Zelfs als Hallo gebruiker aanmelden methode geselecteerd geen AD FS is, kunt u hello Azure AD Connect-hulpprogramma tooeasily update Hallo SSL-certificaat voor Hallo AD FS-farm.

U kunt de hele bewerking hello om SSL-certificaat voor Hallo AD FS-farm bij te werken voor alle federatieve en -servers voor Webtoepassingsproxy (WAP) in drie eenvoudige stappen uitvoeren:

![Drie stappen](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>toolearn meer informatie over de certificaten die worden gebruikt door AD FS, Zie [Understanding-certificaten die worden gebruikt door AD FS](https://technet.microsoft.com/library/cc730660.aspx).

## <a name="prerequisites"></a>Vereisten

* **AD FS-Farm**: Zorg ervoor dat uw AD FS-farm op basis van Windows Server 2012 R2 of hoger.
* **Azure AD Connect**: Zorg ervoor dat Hallo versie van Azure AD Connect is 1.1.443.0 of hoger. U Hallo taak **Update AD FS SSL-certificaat**.

![SSL-taak bijwerken](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>Stap 1: Geef informatie op AD FS-farm

Azure AD Connect probeert automatisch door tooobtain informatie over Hallo AD FS-farm:
1. Het uitvoeren van query's is Hallo Farmgegevens vanaf AD FS (WindowsServer 2016 of hoger).
2. Verwijzende Hallo-informatie uit de vorige wordt uitgevoerd, worden lokaal opgeslagen met Azure AD Connect.

U kunt Hallo lijst met servers die worden weergegeven door het toevoegen of verwijderen van Hallo servers tooreflect Hallo huidige configuratie van Hallo AD FS-farm kunt wijzigen. Zodra het Hallo-servergegevens is opgegeven, geeft Azure AD Connect Hallo connectiviteit en de huidige status van de SSL-certificaat.

![AD FS-serverinformatie](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

Als het Hallo-lijst bevat een server die niet langer deel uitmaakt van Hallo AD FS-farm, klikt u op **verwijderen** toodelete Hallo-server in de lijst Hallo van servers in uw AD FS-farm.

![Offline-server in de lijst](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> Een server verwijderen uit lijst Hallo van servers voor een AD FS-farm in Azure AD Connect is een lokale bewerking en updates Hallo-informatie voor Hallo AD FS-farm die lokaal wordt onderhouden door Azure AD Connect. Azure AD Connect wijzigen niet Hallo configuratie van AD FS tooreflect Hallo wijziging.    

## <a name="step-2-provide-a-new-ssl-certificate"></a>Stap 2: Geef een nieuw SSL-certificaat

Nadat u hebt bevestigd Hallo informatie over AD FS-farm-servers, wordt u gevraagd Azure AD Connect voor Hallo nieuwe SSL-certificaat. Geef een wachtwoord beveiligde PFX toocontinue Hallo installatie van het certificaat.

![SSL-certificaat](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

Nadat u Hallo certificaat opgeeft, wordt Azure AD Connect gaat door een reeks vereisten. Controleer of Hallo certificaat tooensure dat certificaat Hallo klopt voor Hallo AD FS-farm:

-   Hallo is onderwerp naam/alternatieve onderwerpnaam voor Hallo-certificaat dezelfde als de federatieve-servicenaam Hallo Hallo, of een jokertekencertificaat is.
-   Hallo-certificaat is geldig voor meer dan 30 dagen.
-   vertrouwensketen Hallo-certificaat is geldig.
-   Hallo-certificaat is beveiligd met een wachtwoord.

## <a name="step-3-select-servers-for-hello-update"></a>Stap 3: Servers voor Hallo update selecteren

Selecteer in de volgende stap Hallo Hallo-servers die SSL-certificaat voor toohave Hallo is bijgewerkt moeten. Servers die offline zijn, kunnen niet worden geselecteerd voor Hallo-update.

![Selecteer servers tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

Nadat u Hallo configuratie hebt voltooid, geeft Azure AD Connect Hallo-bericht dat geeft de status Hallo van Hallo update en biedt een optie tooverify Hallo AD FS aanmelden.

![Configuratie voltooien](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>Veelgestelde vragen

* **Wat moet Hallo naam van Hallo-certificaat voor de nieuwe AD FS SSL-certificaat Hallo?**

    Azure AD Connect wordt gecontroleerd of Hallo onderwerp naam/alternatieve naam van certificaat Hallo Hallo federatieve-servicenaam bevat. Bijvoorbeeld, als de naam van uw federation service fs.contoso.com is, moet Hallo onderwerp naam/alternatieve onderwerpnaam fs.contoso.com.  Jokertekens-certificaten worden ook geaccepteerd.

* **Waarom moet ik voor referenties opnieuw op pagina Hallo WAP-server?**

    Als Hallo-referenties die u opgeeft voor het verbinden van tooAD FS-servers niet ook Hallo bevoegdheid toomanage Hallo WAP-servers hebt, klikt u vervolgens Azure AD Connect wordt gevraagd om referenties die u Administrator-bevoegdheden op Hallo WAP-servers hebt.

* **Hallo-server wordt weergegeven als offline. Wat moet ik doen?**

    Azure AD Connect kan een bewerking niet uitvoeren als Hallo server offline is. Als Hallo server deel van Hallo AD FS-farm uitmaakt, moet u Hallo connectiviteit toohello server controleren. Nadat u Hallo probleem hebt opgelost, drukt u op Hallo pictogram tooupdate hello vernieuwingsstatus in Hallo-wizard. Als Hallo server deel uitmaakte van Hallo farm eerder, maar nu niet meer bestaat, klikt u op **verwijderen** toodelete uit Hallo lijst met servers die Azure AD Connect houdt. Verwijderen Hallo-server in de lijst Hallo in Azure AD Connect Hallo AD FS-configuratie zelf wordt niet gewijzigd. Als u gebruikmaakt van AD FS in Windows Server 2016 of hoger, Hallo server blijft in Hallo configuratie-instellingen en worden weergegeven wordt opnieuw hello zodra hello taak uitgevoerd.

* **Kan ik een subset van mijn webfarmservers met Hallo nieuwe SSL-certificaat bijwerken?**

    Ja. U kunt altijd Hallo taak uitvoeren **SSL-certificaat bijwerken** opnieuw tooupdate Hallo resterende servers. Op Hallo **geselecteerde servers voor het SSL-certificaat updates** pagina kunt u Hallo lijst met servers sorteren op **SSL vervaldatum** tooeasily-Hallo servers die nog niet zijn bijgewerkt.

* **Ik Hallo-server in de vorige Hallo uitgevoerd verwijderd, maar deze wordt nog steeds wordt weergegeven als offline en vermelde op Hallo AD FS-Servers pagina. Waarom is Hallo offline server nog steeds er zelfs nadat ik verwijderd?**

    Verwijderen Hallo-server in de lijst Hallo in Azure AD Connect verwijderen niet in Hallo AD FS-configuratie. Azure AD Connect verwijst naar AD FS (WindowsServer 2016 of hoger) voor informatie over het Hallo-farm. Als het Hallo-server nog steeds aanwezig zijn in Hallo AD FS-configuratie, wordt het weergegeven terug in de lijst Hallo.  

## <a name="next-steps"></a>Volgende stappen

- [Azure AD Connect en federatie](active-directory-aadconnectfed-whatis.md)
- [Active Directory Federation Services-beheer en aanpassingen met Azure AD Connect](active-directory-aadconnect-federation-management.md)
