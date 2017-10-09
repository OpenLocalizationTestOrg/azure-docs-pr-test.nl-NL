Met behulp van organisaties zijn meer [Software als een Service (SaaS)](https://azure.microsoft.com/overview/what-is-saas/) toepassingen voor productiviteit omdat cloud-technologie en hulpprogramma's worden steeds vaker beschikbaar. Wanneer het aantal SaaS-apps Hallo groeit, wordt het lastig voor Hallo beheerders toomanage accounts en de toegangsrechten en Hallo voor gebruikers tooremember hun verschillende wachtwoorden. Beheer van deze toepassingen afzonderlijk maakt extra werk en is minder veilig is.

* Werknemers met bijhouden van de tookeep van veel wachtwoorden toouse meestal veilige minder methoden tooremember ze schrijven wachtwoorden of met behulp van Hallo dezelfde wachtwoorden veel accounts.
* Wanneer een nieuwe werknemer binnenkomt of een verlaat, moeten alle hun accounts worden afzonderlijk ingericht of buiten gebruik gesteld.
* Bovendien werknemers kunnen aan de slag met SaaS-apps voor hun werk zonder tussenkomst van IT, wat betekent dat ze maken hun eigen accounts op systemen met Hallo IT-beheerders die nog niet goedgekeurd en worden niet controleren.  

Er is een oplossing voor al deze uitdagingen voor eenmalige aanmelding (SSO). Het eenvoudigste manier toomanage meerdere apps heeft Hallo en gebruikers voorzien van een consistente ervaring voor eenmalige aanmelding. Azure Active Directory (Azure AD) biedt een robuuste oplossing voor eenmalige aanmelding en heeft veel beschikbare vooraf geïntegreerde toepassingen, met zelfstudies voor beheerders tooquickly instellen van een nieuwe app en inrichting gebruikers starten.

## <a name="how-does-azure-active-directory-integrate-apps"></a>Hoe Azure Active Directory integreren van apps?
Azure AD kunt u toointegrate uw apps en de ingerichte accounts. Dit kan worden gedaan via een van twee methoden.

* Als het Hallo-app is vooraf geïntegreerd in Hallo app-galerie, kunt u via deze portal tooset van apps en Hallo instellingen tooallow SSO configureren. Voor elke app galerie, u kunt aan de slag door Hallo eenvoudige stapsgewijze instructies die zijn gepresenteerd in app-galerie hello en in hello Azure portal tooenable eenmalige aanmelding.
* Als Hallo app zich niet in de galerie hello, kunt u de meeste apps nog steeds instellen in Azure AD als een aangepaste app. Hiervoor moet iets meer technische kennis tooconfigure. U kunt elke toepassing die SAML 2.0 als federatieve app ondersteunt of elke toepassing die is een op basis van een HTML-aanmeldingspagina als wachtwoord SSO app toevoegen.

In het Hallo-geval waar gebruikers hebben gemaakt hun eigen accounts voor SaaS-apps die niet worden beheerd door IT, Hallo [Cloud App Discovery](../articles/active-directory/active-directory-cloudappdiscovery-whatis.md) hulpprogramma biedt een oplossing. Dit hulpprogramma controleert Hallo web verkeer tooidentify welke apps worden gebruikt in de gehele organisatie Hallo en het aantal gebruikers van elk van deze Hallo. IT de toolearn van deze informatie welke apps Hallo gebruikers liever en welke toointegrate beslist met Azure AD voor eenmalige aanmelding kunt gebruiken.  

Wanneer u een app in Azure AD integreren, kunt u de identiteit van Hallo gebruikers tot stand gebrachte toepassing identiteiten tootheir respectieve Azure AD kunt toewijzen.  

