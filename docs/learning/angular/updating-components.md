# Data Binding & Component State

La **logique** et le **comportement du composant** sont définis à l'intérieur de la **classe TypeScript du composant**.

---

## Interpolation (Texte Dynamique)

Pour créer du **texte dynamique**, Angular utilise une **liaison (binding)** entre le **template** et les **données du composant**.

### Sans Signals (Propriété classique)
```typescript
@Component({
  selector: 'app-user-profile',
  template: `<h1>Profile for {{ userName }}</h1>`
})
export class UserProfile {
  userName = 'pro_programmer_123';
}
```

**Rendu HTML :**
```html
<h1>Profile for pro_programmer_123</h1>
```

---

### Avec Signals (Approche moderne - Angular 16+)
```typescript
@Component({
  selector: 'app-user-profile',
  template: `<h1>Profile for {{ userName() }}</h1>`
})
export class UserProfile {
  userName = signal('pro_programmer_123');
}
```

**Rendu HTML :**
```html
<h1>Profile for pro_programmer_123</h1>
```

---

## Qu'est-ce qu'un Signal ?

**`signal()`** est une API Angular pour gérer l'état réactif.

**Définition :**
Un signal est un **conteneur** pour une valeur (primitive ou complexe) qui permet à Angular de :
- Tracer automatiquement l'utilisation de cette valeur
- Détecter précisément les changements
- Mettre à jour uniquement ce qui est nécessaire

**Syntaxe :**
```typescript
// Création
userName = signal('initial_value');

// Lecture (avec parenthèses)
const name = this.userName();

// Modification
this.userName.set('new_value');

// Dans le template (avec parenthèses)
{{ userName() }}
```

---

## Modifier la Valeur d'un Signal
```typescript
@Component({
  template: `<h1>Profile for {{ userName() }}</h1>`
})
export class UserProfile {
  userName = signal('pro_programmer_123');
  
  updateUsername() {
    // Modification avec .set()
    this.userName.set('cool_coder_789');
  }
}
```

**Avant modification :**
```html
<h1>Profile for pro_programmer_123</h1>
```

**Après appel de `updateUsername()` :**
```html
<h1>Profile for cool_coder_789</h1>
```

**Angular détecte automatiquement le changement et met à jour le DOM !**

---

## Property Binding (Propriétés DOM)

Angular permet de **lier dynamiquement** des valeurs aux **propriétés DOM** (disabled, src, value, etc.).

**Syntaxe :** `[property]="expression"`
```typescript
@Component({
  template: `
    <button [disabled]="!isValidUserId()">Save changes</button>
  `
})
export class UserProfile {
  isValidUserId = signal(false);
}
```

**Rendu quand `isValidUserId = false` :**
```html
<button disabled>Save changes</button>
```

**Rendu quand `isValidUserId = true` :**
```html
<button>Save changes</button>
```

---

## Interpolation vs Property Binding

| Type                 | Syntaxe      | Usage                  | Exemple                        |
| -------------------- | ------------ | ---------------------- | ------------------------------ |
| **Interpolation**    | `{{ }}`      | Afficher du texte      | `<h1>{{ title }}</h1>`         |
| **Property Binding** | `[property]` | Modifier propriété DOM | `<button [disabled]="!valid">` |

**Différence clé :**
- `{{ }}` → Convertit en **texte** (string)
- `[property]` → Lie la **valeur native** (boolean, number, object...)

---

**Date** : 12 Janvier 2026