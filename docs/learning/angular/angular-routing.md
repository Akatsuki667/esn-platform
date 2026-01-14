# `Angular Router`

`@angular/router` : __Bibliothèque officielle__ permettant la gestion de navigation dans l'application. Inclut par défaut dans tous les projets crées par `Angular CLI`.

---

## Single-Page Application

__SPA__ permet au navigateur d'effectuer une seul __requête__ après du __serveur Web__ pour le première `index.html`. Ensuite, un __routeur__ côté __client__ prend le relais et contrôle le contenu affiché en fonction de l'__URL__ (Le __routeur__ MAJ le contenu de la page sans déclencher un rechargement complet de cette dernière).

---

## Routage

Comprend 3 parties principales :

1. __Routes__

   **Configuration** qui définit quel **composant** s'affiche pour une **URL** spécifique.

   ```typescript
   import { Routes } from '@angular/router';
   
   export const routes: Routes = [
     { path: '', component: HomeComponent },
     { path: 'consultants', component: ConsultantListComponent },
     { path: 'consultants/:id', component: ConsultantDetailComponent },
     { path: 'missions', component: MissionListComponent },
     { path: '**', component: NotFoundComponent }  // 404
   ];
   ```

   __Patterns de `path`__ :

   - `''` : Racine(/)

   - `'coonsultants'` : /consultants

   - `'consultants/:id'` : /consultants/123(paramètre)

   - `'**'` : Wildcard(Toute __URL__ inconnue)

     

2. __Router Outlet__

   __Espace réservé(placeholder)__ dans le __template__ où le __routeur__ affiche les composants selon la __route active__.

   ```typescript
   @Component({
     template: `
       <nav>
         <a routerLink="/">Accueil</a>
         <a routerLink="/consultants">Consultants</a>
       </nav>
       
       <router-outlet />  ← Le composant s'affiche ici
     `
   })
   ```

   - L'utilisateur clique sur un lien --> l'__URL__ change

   - Le __routeur__ trouve la route correspondante

   - Le __composant se charge dans  <router-outlet />

     

3. __Links (RouterLink)__

   __Directive `Angular`__ pour lier des éléments cliquables à des __routes__.

   ```typescript
   // Path simple
   <a routerLink="/consultants">Consultants</a>
   
   // Syntaxe tableau (recommandée)
   <a [routerLink]="['/consultants']">Consultants</a>
   
   // Avec paramètres
   <a [routerLink]="['/consultants', 123]">Consultant 123</a>
   
   // Avec query params
   <a [routerLink]="['/consultants']" [queryParams]="{status: 'available'}">
     Consultants disponibles
   </a>
   
   // Style pour lien actif
   <a routerLink="/consultants" routerLinkActive="active">
     Consultants
   </a>
   ```

4. __Setup__

   Activation du __routing__.

   ```typescript
   // main.ts ou app.config.ts
   import { provideRouter } from '@angular/router';
   import { routes } from './app.routes';
   
   export const appConfig = {
     providers: [
       provideRouter(routes)
     ]
   };
   ```

5. __Navigation Programmatique__

   Naviguer vers une route depuis le code `TypeScript`.

   ```typescript
   import { Router } from '@angular/router';
   import { inject } from '@angular/core';
   
   @Component({ /* ... */ })
   export class ConsultantForm {
     private router = inject(Router); // injecction de dépendances
     
     onSubmit() {
       // Sauvegarder le consultant...
       
       // Naviguer vers la liste
       this.router.navigate(['/consultants']);
     }
     
     goToDetail(id: number) {
       this.router.navigate(['/consultants', id]);
       // Navigue vers : /consultants/123
     }
   }
   ```

6. __Paramètres de routes__

   __Valeurs dynamiques__ dans le chemin de l'__URL__. 

   Accès avec `ActivatedRoute` :

   ```typescript
   import { ActivatedRoute } from '@angular/router';
   import { inject } from '@angular/core';
   
   @Component({ /* ... */ })
   export class ConsultantDetail implements OnInit {
     private route = inject(ActivatedRoute);
     consultantId: number;
     
     ngOnInit() {
       this.consultantId = Number(this.route.snapshot.params['id']);
       this.loadConsultant(this.consultantId);
     }
   }
   ```

   Accès avec __Component Input Binding__ :

   ```typescript
   // Activer dans la config
   providers: [provideRouter(routes, withComponentInputBinding())]
   
   // Dans le composant
   @Component({ /* ... */ })
   export class ConsultantDetail {
     @Input() id!: number;  // Auto-rempli depuis :id
     
     ngOnInit() {
       this.loadConsultant(this.id);
     }
   }
   ```

7. __Route Wildcard (404)__

   Route catch-all pour __URL__ inconnues.

   ```typescript
   export const routes: Routes = [
     { path: '', component: HomeComponent },
     { path: 'consultants', component: ConsultantListComponent },
     { path: '**', component: NotFoundComponent }  // ← Doit être en dernier !
   ];
   ```

8. __Autres Fonctionnalités__ :

   - __Routes imbriquées__
   - __Query parameters__
   - __Guards de routes__ (Protection de __route__)
   - __Lazy loading__ (Chargement des __modules__ à la demande)
   - __Transitions de vue__ (Animations)
   - __ActivatedRoute__ (Accès aux informations de __route__)

---

**Date**: 14 Janvier 2026