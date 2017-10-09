---
title: aaaAzure AD v2 Android aan de slag - gebruik | Microsoft Docs
description: Hoe een Android-app kunt ophalen van een toegangstoken en Microsoft Graph API of API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 4480d89eb7638fe7d588c8cebd2b1e3c9d4c6e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="use-hello-microsoft-authentication-library-msal-tooget-a-token-for-hello-microsoft-graph-api"></a>Hallo Microsoft Authentication Library (MSAL) tooget een token voor Hallo Microsoft Graph API gebruiken

1.  Open: `MainActivity` (onder `app`  >  `java`  >  `{domain}.{appname}`)
2.  Hallo na invoer toevoegen:

```java
import android.app.Activity;
import android.content.Intent;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import com.android.volley.*;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.Volley;
import org.json.JSONObject;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import com.microsoft.identity.client.*;
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Vervang Hallo `MainActivity` klasse met hieronder:
</li>
</ol>

```java
public class MainActivity extends AppCompatActivity {

    final static String CLIENT_ID = "[Enter hello application Id here]";
    final static String SCOPES [] = {"https://graph.microsoft.com/User.Read"};
    final static String MSGRAPH_URL = "https://graph.microsoft.com/v1.0/me";

    /* UI & Debugging Variables */
    private static final String TAG = MainActivity.class.getSimpleName();
    Button callGraphButton;
    Button signOutButton;

    /* Azure AD Variables */
    private PublicClientApplication sampleApp;
    private AuthenticationResult authResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        callGraphButton = (Button) findViewById(R.id.callGraph);
        signOutButton = (Button) findViewById(R.id.clearCache);

        callGraphButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onCallGraphClicked();
            }
        });

        signOutButton.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                onSignOutClicked();
            }
        });

  /* Configure your sample app and save state for this activity */
        sampleApp = null;
        if (sampleApp == null) {
            sampleApp = new PublicClientApplication(
                    this.getApplicationContext(),
                    CLIENT_ID);
        }

  /* Attempt tooget a user and acquireTokenSilent
   * If this fails we do an interactive request
   */
        List<User> users = null;

        try {
            users = sampleApp.getUsers();

            if (users != null && users.size() == 1) {
          /* We have 1 user */

                sampleApp.acquireTokenSilentAsync(SCOPES, users.get(0), getAuthSilentCallback());
            } else {
          /* We have no user */

          /* Let's do an interactive request */
                sampleApp.acquireToken(this, SCOPES, getAuthInteractiveCallback());
            }
        } catch (MsalClientException e) {
            Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

        } catch (IndexOutOfBoundsException e) {
            Log.d(TAG, "User at this position does not exist: " + e.toString());
        }

    }

//
// App callbacks for MSAL
// ======================
// getActivity() - returns activity so we can acquireToken within a callback
// getAuthSilentCallback() - callback defined toohandle acquireTokenSilent() case
// getAuthInteractiveCallback() - callback defined toohandle acquireToken() case
//

    public Activity getActivity() {
        return this;
    }

    /* Callback method for acquireTokenSilent calls 
     * Looks if tokens are in hello cache (refreshes if necessary and if we don't forceRefresh)
     * else errors that we need toodo an interactive request.
     */
    private AuthenticationCallback getAuthSilentCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call Graph now */
                Log.d(TAG, "Successfully authenticated");

            /* Store hello authResult */
                authResult = authenticationResult;

            /* call graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                } else if (exception instanceof MsalUiRequiredException) {
                /* Tokens expired or no session, retry with interactive */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }


    /* Callback used for interactive request.  If succeeds we use hello access
         * token toocall hello Microsoft Graph. Does not check cache
         */
    private AuthenticationCallback getAuthInteractiveCallback() {
        return new AuthenticationCallback() {
            @Override
            public void onSuccess(AuthenticationResult authenticationResult) {
            /* Successfully got a token, call graph now */
                Log.d(TAG, "Successfully authenticated");
                Log.d(TAG, "ID Token: " + authenticationResult.getIdToken());

            /* Store hello auth result */
                authResult = authenticationResult;

            /* call Graph */
                callGraphAPI();

            /* update hello UI toopost call Graph state */
                updateSuccessUI();
            }

            @Override
            public void onError(MsalException exception) {
            /* Failed tooacquireToken */
                Log.d(TAG, "Authentication failed: " + exception.toString());

                if (exception instanceof MsalClientException) {
                /* Exception inside MSAL, more info inside MsalError.java */
                } else if (exception instanceof MsalServiceException) {
                /* Exception when communicating with hello STS, likely config issue */
                }
            }

            @Override
            public void onCancel() {
            /* User canceled hello authentication */
                Log.d(TAG, "User cancelled login.");
            }
        };
    }

    /* Set hello UI for successful token acquisition data */
    private void updateSuccessUI() {
        callGraphButton.setVisibility(View.INVISIBLE);
        signOutButton.setVisibility(View.VISIBLE);
        findViewById(R.id.welcome).setVisibility(View.VISIBLE);
        ((TextView) findViewById(R.id.welcome)).setText("Welcome, " +
                authResult.getUser().getName());
        findViewById(R.id.graphData).setVisibility(View.VISIBLE);
    }

    /* Use MSAL tooacquireToken for hello end-user
     * Callback will call Graph api w/ access token & update UI
     */
    private void onCallGraphClicked() {
        sampleApp.acquireToken(getActivity(), SCOPES, getAuthInteractiveCallback());
    }

    /* Handles hello redirect from hello System Browser */
    @Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        sampleApp.handleInteractiveRequestRedirect(requestCode, resultCode, data);
    }

}
```
<!--start-collapse-->
### <a name="more-information"></a>Meer informatie
#### <a name="getting-a-user-token-interactive"></a>Een token ophalen interactieve
Aanroepen Hallo `AcquireTokenAsync` methode resulteert in een venster waarin wordt gevraagd Hallo toosign van de gebruiker in. Toepassingen zijn doorgaans vereist een gebruiker toosign in interactief Hallo eerste keer dat ze tooaccess moeten een beveiligde bron of wanneer een stille bewerking tooacquire een token mislukt (bijvoorbeeld Hallo gebruikerswachtwoord verlopen).

#### <a name="getting-a-user-token-silently"></a>Een gebruiker ophalen achtergrond token
`AcquireTokenSilentAsync`token acquisities van organisaties en verlenging zonder tussenkomst van de gebruiker worden verwerkt. Na `AcquireTokenAsync` wordt uitgevoerd voor Hallo eerst `AcquireTokenSilentAsync` Hallo methode gebruikte tooobtain tokens tooaccess resources voor volgende aanroepen - beveiligd als aanroepen toorequest of vernieuwen van tokens achtergrond worden aangebracht.
Uiteindelijk `AcquireTokenSilentAsync` mislukt: bijvoorbeeld Hallo gebruiker heeft zich afgemeld of het wachtwoord op een ander apparaat is gewijzigd. Wanneer MSAL detecteert dat Hallo probleem doordat een interactieve actie kan worden omgezet, wordt deze gebeurtenis wordt gestart een `MsalUiRequiredException`. Uw toepassing kan verwerken van deze uitzondering op twee manieren:

1.  Een aanroep tegen `AcquireTokenAsync` onmiddellijk, wat ertoe leidt Hallo gebruiker toosign in. Dit patroon wordt meestal gebruikt in de on line toepassingen wanneer er geen offline inhoud in de toepassing hello beschikbaar voor Hallo-gebruiker is. Hallo voorbeeld gegenereerd met deze Begeleide installatie maakt gebruik van dit patroon: u kunt deze bekijken in actie Hallo eerste keer dat u Hallo voorbeeld uitvoert: omdat er geen gebruiker ooit toepassing hello gebruikt, `PublicClientApp.Users.FirstOrDefault` bevat een null-waarde en een `MsalUiRequiredException` uitzondering gegenereerd. code in de steekproef Hallo Hallo vervolgens ingangen Hallo uitzondering door aan te roepen `AcquireTokenAsync` waardoor Hallo gebruiker toosign in.
2.  Toepassingen kunnen ook een visuele indicatie toohello-gebruiker die een interactief aanmelden is vereist, zodat Hallo-gebruiker kunt selecteren Hallo juiste moment toosign in of toepassing hello opnieuw kunt maken `AcquireTokenSilentAsync` op een later tijdstip. Dit wordt meestal gebruikt wanneer het Hallo-gebruiker is kunnen tooaccess functionaliteit van de toepassing hello zonder wordt onderbroken - bijvoorbeeld is offline-inhoud in de toepassing hello beschikbaar. In dit geval Hallo-gebruiker kunt bepalen wanneer hij of zij wil toosign in tooaccess Hallo beveiligde resource, toorefresh Hallo verouderde informatie of uw toepassing kunt bepalen tooretry `AcquireTokenSilentAsync` wanneer netwerk is hersteld na een tijdelijk niet beschikbaar.
<!--end-collapse-->

## <a name="call-hello-microsoft-graph-api-using-hello-token-you-just-obtained"></a>Hallo Hallo-token die u zojuist hebt verkregen met Microsoft Graph-API niet aanroepen
1.  Toevoegen van de volgende methoden in Hallo Hallo `MainActivity` klasse:

```java
/* Use Volley toomake an HTTP request toohello /me endpoint from MS Graph using an access token */
private void callGraphAPI() {
    Log.d(TAG, "Starting volley request toograph");

    /* Make sure we have a token toosend toograph */
    if (authResult.getAccessToken() == null) {return;}

    RequestQueue queue = Volley.newRequestQueue(this);
    JSONObject parameters = new JSONObject();

    try {
        parameters.put("key", "value");
    } catch (Exception e) {
        Log.d(TAG, "Failed tooput parameters: " + e.toString());
    }
    JsonObjectRequest request = new JsonObjectRequest(Request.Method.GET, MSGRAPH_URL,
            parameters,new Response.Listener<JSONObject>() {
        @Override
        public void onResponse(JSONObject response) {
            /* Successfully called graph, process data and send tooUI */
            Log.d(TAG, "Response: " + response.toString());

            updateGraphUI(response);
        }
    }, new Response.ErrorListener() {
        @Override
        public void onErrorResponse(VolleyError error) {
            Log.d(TAG, "Error: " + error.toString());
        }
    }) {
        @Override
        public Map<String, String> getHeaders() throws AuthFailureError {
            Map<String, String> headers = new HashMap<>();
            headers.put("Authorization", "Bearer " + authResult.getAccessToken());
            return headers;
        }
    };

    Log.d(TAG, "Adding HTTP GET tooQueue, Request: " + request.toString());

    request.setRetryPolicy(new DefaultRetryPolicy(
            3000,
            DefaultRetryPolicy.DEFAULT_MAX_RETRIES,
            DefaultRetryPolicy.DEFAULT_BACKOFF_MULT));
    queue.add(request);
}

/* Sets hello Graph response */
private void updateGraphUI(JSONObject graphResponse) {
    TextView graphText = (TextView) findViewById(R.id.graphData);
    graphText.setText(graphResponse.toString());
}
```
<!--start-collapse-->
### <a name="more-information-about-making-a-rest-call-against-a-protected-api"></a>Meer informatie over het maken van een REST-aanroep op basis van een beveiligde API

In deze voorbeeldtoepassing `callGraphAPI` aanroepen `getAccessToken` en maakt vervolgens een HTTP `GET` -aanvraag in voor een resource die is een token vereist en retourneert Hallo inhoud. Met deze methode wordt Hallo verkregen token in Hallo *HTTP-autorisatie-header*. Voor dit voorbeeld is Hallo resource Hallo Microsoft Graph API *mij* eindpunt – Hallo van gebruikersprofielgegevens worden weergegeven.
<!--end-collapse-->

## <a name="setup-sign-out"></a>Setup afmelden

1.  Toevoegen van de volgende methoden in Hallo Hallo `MainActivity` klasse:

```java
/* Clears a user's tokens from hello cache.
 * Logically similar too"sign out" but only signs out of this app.
 */
private void onSignOutClicked() {

    /* Attempt tooget a user and remove their cookies from cache */
    List<User> users = null;

    try {
        users = sampleApp.getUsers();

        if (users == null) {
            /* We have no users */

        } else if (users.size() == 1) {
            /* We have 1 user */
            /* Remove from token cache */
            sampleApp.remove(users.get(0));
            updateSignedOutUI();

        }
        else {
            /* We have multiple users */
            for (int i = 0; i < users.size(); i++) {
                sampleApp.remove(users.get(i));
            }
        }

        Toast.makeText(getBaseContext(), "Signed Out!", Toast.LENGTH_SHORT)
                .show();

    } catch (MsalClientException e) {
        Log.d(TAG, "MSAL Exception Generated while getting users: " + e.toString());

    } catch (IndexOutOfBoundsException e) {
        Log.d(TAG, "User at this position does not exist: " + e.toString());
    }
}

/* Set hello UI for signed-out user */
private void updateSignedOutUI() {
    callGraphButton.setVisibility(View.VISIBLE);
    signOutButton.setVisibility(View.INVISIBLE);
    findViewById(R.id.welcome).setVisibility(View.INVISIBLE);
    findViewById(R.id.graphData).setVisibility(View.INVISIBLE);
    ((TextView) findViewById(R.id.graphData)).setText("No Data");
}
```
<!--start-collapse-->
### <a name="more-information"></a>Meer informatie

`onSignOutClicked`hierboven verwijdert hello gebruiker uit de cache van de gebruiker MSAL – effectief ziet MSAL tooforget Hallo huidige gebruiker zodat een tooacquire toekomstige aanvraag een token alleen slaagt als het gaat toobe interactieve.
Hoewel het Hallo-toepassing in dit voorbeeld ondersteunt een enkele gebruiker, MSAL scenario's waar meerdere accounts aangemeld op Hallo worden kunnen ondersteunt dezelfde tijd: een voorbeeld hiervan is een e-mailtoepassing waar een gebruiker heeft meerdere accounts.
<!--end-collapse-->
