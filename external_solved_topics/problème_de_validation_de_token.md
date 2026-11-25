# Problème de validation de TOKEN

**URL:** https://community.simplicite.io/t/13656

## Question
### Request description

Bonjour,

Depuis notre dernière mise à jour qui a embarqué les versions 6.3.17 à 6.3.22 (nous avions un souci technique de récupération d'image qui vient d'être résolu), nous avons un problème de validation de TOKEN par un consommateur de nos API.

Nos API sont accessibles à un groupe habilité sur OKTA.

On dirait que Simplicité ne parvient plus à valider le TOKEN car elle tente de le faire via une URL au lieu de décoder directement, ce qui n'était pas le cas auparavant.
Comme nous n'avons pas défini ```tokeninfo_url```, on dirait que la validation tente une URL par défaut ```[tokeninfo_url](https://okta/oauth2/tokeninfo)```

```text
2026-11-23 09:30:00,808|SIMPLICITE|INFO||http://simplicite-ope-64c54c8f4b-5xtlh:8080||DAUTHCS001|system|com.simplicite.webapp.tools.ServletTool|getAPIGrant||Authentication debug: Token got from the HTTP request = [eyJraWQi(...)ZCPAG66Q]
2026-11-23 09:30:00,809|SIMPLICITE|INFO||http://simplicite-ope-64c54c8f4b-5xtlh:8080||DAUTHCS001|system|com.simplicite.webapp.tools.ServletTool|validateJWTToken||Authentication debug: Token expiration date from the JWT token is [2026-11-23 10:30:00]
2026-11-23 09:30:00,848|SIMPLICITE|ERROR||http://simplicite-ope-64c54c8f4b-5xtlh:8080||ERROR|system|com.simplicite.util.Tool|readUrl||Event: HTTP I/O exception Unable to tunnel through proxy. Proxy returns "HTTP/1.1 503 Service Unavailable": https://okta/oauth2/tokeninfo
2026-11-23 09:30:00,848|SIMPLICITE|WARN||http://simplicite-ope-64c54c8f4b-5xtlh:8080||WAUTHCS001|system|com.simplicite.webapp.tools.ServletTool|createAPIGrantFromToken||Authentication warning: Error calling token info https://okta/oauth2/tokeninfo
```

Nous avons tenté de tester des URL de validation (sans être certains qu'elles soient correctes), mais nous avons ensuite l'erreur suivante. Il semble que Simplicité n'arrive pas à récupérer la date d'expiration.

```
2026-11-23 16:49:48,056|SIMPLICITE|INFO||http://simplicite-ope-64c54c8f4b-5xtlh:8080||DAUTHCS001|system|com.simplicite.webapp.tools.ServletTool|getAPIGrant||Authentication debug: Token got from the HTTP request = [eyJraWQi(...)czsCDOzw]
2026-11-23 16:49:48,057|SIMPLICITE|INFO||http://simplicite-ope-64c54c8f4b-5xtlh:8080||DAUTHCS001|system|com.simplicite.webapp.tools.ServletTool|validateJWTToken||Authentication debug: Token expiration date from the JWT token is [2026-11-23 17:32:54]
2026-11-23 16:49:48,262|SIMPLICITE|WARN||http://simplicite-ope-64c54c8f4b-5xtlh:8080||WAUTHCS001|system|com.simplicite.webapp.tools.ServletTool|createAPIGrantFromToken||Authentication warning: Unable to get the token expiration date from the token info
2026-11-23 16:49:48,263|SIMPLICITE|ERROR||http://simplicite-ope-64c54c8f4b-5xtlh:8080||EAUTHCS001|system|com.simplicite.webapp.tools.ServletTool|createAPIGrantFromToken||Authentication error: Token is expired vs the token expiration date got from the token info 2026-11-23 16:49:48
2026-11-23 16:49:48,263|SIMPLICITE|ERROR||http://simplicite-ope-64c54c8f4b-5xtlh:8080||ERROR|system|com.simplicite.webapp.servlets.api.ExternalObjectServlet|service||Event: Authentication error: Expired token
```

Notre parsauth est le suivant

```json
[
	{ "name": "simplicite", "type": "internal", "visible": true },
	{
        "name": "okta",
        "type": "oauth2",
        "label": "Sign in with MFS credentials",
        "sync": true,
        "visible": true,
        "client_id": "XXXXX",
       "client_secret": "XXXXX",
        "scopes": "openid profile email alliance_profile",
        "authorize_url": "XXXXX/authorize",
        "token_url": "XXXXX/token",
        "logout_url": "XXXXX/logout",
        "post_logout_redirect_uri": "XXXXX/ui",
        "userinfo_url": "hXXXXX/userinfo",
        "userinfo_mappings": {
            "login": "preferred_username",
            "firstname": "given_name",
            "lastname": "family_name",
            "email": "email",
            "phone": "phone",
            "lang": "ignore"
        },
        "jwt_issuer": "XXXXX",
        "tokeninfo_mappings" : {
		"login": "uid" 
	},
        "jwt_claims_mappings": {
            "login": "sub",
            "lang": "ignore"
        }
    },
    { "name": "ldap", "type": "ldap", "visible": false, "sync": false },
{ 
    "visible": false, 
    "name": "standard_external_auth", 
    "label": "Public authentication", 
    "type": "custom" 
}, 
{ 
    "visible": false, 
    "name": "api_external_auth", 
    "label": "API authentication", 
    "type": "custom" 
}
]
```

Auriez-vous des pistes pour nous aider à identifier la source du problème ?
C'est bloquant car l'accès à nos APIs n'est plus possible en production.

Merci d'avance !
Emmanuelle

## Answer
_No answer provided._
