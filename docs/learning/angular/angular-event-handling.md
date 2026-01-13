# Event Handling

La gestion d'événements permet d'ajouter des **fonctionnalités interactives** aux composants en réagissant aux actions utilisateur.

---

### Event Listener

**Syntaxe :** `(eventName)="handler()"`

```typescript
@Component({
  template: `
    <button (click)="cancelSubscription()">Cancel subscription</button>
  `
})
export class UserProfile {
  cancelSubscription() {
    console.log('Subscription cancelled');
  }
}
```

---

## L'Objet `$event`

Possibilité de transmettre l'**objet événement** au handler en utilisant la variable `$event`.

**Syntaxe :** `(eventName)="handler($event)"`

```typescript
@Component({
  template: `
    <button (click)="cancelSubscription($event)">Cancel</button>
  `
})
export class UserProfile {
  cancelSubscription(event: MouseEvent) {
    console.log('Button clicked at:', event.clientX, event.clientY);
    event.preventDefault(); // Exemple d'utilisation
  }
}
```

**Types d'événements courants :**
- `MouseEvent` → click, dblclick, mouseenter, mouseleave
- `KeyboardEvent` → keydown, keyup, keypress
- `InputEvent` → input
- `FocusEvent` → focus, blur
- `SubmitEvent` → submit (formulaires)

---

## Types d'Événements Courants

### Click Events
```typescript
<button (click)="save()">Save</button>
<div (click)="onDivClick($event)">Clickable div</div>
<button (dblclick)="onDoubleClick()">Double click</button>
```

### Input Events (Saisie Utilisateur)
```typescript
<input (input)="onInputChange($event)" placeholder="Type something" />
<input (keyup)="onKeyUp($event)" placeholder="Press a key" />
<input (keydown)="onKeyDown($event)" />
<input (change)="onChange($event)" />
```

### Form Events
```typescript
<form (submit)="onSubmit($event)">
  <input type="text" />
  <button type="submit">Submit</button>
</form>
```

### Mouse Events
```typescript
<div (mouseenter)="onMouseEnter()">Hover me</div>
<div (mouseleave)="onMouseLeave()">Stop hovering</div>
```

### Focus Events
```typescript
<input (focus)="onFocus()" placeholder="Click me" />
<input (blur)="onBlur()" placeholder="Click outside" />
```

---

## Bonnes Pratiques

### 1. Typage des Événements
```typescript
onSubmit(event: SubmitEvent) { }
onClick(event: MouseEvent) { }
onInput(event: InputEvent) { }
```

### 2. Nommage des Handlers
```typescript
onSubmit() { }
onSearchChange() { }
onConsultantClick() { }
```

### 3. Prévenir Comportements par Défaut
```typescript
// Formulaires : empêcher rechargement
onSubmit(event: Event) {
  event.preventDefault();
  // ...
}

// Empêcher propagation événement
onButtonClick(event: Event) {
  event.stopPropagation();
  // ...
}
```

---

**Date** : 13 Janvier 2026