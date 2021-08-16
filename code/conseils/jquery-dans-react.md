React est super cool et très à la mode comparais à Jquery, mais s'il vous arrive de vouloir garder vos vieux codes Jquery et de les faire quoi habitué avec React voici comment je m'y prends.

Retrouvez-le [ici](https://codesandbox.io/s/github/dofbi/jquery-in-react/tree/main/) et les explications ici-bas.

## Étape 1
Charger les librairies

```html
...
<link rel="stylesheet" type="text/css" href="./css/slick.css" />
...
<script src="./js/vendor/jquery-1.12.4.min.js"></script>

<script src="./js/vendor/waypoints.min.js"></script>

<script src="./js/vendor/jquery.counterup.min.js"></script>

<script src="./js/vendor/slick.min.js"></script>
...
```

## Étape 2
Découper votre code jquery en fichier.

public/js/counter.js
```js
$(".counter").counterUp({

  delay: 10,

  time: 3000

});

```

public/js/slick.js
```js
$(".slick-track").slick({

  infinite: true,

  slidesToShow: 3,

  slidesToScroll: 3

});
```



## Étape 3
Charger vos fichiers dans le composant qui les utilise.

services.js
```js
import { useEffect } from 'react'

export const ImportScript = resourceUrl => {

  useEffect(() => {
    const script = document.createElement('script');
    script.src = resourceUrl;
    script.async = true;

    if (window.jQuery) {
      document.body.appendChild(script);
      return () => {
        document.body.removeChild(script);
      }
    }
  }, [resourceUrl]);
}
```


components/counter.js
```js
...
import { ImportScript } from "../services";

const Counter = () => {
  ImportScript("./js/load/counter.js");

  return (...);
};
...
```

components/slick.js
```js
...
import { ImportScript } from "../services";

const Slick = () => {
  ImportScript("./js/load/slick.js");

  return (...);
};
...
```

Voilà, c'est fini, pour le moment.