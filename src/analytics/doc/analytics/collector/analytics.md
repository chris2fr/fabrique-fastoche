## class Analytics

L’instance d’Analytics est accessible depuis `window.village.analytics`

### PROPRIÉTÉS

##### page

_Page_

`window.village.analytics.page`

Getter qui retourne l’instance de [Page](page.md)

* * *

##### site

_Site_

`window.village.analytics.site`

Getter qui retourne l’instance de [Site](site.md)

* * *

##### user

_User_

`window.village.analytics.user`

Getter qui retourne l’instance de [User](user.md)

* * *


##### search

_Search_

`window.village.analytics.search`

Getter qui retourne l’instance de [Search](search.md)

* * *

##### funnel :

_Funnel_

`window.village.analytics.funnel`

Getter qui retourne l’instance de [Funnel](funnel.md)

* * *

##### cmp

_ConsentManagerPlatform_

`window.village.analytics.cmp`

Getter qui retourne l’instance de [ConsentManagerPlatform](cmp.md)

* * *

##### opt

_Opt_

`window.village.analytics.opt`

Getter qui retourne l’instance de [Opt](opt.md)

##### isReady

_Boolean_

`window.village.analytics.isReady`

Getter qui retourne l'état de l'API, à savoir `true` quand elle est prête à être utilisée.

* * *

##### readiness

_Promise_

`window.village.analytics.readiness`

Getter qui retourne une Promise permettant de se synchroniser sur l'API, lorsque celle-ci est prête à être utilisée.

    window.village.analytics.readiness.then(() => { // start }, () => { // error } );

* * *

##### collection

_String_

`window.village.analytics.collection`

Getter qui retourne le mode de récolte des données de la page. Défini dans la configuration (voir propriété `collection` de la [configuration](../installation/configuration.md#collection))

* `manual` : Les données de pages ne sont pas envoyées. Attend l’execution de la fonction `collect()`.

* `load` : Les données de page sont envoyées automatiquement au chargement de la page. (par défaut)

* `full` : Les données sont envoyées à chaque changement de path dans l’URL, permettant le support des “Single-page
  application” (par défaut si village en mode ‘vue’, ‘react’ ou ‘angular’)
  
* `hash` : Les données sont envoyées à chaque changement de hash dans l'URL

* * *

##### isActionEnabled

_Boolean_

`window.village.analytics.isActionEnabled`

Permet d’activer / désactiver la mesure d'audience des actions.

* Par défaut, la mesure d'audience des actions est désactivée.

Défini dans la configuration (voir propriété `isActionEnabled` de la [configuration](../installation/configuration.md))

* * *

##### isDebugging

_Boolean_

`window.village.analytics.isDebugging`

Permet d’activer / désactiver le debug Eulerian.

⚠️ le debug Eulerian reste persistant sur la page par le biais du LocalStorage jusqu'à désactivation.

* * *

### MÉTHODES

##### push (type, layer)

`window.village.analytics.push(type, layer)`

Alias de la fonction EA\_push d’Eulerian via le package. (voir doc Eulerian [https://eulerian.wiki/doku.php?id=fr:quickonboarding:installation:tag\_installation\_guide#types\_d\_appels](https://eulerian.wiki/doku.php?id=fr:quickonboarding:installation:tag_installation_guide#types_d_appels))

* * *

##### reset (clear = false)

`window.village.analytics.reset(clear)`

Permet de remettre les données dans l'état d’origine de la configuration.

Si le paramètre `clear = true` => toutes les données sont remises en état indéfini.

* * *

###### collect {#collect}

`window.village.analytics.collect()`

Envoie au collector le datalayer constitué par l’ensemble des données consolidées depuis :

* Page

* Site

* User

* Search

* Funnel

* * *

### USAGE

> **Note**
> Le package Analytics repose sur 2 principes de fonctionnement pour traquer les pages :
> * Par le biais de la configuration, il est possible de définir toutes les données qui seront envoyées au chargement de la page (via le mode automatique)
> * Par le biais de l’API, on peut définir toutes les données propriété par propriété pour ensuite envoyer l’ensemble grâce à la méthode **collect**


```javascript
village.analytics.readiness.then(() => { // l'API analytics est prête à l'utilisation
    village.analytics.isDebugging = true; // active le debugging eulerian
    village.analytics.reset(); // remet les données à l'état de configuration
    village.analytics.user.connect('USER\_ID', 'ENCRYPTED\_EMAIL', true);
    village.analytics.page.path = 'my/virtual/page';
    village.analytics.page.isError = true;
    village.analytics.page.template = 'page404';
    village.analytics.collect(); // envoie les données
});
```
