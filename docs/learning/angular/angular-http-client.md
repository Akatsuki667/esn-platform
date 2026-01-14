# HTTP Client

__Module intégré `Angular`__ permettant des __requêtes `HTTP`__ à un serveur backend (__API__).

---

## HTTP Methods

- `GET` : Récupération de __données__

  ```typescript
  http.get<Type>(url) // Syntaxe
  
  import {HttpClient} from '@angular/common/http';
  
  @Injectable({provideIn: 'root'})
  export class ConsultantService {
      private http = inject(HttpClient);
      private apiUrl = 'http://localhost:8080/api/v1/consultants';
      
      getConsultant() {
          return this.http.get<Consultant[]>(this.apiUrl)
      }
  }
  ```

  

- `POST` : Création de __données__

  ```typescript
  http.post<Type>(url, body) // Syntaxe
  
  import {HttpClient} from '@angular/common/http';
  
  @Injectable({provideIn: 'root'})
  export class ConsultantService {
      private http = inject(HttpClient);
      private apiUrl = 'http://localhost:8080/api/v1/consultants';
      
      createConsultant(data: CreateConsultantRequest) {
          return this.http.post<Consultant>(this.apiUrl, data);
      }
  ```

  

- `PUT` : Modification de __données__

  ```typescript
  http.put<Type>(url, body) // Syntaxe
  
  import {HttpClient} from '@angular/common/http';
  
  @Injectable({provideIn: 'root'})
  export class ConsultantService {
      private http = inject(HttpClient);
      private apiUrl = 'http://localhost:8080/api/v1/consultants';
      
      updateConsultant(id: number, data: UpdateConsultantRequest) {
          return this.http.put<Consultant>(`${this.apiUrl}/${id}`, data);
      }
  }
  ```

  

- `DELETE` : Suppression de __données__

  ```typescript
  http.delete<Type>(url) // Syntaxe
  
  import {HttpClient} from '@angular/common/http';
  
  @Injectable({provideIn: 'root'})
  export class ConsultantService {
      private http = inject(HttpClient);
      private apiUrl = 'http://localhost:8080/api/v1/consultants';
      
      deleteConsultant(id: number) {
          return this.http.delete<void>(`${this.apiUrl}/${id}`);
      }
  ```

---

## Observables

__Flux de données__ qui peut émettre des valeurs au fil du temps.
Les __requêtes HTTP `Angular`__ retourne des __Observables__, pas de valeur direct.

- __Asynchrone__
- __Annulable__ : Annulation __requête__ en cours

---

## `subscribe()` - Exécution de requête & Gestion d'erreur

Méthode qui déclenche la __requête `HTTP`__ et gère la __réponse__.

```typescript
observable.subscribe({
  next: (data) => { /* Handle success */ },
  error: (error) => { /* Handle error */ },
  complete: () => { /* Optional: called when done */ }
})

@Component({ /* ... */ })
export class ConsultantList implements OnInit {
  consultantService = inject(ConsultantService);
  consultants = signal<Consultant[]>([]);
  
  ngOnInit() {
    this.consultantService.getConsultants()
      .subscribe({
        next: (data) => {
          this.consultants.set(data);
        },
        error: (error) => {
          console.error('Error fetching consultants:', error);
        }
      });
  }
}
```

---

## `ngOnInit()` - Lifecycle Hook

__Hook__ : __Point d'entrée__ dans le cycle de vie d'un __composant__.
__Lifecycle(Création/Destruction)__ : Différentes étapes par lesquelles passe un __composant__.

### Cycle de vie composant

```bash
1. constructor()       ← Création de la classe
2. ngOnInit()          ← Initialisation
3. ngAfterViewInit()   ← Vue affichée
4. ngOnDestroy()       ← Destruction (cleanup)
```

```typescript
import { OnInit } from '@angular/core';

export class MyComponent implements OnInit {
  ngOnInit() {
    // Load data here
    this.loadConsultants();
  }
  
  loadConsultants() {
    this.consultantService.getConsultants()
      .subscribe(data => this.consultants.set(data));
  }
}
```

- __Constructor__ s'exécute
- `ngOnInit` s'exécute
- Rendu __composant__

---

## HTTP Error Object

- `error.status` : `HTTP` status code
- `error.message` : Message d'erreur
- `error.error` : __Réponse__ d'erreur backend

---

## Request Options

- `headers` : __En-têtes HTTP__, transport des __métadonnées__. Permet l'__authentification__ via __token__ utilisateur, définit le __format des données__.

  ```typescript
  import { HttpHeaders } from '@angular/common/http';
  
  // Création de la classe HttpHeaders
  const headers = new HttpHeaders({
    'Content-Type': 'application/json',
    'Authorization': 'Bearer ' + token
  });
  
  this.http.get(url, { headers })
    .subscribe(/* ... */);
  ```

---

## Query Parameters

Paires __clé-valeur__ ajoutés à la fin de l'__URL__. Permet __affinage__, __trier__, ou  __filtré__ une __ressource__ demandée.

```typescript
import { HttpParams } from '@angular/common/http';

// Création classe HttpParams
const params = new HttpParams()
  .set('status', 'available')
  .set('limit', '10');

// URL becomes: /api/consultants?status=available&limit=10
this.http.get(url, { params })
  .subscribe(/* ... */);
```

---

**Date** : 14 janvier 2026