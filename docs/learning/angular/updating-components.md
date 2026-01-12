# Updating Component Class

La __logique __ et le __comportement du composant__ est défini à __l'intérieur de la classe `TypeScript` du composant__.

### Texte dynamique

Pour la création de ce __type de texte__, utilisation d'une __liaison(création connexion dynamique)__ entre le __modèle d'un composant__ et ses __données__.

```typescript
@Component({
  selector: 'user-profile',
  template: `<h1>Profile for {{userName}}</h1>`,
})
export class UserProfile {
  userName = 'pro_programmer_123';
}
// OU
@Component({
  selector: 'user-profile',
  template: `<h1>Profile for {{userName()}}</h1>`,
})
export class UserProfile {
  userName = signal('pro_programmer_123');
}
```

- `signal()` : Conteneur valeur, données prilitves ou structures de données complexes. Permet la traçabilité de l'utilisation, modification de cet élément

__Rendu `HTML`__ :

```html
<h1>Profile for pro_programmer_123</h1>
```

#### Update `userName`

```typescript
this.userName.set('cool-coder_789');
```

__Rendu `HTML`__ :

```html
<h1>Profile for cool_coder_789</h1>
```

---

## Paramètres propriétés & attributs

`Angular` prend en charge la __liaison__ de valeurs dynmaiques aux __propriétés DOM__.

```typescript
@Component({
  /*...*/
  // Set the `disabled` property of the button based on the value of `isValidUserId`.
  template: `<button [disabled]="!isValidUserId()">Save changes</button>`,
})
export class UserProfile {
  isValidUserId = signal(false);
}
```

---

## Date : 12 Janvier 2026