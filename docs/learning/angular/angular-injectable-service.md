# Services & Dependency Injection

## Dependency Injection (DI)

Design pattern permettant à une classe de **recevoir ses dépendances** de l'extérieur plutôt que de les créer elle-même.

**Dépendance :** Tout **objet**, **valeur**, **fonction** ou **service** dont une **classe** a besoin pour fonctionner.

- **Testabilité** (facile de mocker pour les tests)
- **Réutilisabilité** (partage entre composants)
- **Découplage** (indépendance des implémentations)

---

## Service

Un **service `Angular`** est une **classe TypeScript** avec le **decorator `@Injectable`** qui permet de créer une **instance injectable** comme **dépendance**. Partage de **données** et de **fonctionnalités** entre **composants**.
```typescript
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class AnalyticsLogger {
  trackEvent(category: string, value: string) {
    console.log('Analytics event logged:', {
      category,
      value,
      timestamp: new Date().toISOString()
    });
  }
}
```

**`providedIn: 'root'`** : Rend ce **service** disponible dans toute l'application en tant que **singleton** (une seule instance partagée).

---

## Types de Services

- **Data clients** : Gestion des requêtes HTTP vers le serveur
- **State management** : Partage d'état entre composants/pages
- **Authentication & Authorization** : Gestion authentification et tokens
- **Logging & Error handling** : Journalisation et gestion d'erreurs
- **Utility functions** : Fonctions réutilisables (formatage, validation, etc.)

---

## Fonction `inject()`

Fonction permettant d'**injecter des dépendances** dans un **composant** ou **service**.
```typescript
import { Component, inject } from '@angular/core';
import { Router } from '@angular/router';
import { AnalyticsLogger } from './analytics-logger';

@Component({
  selector: 'app-navbar',
  template: `
    <a href="#" (click)="navigateToDetail($event)">Detail Page</a>
  `
})
export class Navbar {
  private router = inject(Router);
  private analytics = inject(AnalyticsLogger);
  
  navigateToDetail(event: Event) {
    event.preventDefault();
    this.analytics.trackEvent('navigation', '/details');
    this.router.navigate(['/details']);
  }
}
```

---

### Où Utiliser `inject()` ?
```typescript
@Component({ /* ... */ })
export class MyComponent {
  // ✅ Dans l'initialiseur de champ (recommandé)
  private service = inject(MyService);
  
  // ✅ Dans le constructor
  private anotherService: MyService;
  constructor() {
    this.anotherService = inject(MyService);
  }
```

**Important :** `inject()` fonctionne uniquement pendant la construction du **composant**.

---

**Date** : 13 Janvier 2026