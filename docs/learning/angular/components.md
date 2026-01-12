# Composants

Éléments constitutifs fondamentaux de toute application `Angular`. Chaque __composant__ comporte 3  parties :

- `TypeScript` classe
- `HTML` template
- `CSS` styles

---

## Structure Composant

```typescript
// user-profile.ts
@Component({
  selector: 'user-profile',
  template: `
    <h1>User profile</h1>
    <p>This is the user profile page</p>
  `,
  styles: `h1 { font-size: 3em; } `,
})
export class UserProfile { /* Your component code goes here */ }
```

- `@Component` : Decorator de configuration du composant.
- `selector` : __HTML tag name__
- `template` : Code __HTML__
- `styles` : Propriétés `CSS`

### Comment cela fonctionne ?

1. Définition du __composant__.

   ```typescript
   @Component({
     selector: 'user-profile',  // ← This is the custom HTML tag name
     template: `
       <h1>User profile</h1>
       <p>This is the user profile page</p>
     `,
     styles: `h1 { font-size: 3em; } `,
   })
   export class UserProfile { }
   ```

2. Utilisation dans un autre __composant__.

   ```html
   <!-- In another component's template -->
   <div>
     <user-profile></user-profile>  <!-- ← Using the selector -->
   </div>
   ```

3. Rendu `Angular`.

   ```html
   <!-- Result in the browser -->
   <div>
     <user-profile>
       <h1>User profile</h1>
       <p>This is the user profile page</p>
     </user-profile>
   </div>
   ```

---

## Structure Composant Séparation

Définition d'un composant avec fichiers `.html` et `.css`.

```typescript
// user-profile.ts
@Component({
  selector: 'user-profile',
  templateUrl: 'user-profile.html',
  styleUrl: 'user-profile.css',
})
export class UserProfile {
  // Component behavior is defined in here
}
```

---

```typescript
<!-- user-profile.html -->
<h1>User profile</h1>
<p>This is the user profile page</p>
```

---

```typescript
/* user-profile.css */
h1 {
  font-size: 3em;
}
```

---

## Importation d'autres composants

```typescript
// user-profile.ts
import {ProfilePhoto} from 'profile-photo.ts';
@Component({
  selector: 'user-profile',
  imports: [ProfilePhoto],
  template: `
    <h1>User profile</h1>
    <profile-photo />
    <p>This is the user profile page</p>
  `,
})
export class UserProfile {
  // Component behavior is defined in here
}
```

- `import {} from ''` : Import du __composant__ au `fichier.ts`
- `imports : []` : Tableau d'entrée du composant importé
- `template` : Ajout composant importé

---

## Date : 12 Janvier 2026