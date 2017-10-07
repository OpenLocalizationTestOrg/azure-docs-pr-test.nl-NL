---
title: aaaMFA software development kit voor aangepaste apps | Microsoft Docs
description: Dit artikel laat zien hoe Hallo verificatie van Azure MFA-SDK tooenable in twee stappen voor uw aangepaste apps toodownload en het gebruik.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a>Gebouw multi-factor Authentication in aangepaste Apps (SDK)

Hello Azure multi-factor Authentication Software Development Kit (SDK) kunt die u de verificatie in twee stappen rechtstreeks in bouwen Hallo aanmelden of transactie verwerkt van toepassingen in uw Azure AD-tenant.

Hallo multi-factor Authentication SDK is beschikbaar voor C#, Visual Basic (.NET), Java, Perl, PHP en Ruby. Hallo SDK biedt een thin wrapper rond verificatie in twee stappen. Het bevat alles wat dat u moet toowrite uw code, inclusief opmerkingen broncodebestanden, bijvoorbeeld bestanden en een gedetailleerde Leesmij-bestand. Elke SDK bevat ook een certificaat en de persoonlijke sleutel voor het versleutelen van transacties die unieke tooyour multi-factor Authentication-Provider zijn. Als u een provider hebt, kunt u Hallo SDK in zoveel talen en indelingen downloaden als u nodig hebt.

Hallo-structuur van Hallo API's in Hallo multi-factor Authentication SDK is eenvoudig. Controleer één functie tooan API met Hallo meerledige optie parameters (zoals de verificatie-modus) en gegevens van de gebruiker (zoals Hallo telefoon nummer toocall of Hallo PINCODE nummer toovalidate) aanroepen. Hallo API's vertalen Hallo functieaanroep in web services aanvragen toohello cloud-gebaseerde Azure multi-factor Authentication Service. Alle aanroepen moeten een verwijzing toohello persoonlijk certificaat dat is opgenomen in elke SDK bevatten.

Omdat Hallo API's toegang toousers geregistreerd in Azure Active Directory niet hebt, moet u gebruikersgegevens in een bestand of de database opgeven. Ook Hallo API's bieden geen informatie over de beheerfuncties van inschrijving of gebruiker, dus moet u toobuild deze processen in uw toepassing.

> [!IMPORTANT]
> toodownload Hallo SDK, moet u een Azure multi-factor Authentication-Provider toocreate zelfs als u Azure MFA, AAD Premium of EMS-licenties hebt. Als u een Azure multi-factor Authentication-Provider voor dit doel maken en hebt al licenties, zorg ervoor dat toocreate Hallo Provider Hello **Per ingeschakelde gebruiker** model. Koppel vervolgens Hallo Provider toohello map waarin hello Azure MFA, Azure AD Premium of EMS-licenties. Deze configuratie zorgt ervoor dat u wordt alleen gefactureerd als u meer unieke gebruikers met behulp van Hallo SDK dan het aantal licenties dat u bezit Hallo hebt.


## <a name="download-hello-sdk"></a>Hallo SDK downloaden
Hello Azure multi-factor Authentication SDK downloaden vereist een [Azure multi-factor Authentication-Provider](multi-factor-authentication-get-started-auth-provider.md).  Hiervoor moet een volledige Azure-abonnement, zelfs als het eigendom van Azure MFA, Azure AD Premium of Enterprise Mobility Suite licenties zijn.  toodownload hello SDK, navigeer toohello multi-factor-beheerportal. U kunt Hallo portal door het beheer van Hallo multi-factor Auth Provider rechtstreeks of door te klikken op Hallo bereiken **"Ga toohello portal"** koppeling op de pagina instellingen Hallo MFA-service.

### <a name="download-from-hello-azure-classic-portal"></a>Downloaden van Hallo klassieke Azure-portal
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als beheerder.
2. Selecteer aan de linkerkant Hallo **Active Directory**.
3. Op de pagina van het Hallo Active Directory, op de bovenste Selecteer Hallo **multi-factor Auth-Providers**
4. Selecteer onderaan Hallo **beheren**. Er wordt een nieuwe pagina geopend.
5. Klik op Hallo links onderin Hallo **SDK**.
   <center>![Downloaden](./media/multi-factor-authentication-sdk/download.png)</center>
6. Selecteer Hallo gewenste taal en klikt u op één Hallo gekoppeld downloadkoppelingen.
7. Sla Hallo downloaden.

### <a name="download-from-hello-service-settings"></a>Downloaden van Hallo service-instellingen
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als beheerder.
2. Selecteer aan de linkerkant Hallo **Active Directory**.
3. Dubbelklik op uw exemplaar van Azure AD.
4. Op Hallo bovenaan op **configureren**
5. Selecteer onder multi-factor authentication **service-instellingen beheren**
   ![downloaden](./media/multi-factor-authentication-sdk/download2.png)
6. Klik op Hallo services instellingenpagina onderaan Hallo welkomstscherm op **Ga toohello portal**. Er wordt een nieuwe pagina geopend.
   ![Downloaden](./media/multi-factor-authentication-sdk/download3a.png)
7. Klik op Hallo links onderin Hallo **SDK**.
8. Selecteer Hallo gewenste taal en klikt u op één Hallo gekoppeld downloadkoppelingen.
9. Sla Hallo downloaden.

## <a name="whats-in-hello-sdk"></a>Wat is er in Hallo SDK
Hallo SDK omvat Hallo volgende items:

* **LEESMIJ**. Legt uit hoe toouse multi-factor Authentication-API's in een nieuwe of bestaande toepassing hello.
* **Bronbestanden** voor multi-factor Authentication
* **Clientcertificaat** dat u toocommunicate Hello multi-factor Authentication-service
* **Persoonlijke sleutel** voor Hallo certificaat
* **Aanroepen van resultaten.** Een lijst met oproepresultaatcodes. tooopen dit bestand, gebruikt u een toepassing met de tekst, zoals WordPad. Gebruik Hallo resultaat codes tootest aanroepen en problemen oplossen Hallo-implementatie van multi-factor Authentication in uw toepassing. Ze zijn geen statuscodes voor verificatie.
* **Voorbeelden.** Voorbeeldcode voor een eenvoudige werkende implementatie van multi-factor Authentication.

> [!WARNING]
> Hallo-clientcertificaat is een unieke persoonlijk certificaat die speciaal voor u is gegenereerd. Geen delen of dit bestand verloren. Het is de beveiliging van uw belangrijkste tooensuring Hallo van uw communicatie met Hallo multi-factor Authentication-service.

## <a name="code-sample"></a>Codevoorbeeld
Dit voorbeeld laat zien u hoe toouse Hallo API's in de SDK van Azure multi-factor Authentication tooadd standaardmodus stem Hallo verificatie tooyour toepassing aanroepen. Standaardmodus is een telefoongesprek die Hallo gebruiker reageert tooby Hallo # te drukken.

In dit voorbeeld Hallo C# .NET 2.0 SDK multi-factor Authentication in een eenvoudige ASP.NET-toepassing met C#-serverzijde logica gebruikt, maar gaat Hallo op dezelfde manier in andere talen. Omdat Hallo SDK bronbestanden, niet-uitvoerbare bestanden bevat, kunt u Hallo-bestanden maken en ernaar te verwijzen of opnemen rechtstreeks in uw toepassing.

> [!NOTE]
> Bij het implementeren van multi-factor Authentication gebruiken Hallo aanvullende methoden (telefoongesprek of tekstbericht) als secundair of tertiair verificatie toosupplement primaire authenticatiemethode (gebruikersnaam en wachtwoord). Deze methoden zijn niet bedoeld als primaire verificatiemethoden.

### <a name="code-sample-overview"></a>Overzicht van de code-voorbeeld
Deze voorbeeldcode voor een eenvoudige demo webtoepassing maakt gebruik van een telefoongesprek met een # reactie tooverify Hallo gebruikersverificatie. Deze factoren telefoongesprek wordt genoemd in de multi-factor Authentication standaardmodus.

Hallo clientcode omvat niet alle multi-factor Authentication-specifieke elementen bevat. Omdat de aanvullende verificatiefactoren Hallo onafhankelijk van de primaire verificatie hello, kunt u ze kunt toevoegen zonder bestaande Hallo aanmelding interface. Hallo API's in Hallo multi-factor-SDK kunt u Hallo gebruikerservaring aanpassen, maar hoeft u mogelijk niet toochange iets helemaal.

Hallo servercode wordt standaard verificatiemodus toegevoegd in stap 2. Er wordt een PfAuthParams-object gemaakt met Hallo-parameters die vereist voor de verificatie standaardmodus zijn: gebruikersnaam, telefoon aantal en de modus en Hallo pad toohello clientcertificaat (CertFilePath), die is in elke aanroep vereist. Zie voor een demonstratie van alle parameters in PfAuthParams Hallo voorbeeld van een bestand in Hallo SDK.

Hallo-code wordt vervolgens Hallo PfAuthParams object toohello pf_authenticate() functie doorgegeven. Hallo-retourwaarde geeft Hallo slagen of mislukken van Hallo-verificatie. Hallo-parameters, callStatus en Aanroepstatus, extra aanroep resultaat informatie bevatten. oproepresultaatcodes Hello zijn gedocumenteerd in Hallo aanroep resultatenbestand in Hallo SDK.

Deze minimale implementatie kan worden geschreven in een paar regels. In productiecode moet zou u bevatten echter meer geavanceerde foutafhandeling, extra databasecode en een betere gebruikerservaring.

### <a name="web-client-code"></a>Web-Client-Code
Hallo volgt web clientcode voor een demo-pagina.

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a>Code op de server
Multi-factor Authentication is geconfigureerd en worden uitgevoerd in stap 2 in Hallo servercode te volgen. Standaard-modus (MODE_STANDARD) is dat een telefoongesprek toowhich Hallo gebruiker reageert door Hallo #-toets te drukken.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
