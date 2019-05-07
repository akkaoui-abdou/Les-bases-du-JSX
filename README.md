Simple Exemples in react explain how to use the component in JSX
===



Introduction
---
Voici un composant React ultra basique:
```javascript

var HelloWorld = () => {
  return <div>Hello World</div>;
};

```


Cette fonction ne prenant pas d’argument retourne donc du … HTML ? XML ? What the f… ?!
On se calme, on appelle ça du JSX et on va découvrir à quel point c’est pratique.


Introduction au JSX
---

Le JSX est du sucre syntaxique uniquement là pour faciliter l’expérience de développement (nous verrons plus tard pourquoi).

Pas à pas, nous allons découvrir sa syntaxe.


Le basique
---

On l’a déjà vu mais on le rappelle :

```javascript

var HelloWorld = () => {
  return <div>Hello World</div>;
};

```

Ici, le JSX retourne un texte contenu dans une balise div.



Le composant avec une variable
---

On l’a déjà vu mais on le rappelle :

```javascript

var HelloUser = () => {
  var user = 'Gaël';
  return <div>Hello {user}!</div>;
};

```

Pour utiliser du JavaScript dans du JSX, il faut l’inclure entre { }.



Le commentaire
---

Tout simplement du commentaire JavaScript mais entre {}

```javascript

var HelloWorld = () => {
  {/* Je suis un commentaire JSX */}
  return <div>Hello World</div>;
};

```

Ici, le JSX retourne un texte contenu dans une balise div.




Avec un tableau
---

Ici on map sur un tableau par exemple :

```javascript

var AfficheUsers = () => {
  var users = ['Johnny','Billy','Alfred'];
  return (
    <div>
      { users.map(user => <p>{user}<p> }
    </div>
  );
};

```

ce qui donnera dans notre navigateur:

```html
<div>
  <p>Johnny</p>
  <p>Billy</p>
  <p>Alfred</p>
</div>
```



Insérer un composant React dans du JSX
---

Si manipuler des éléments HTML classiques ne bousculent pas trop l’esprit, le JSX a un intérêt, celui de manipuler directement des éléments React.

Dans cette exemple, on va créer deux composants qui vont être utilisés dans un troisième.

```javascript

//1er composant
var Hello = () => {
  return <p>Hello</p>;
};
	
//2ème composant
var User = () => {
  var user = 'Gaël';
  return <span>{user}</span>;
};

```

Dans cette exemple, on a donc créé deux composants. L’un affichant simplement Hello et l’autre affichant le nom d’un utilisateur.

On va maintenant les composer, en JSX cela se réalise très simplement :

```javascript

//1er composant + 2ème componsant = un 3ème composant
var HelloUser = function() {
return (
 <div>
   <Hello />
   <User />
 </div>
)};

```


Le troisième composant, utilise les deux composants précédemment créés en utilisant leurs noms respectifs entre < et /> comme des balises HTML custom.

On peut voir dans ces exemples que tous les composants React commencent par des majuscules, c’est voulu car… obligatoire :-). 
Sans ça, React va penser qu’il s’agit d’un tag HTML standard.




Un composant React recevant des props
---

Nous allons légèrement modifier le composant User vu précédemment.

```javascript

var User = (props) => {
 var user = props.name;
 return <span>{user}</span>;
};

```

Il reçoit maintenant un argument props qui contient un attribut name.

Mais comment créer en JSX un composant HelloUser et lui passer l’argument User ?

```javascript

//Rappel du composant Hello
var Hello = () => {
  return <span>Hello</span>;
};
var HelloUser = () => {
  return (
    <div>
      <Hello />
      <User name='Gaël' />
    </div>
  );
}

```

Pour passer des props au composant User, on a simplement rajouté user="Gaël" entre les balises du composant. En faisant ça, l’objet { user : 'Gaël' } est passé en argument à la fonction qui crée le composant User.

De plus, en externalisant l’information du name du composant User, on vient de créer un composant réutilisable ! La force de React commence à apparaître ! :-)

Exemple:

```javascript

var HelloUser = function() {
  return (
    <div>
      <Hello />
      <User name='Jack' />
      <User name='John' />
      <User name='Billy Bop' />
    </div>
  );
}

```

Ici, une chaîne de caractère est passé en props mais grâce aux { }, objet, fonction ou variable JavaScript peuvent être utilisés.

Exemple :

```javascript

var PropsEnFolie = function() {
  var foo = 'bar';
  return (
    <User 
      string="Gaël" 
      tableau={ [1,2,3] }
      fonction={ function() { console.log( 'YOLO'); }
      objet={{ key : 'value', foo : 'bar' }}
      variable={foo}
    />
  );
}

```



Un composant React et ses “children”
---

Voyons maintenant une utilisation un peu plus avancé des props. On a le composant suivant :

```javascript

var Hello = function(props) {
	return <div>Hello {props.children}</div>
};

```

On peut se dire, à juste titre avec ce que l’on vient de voir, que que l’on va le composant Hello de la façon suivante :

```javascript

<Hello children={/* QUELQUE CHOSE */} />

```

mais en réalité, on a ça :
```javascript
<User>
  <span>John</span>
</User>
```

On découvre donc une nouvelle façon de manipuler le JSX :
```javascript
<MonComposant> {/*DU JSX ICI*/} </MonComposant>
```

