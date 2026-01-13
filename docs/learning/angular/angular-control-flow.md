# Control Flow

Mécanisme permettant d'afficher ou de répéter de manière **conditionnelle** des éléments dans les templates en fonction des données du composant.

---

## Types de Control Flow

### 1. Conditional Rendering (Show/Hide)

Affichage conditionnel avec `@if` / `@else` / `@else if`.

```typescript
<h1>User profile</h1>

@if (isAdmin()) {
  <h2>Admin settings</h2>
  <!-- Admin content -->
} @else {
  <h2>User settings</h2>
  <!-- User content -->
}
```

**Conditions multiples :**
```typescript
@if (a > b) {
  {{a}} is greater than {{b}}
} @else if (b > a) {
  {{a}} is less than {{b}}
} @else {
  {{a}} is equal to {{b}}
}
```

---

#### Sauvegarder le Résultat avec `as`

Enregistrement du résultat de l'expression conditionnelle dans une variable → Réutilisation à l'intérieur du bloc.

```typescript
@if (expression; as variableName) {
  <!-- Utilise variableName -->
}
```

---

### 2. List Rendering (Loops/Iteration)

Affichage multiple du contenu en itérant sur une collection.

```typescript
<h1>User profile</h1>
<ul class="user-badge-list">
  @for (badge of badges(); track badge.id) {
    <li class="user-badge">{{ badge.name }}</li>
  }
</ul>
```

#### Paramètre `track`

Maintenir une relation entre les données et les nœuds DOM.

**Best practice :**
```typescript
@for (item of items(); track item.id) { }  // Identifiant unique
@for (item of items(); track $index) { }   // Seulement si pas d'ID
```

---

#### Variables Implicites

Variables **automatiquement disponibles** dans un bloc `@for`.

| Variable | Type      | Description                                |
| -------- | --------- | ------------------------------------------ |
| `$count` | `number`  | Nombre total d'éléments dans la collection |
| `$index` | `number`  | Indice de la ligne actuelle (commence à 0) |
| `$first` | `boolean` | `true` si première itération               |
| `$last`  | `boolean` | `true` si dernière itération               |
| `$even`  | `boolean` | `true` si indice pair (0, 2, 4...)         |
| `$odd`   | `boolean` | `true` si indice impair (1, 3, 5...)       |

**Exemple d'utilisation :**
```typescript
@for (consultant of consultants(); track consultant.id) {
  <div [class.even]="$even" [class.odd]="$odd">
    <span>{{ $index + 1 }}/{{ $count }}</span>
    <h3>{{ consultant.name }}</h3>
    
    @if ($first) {
      <span class="badge">⭐ Premier</span>
    }
    
    @if ($last) {
      <span class="badge">🏁 Dernier</span>
    }
  </div>
}
```

**Aliasing (renommer variables) :**
```typescript
@for (item of items; track item.id; let idx = $index, isEven = $even) {
  <p>Item #{{ idx }}: {{ item.name }}</p>
  <span [class.highlight]="isEven">{{ isEven ? 'Pair' : 'Impair' }}</span>
}
```

---

#### @empty (Fallback)

Bloc optionnel affiché **si la collection est vide**.

```typescript
@for (item of items(); track item.id) {
  <p>{{ item.name }}</p>
} @empty {
  <p>Aucun élément à afficher</p>
}
```

---

### 3. Switch (Choix Multiple)

Affiche **un seul cas** parmi plusieurs options basées sur une valeur.

```typescript
@switch (consultantStatus()) {
  @case ('available') {
    <span class="badge green">Disponible</span>
    <button>Affecter à une mission</button>
  }
  @case ('on-mission') {
    <span class="badge orange">En mission</span>
  }
  @case ('on-leave') {
    <span class="badge blue">En congés</span>
  }
  @default {
    <span class="badge gray">Statut inconnu</span>
  }
}
```

---

**Date** : 13 Janvier 2026