
1. Hallo-project in Android Studio openen.

2. In **Projectverkenner** open Hallo ToDoActivity.java bestand in Android Studio en volgende importinstructies Hallo toevoegen:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Hallo na methode toohello toevoegen **ToDoActivity** klasse:

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    Deze code maakt een methode toohandle Hallo Google-verificatieproces. Een dialoogvenster weergegeven Hallo-ID van Hallo geverifieerde gebruiker. U kunt alleen doorgaan op een geslaagde verificatie.

    > [!NOTE]
    > Als u van een id-provider dan Google gebruikmaakt, wijzigt u Hallo-waarde doorgegeven toohello **aanmelding** methode tooone Hallo volgende waarden: _MicrosoftAccount_, _Facebook_, _Twitter_, of _windowsazureactivedirectory_.

4. In Hallo **onCreate** methode toevoegen van de volgende coderegel na het Hallo-code die Hallo instantieert Hallo `MobileServiceClient` object.

        authenticate();

    Deze aanroep start Hallo-verificatie.

5. Hallo resterende code na verplaatsen `authenticate();` in Hallo **onCreate** methode tooa nieuwe **createTable** methode:

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. tooensure omleiding werkt zoals verwacht, toevoegen Hallo volgende tekstfragment _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. RedirectUriScheme too_build.gradle_ van uw Android-toepassing toevoegen.

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. Com.android.support:customtabs:23.0.1 toohello afhankelijkheden in uw build.gradle toevoegen:

      afhankelijkheden {/ /... 'com.android.support:customtabs:23.0.1' compileren}

9. Van Hallo **uitvoeren** menu, klikt u op **app uitvoeren** toostart Hallo-app en meld u aan met uw gekozen id-provider.

> [!WARNING]
> Hallo vermeld URL-schema is hoofdlettergevoelig.  Zorg ervoor dat alle instanties van `{url_scheme_of_you_app}` gebruik Hallo dezelfde aanvraag.

Wanneer u bent aangemeld, moet Hallo app moet worden uitgevoerd zonder fouten, en u kunnen tooquery Hallo back-end-service worden updates toodata maken.
