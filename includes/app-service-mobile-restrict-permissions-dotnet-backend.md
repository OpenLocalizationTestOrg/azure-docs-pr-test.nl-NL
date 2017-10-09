
Standaard worden-API's van een back-end van Mobile Apps anoniem aangeroepen. Vervolgens moet u toorestrict toegang tooonly geverifieerde clients.  

* **Node.js back-end (via hello Azure-portal)** :  

    Klik in de instellingen voor mobiele Apps op **gemakkelijk tabellen** en selecteer uw tabel. Klik op **wijzigingsmachtigingen**, selecteer **geverifieerde toegang alleen** voor alle machtigingen en klik vervolgens op **opslaan**.
* **.NET back-end (C#)**:  

    Hallo serverproject, navigeert u in te**domeincontrollers** > **TodoItemController.cs**. Hallo toevoegen `[Authorize]` kenmerk toohello **TodoItemController** klasse als volgt. toorestrict alleen toospecific toegangsmethoden, kunt u ook deze methoden kenmerk NET toothose in plaats van de klasse Hallo toepassen. Hallo serverproject publiceren.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Node.js-back-end (via Node.js-code)** :  

    toorequire verificatie voor toegang tot tabellen, toevoegen Hallo regel toohello Node.js server-script te volgen:

        table.access = 'authenticated';

    Zie voor meer informatie [procedure: verificatie vereisen voor toegang tot tootables](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). hoe toodownload Hallo Quick Start-CodeProject van uw site zien toolearn [hoe: Download Hallo Node.js-back-end Quick Start CodeProject met Git](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
