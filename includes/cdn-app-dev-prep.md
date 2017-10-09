## <a name="prerequisites"></a>Vereisten
Voordat we CDN management code schrijven kunt, moeten we toodo sommige tooenable voorbereiding onze toointeract code Hello Azure Resource Manager.  toodo, moet u:

* Een resource groep toocontain Hallo CDN-profiel we in deze zelfstudie maken maken
* Azure Active Directory tooprovide verificatie voor de toepassing configureren
* Machtigingen toohello resourcegroep zodat alleen gemachtigde gebruikers uit onze Azure AD-tenant met onze CDN-profiel communiceren kan toe te passen

### <a name="creating-hello-resource-group"></a>Hallo resourcegroep maken
1. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com).
2. Klik op Hallo **nieuw** knop in de linkerbovenhoek hello, en vervolgens **Management**, en **resourcegroep**.

    ![Een nieuwe resourcegroep maken](./media/cdn-app-dev-prep/cdn-new-rg-1-include.png)
3. Aanroepen van de resourcegroep *CdnConsoleTutorial*.  Selecteer uw abonnement en kies een locatie in de buurt.  Als u wilt, klikt u op Hallo **pincode toodashboard** selectievakje toopin Hallo resource groep toohello dashboard in Hallo-portal.  Dit maakt het eenvoudiger toofind later.  Nadat u uw selecties hebt gemaakt, klikt u op **maken**.

    ![Naamgeving Hallo resourcegroep](./media/cdn-app-dev-prep/cdn-new-rg-2-include.png)
4. Nadat het Hallo-resourcegroep wordt gemaakt, als u tooyour dashboard niet vastmaken, kunt u deze vinden door te klikken op **Bladeren**, klikt u vervolgens **resourcegroepen**.  Klik op Hallo resource groep tooopen deze.  Maak een notitie van uw **abonnements-ID**.  We hebt deze later nodig.

    ![Naamgeving Hallo resourcegroep](./media/cdn-app-dev-prep/cdn-subscription-id-include.png)

### <a name="creating-hello-azure-ad-application-and-applying-permissions"></a>Hello Azure AD-toepassing maken en toepassen van machtigingen
Er zijn twee benaderingen tooapp verificatie met Azure Active Directory: individuele gebruikers of een service-principal. Een service-principal is vergelijkbaar tooa-serviceaccount in Windows.  In plaats van verleent een bepaalde gebruiker machtigingen toointeract met Hallo CDN-profielen, wordt in plaats daarvan machtigingen Hallo toohello service-principal.  Service-principals worden meestal gebruikt voor geautomatiseerde, niet-interactieve processen.  Hoewel deze zelfstudie een interactieve console-app schrijft is, moet we zich richten op Hallo service principal benadering.

Maken van een service-principal bestaat uit verschillende stappen, zoals het maken van een Azure Active Directory-toepassing.  toodo, gaan we te[Volg deze zelfstudie](../articles/resource-group-create-service-principal-portal.md).

> [!IMPORTANT]
> Ervoor toofollow worden alle Hallo stappen in Hallo [gekoppelde zelfstudie](../articles/resource-group-create-service-principal-portal.md).  Het is *zeer belangrijk* dat u deze hebt voltooid zoals beschreven.  Zorg ervoor dat toonote uw **tenant-ID**, **tenant domeinnaam** (meestal een *. onmicrosoft.com* domein tenzij u een aangepast domein hebt opgegeven), **client-ID** , en **client-verificatiesleutel**, zoals we zullen deze later nodig hebt.  Uiterst voorzichtig tooguard worden uw **client-ID** en **client-verificatiesleutel**, zoals deze referenties kunnen worden gebruikt door iedereen tooexecute bewerkingen als Hallo service-principal.
>
> Als u toohello stap multitenant-toepassing configureren met de naam krijgt, selecteer **Nee**.
>
> Wanneer u stap toohello ophalen [toepassing toorole toewijzen](../articles/azure-resource-manager/resource-group-create-service-principal-portal.md#assign-application-to-role), gebruik Hallo-resourcegroep we eerder hebt gemaakt, *CdnConsoleTutorial*, maar in plaats van Hallo **lezer** rol toewijzen Hallo **CDN-profiel Inzender** rol.  Nadat u hebt toegewezen Hallo toepassing hello **CDN-profiel Inzender** rol in de resourcegroep, return toothis zelfstudie. 
>
>

Als u uw service-principal en toegewezen Hallo hebt gemaakt **CDN-profiel Inzender** rol, Hallo **gebruikers** blade voor de resourcegroep moet vergelijkbaar toothis eruitzien.

![Blade gebruikers](./media/cdn-app-dev-prep/cdn-service-principal-include.png)

### <a name="interactive-user-authentication"></a>Interactieve gebruikersverificatie
Als u in plaats van een service-principal u liever interactieve afzonderlijke gebruikersverificatie, wordt Hallo vergelijkbaar toothat voor een service-principal.  In feite, moet u toofollow Hallo dezelfde procedure, maar een paar kleine wijzigingen aanbrengen.

> [!IMPORTANT]
> Deze stappen alleen volgende als u afzonderlijke gebruikersverificatie toouse in plaats van een service-principal.
>
>

1. Bij het maken van uw toepassing, in plaats van **webtoepassing**, kies **systeemeigen toepassing**.

    ![Systeemeigen toepassing](./media/cdn-app-dev-prep/cdn-native-application-include.png)
2. Op de volgende pagina hello, wordt u gevraagd om een **omleidings-URI**.  Hallo URI won't worden gevalideerd, maar onthouden wat u hebt ingevoerd.  U hebt deze later nodig.
3. Er is geen toocreate moet een **client-verificatiesleutel**.
4. In plaats van het toewijzen van een service-principal toohello **CDN-profiel Inzender** rol, gaan we tooassign individuele gebruikers of groepen.  In dit voorbeeld kunt u zien dat ik hebt toegewezen *CDN Demo gebruiker* toohello **CDN-profiel Inzender** rol.  

    ![Afzonderlijke gebruikerstoegang](./media/cdn-app-dev-prep/cdn-aad-user-include.png)
