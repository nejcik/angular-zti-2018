## Prezentacja.

Prezentacja dotycząca Angular 5 jest dostępna [tutaj](https://docs.google.com/presentation/d/1tDjAQD24NfvkbNOklPTW4DhHPA73MrJtGaDd9DHsLjY/edit?usp=sharing)

# Zadanie

Poniżej przedstawiam tutorial do prostego zadania, z wykorzytaniem Angulara:

## 1. Środowisko:

Do zabawy wykorzytamy prosty edytor online [stacklitz](https://stackblitz.com/edit/angular-playground), aby nie tracić czasu na instalację Angulara[1].

## 2. Treść zadania:

### a. Pobieranie:

Pobierz plik zwierający bazową aplikację: [angular-app-zti-zip](https://drive.google.com/open?id=1DjPmLxAjRnreoLplSOVjamRISveB_VyB)

### b. Przygotowanie aplikacji:

Rozpakuj plik, a następnie wejdź w edytor online [stacklitz](https://stackblitz.com/edit/angular-playground).


W edytorze są przygotowane poszczególne foldery i bazowe komponenty, jednak zastąp je tymi, które znajdują się w rozpakowanym przez Ciebie folderze, w katalogu **/src/**
- usuń wszystkie foldery i pliki **POMIJAJĄC: .angular-cli.json** 
- zaznacz całą _zawartość_ folderu  **/src/** i przeciągnij w miejsce **FILES** na stronie

zawartość katalogów powinna wyglądać następująco:

![img-katalog](/images/katalogi.png)


aplikacja wygląda następująco:


![img-apka](/images/apka.png)


**WAŻNE!** Plik **.angular-cli.json** powinien wyglądać następująco:

```json
{
  "apps": [{
    "styles": [
      "scss/styles.scss",
      "scss/material-theme.scss",
      "app/app.component.scss",
      "app/posts/posts.component.scss",
      "app/hello-framework/hello-framework.component.scss"
    ]
  }]
}
```

### c. Stworzenie nowego komponentu - wyświetlenie detali postów:

Cała aplikacja nie jest skomplikowana i zawiera jeden link do wszystkich postów (źródło [to api](https://jsonplaceholder.typicode.com)). Twoim zadaniem bedzie stworzenie komponentu Details wyświetlającego jeden post o danym id

#### A. Bazowe pliki:
Stwórz folder **app/details**, a w środku stwórz następujące pliki: **details.component.html, details.component.scss, details.component.ts**

#### B. Import w app.module:
W pliku **app.module.ts** zaimportuj component details:

```typescript 
import { DetailsComponent } from './details/details.component';
```

I dodaj do listy deklaracji:

```typescript 
...
@NgModule({
  declarations: [
    AppComponent, 
    HelloFrameworkComponent,
    SidebarComponent,
    PostsComponent,
    DetailsComponent
  ],
...
```

#### C. Dodanie ścieżki w Routes:

W pliku **app-routing.module.ts** zaimportuj nowy komponent oraz dodaj ścieżkę _"details/:id"_ do listy:

```typescript 
...
// !!!!
import { DetailsComponent } from './details/details.component';

...

 const routes: Routes = [
  {
      path: 'posts',
      component: PostsComponent
  },
  {
    path: '',
    component: HelloFrameworkComponent
  },
  // DODAJ TO CO JEST PONIŻEJ:
  {
    path: 'post-details/:id',
    component: DetailsComponent
  }
];
...
```


#### D. Metoda w DataService:

W pliku **data.service.ts** poniżej zdefiniowanej metody _getPosts()_ dodaj metode **getDetails()**:

```typescript
getDetails(postId) {
    return this.http.get('https://jsonplaceholder.typicode.com/posts/'+postId)
  }
```

#### E. Przygotuj Component Details:

W pliku komponentu **details.component.ts** zaimportuj następujące komponenty/biblioteki: **Component, OnInit, DataService, Observable, ActivatedRoute**, dodaj dekorator **@Components** z odpowiednim selektorem (nazwa dowolna) oraz ścieżką do html-a (templateUrl). 
Jako przykład można wziąć plik **posts.component.ts**.

Aby właściwie wyciągnąć dane z DataService, trzeba dodać informację dotyczącą id tego postu, przypisujemy jako parametry funkcji _subscribe()_ następująco: _params => this.post$ = params.id_

Cały komponent powinien wyglądać następująco:

```typescript

import { Component, OnInit } from '@angular/core';
import { DataService } from '../data.service';
import { Observable } from 'rxjs';
import { ActivatedRoute } from "@angular/router";

@Component({
  selector: 'app-details',
  templateUrl: './details.component.html',
  styleUrls: ['./details.component.scss']
})
export class DetailsComponent implements OnInit {

  post$: Object;
  
  constructor(private route: ActivatedRoute, private data: DataService) { 
     this.route.params.subscribe( params => this.post$ = params.id );
  }

  ngOnInit() {
    this.data.getDetails(this.post$).subscribe(
      data => this.post$ = data 
    );
  }

}
```

#### F. Wygląd pojedynczego postu + routeLink:

do pliku  **.angular-cli.json** dodaj następującą linię:
```json
"app/details/details.component.scss"
```

W pliku **details.component.html** powinno się znajdować

<?PHP
call_some_php_function(1,2,"a","b"); /* This is may return nothing, a text string, or actual HTML markup code */
?>
```
<h5>"{{ post$.title }\}"</h5>
<p>/{/{ post$.body /}/}</p>
<ul>
  <li><strong>Post id:</strong> /{/{ post$.id /}/}</li>
  <li><strong>User Id:</strong> \{\{ post$.userId \}\}</li>
</ul>
```
Jeżeli się nie wyświetlają porawnie dyrektywy - screen: 
[img-html](images/html.png)

Aby przejść pojedynczego postu, trzeba zmienić w pliku **posts.component.html** bazowy link **href="#"** na następujący: 
```
routerLink="/post-details/{{post.id}}?>"
```

----------------------------------------------------------------------------------------------------------------------------------------
[1] Dla ciekawskich, wszystko (instalacja + quickstart) jest pięknie wyjaśnione na stronie [Angular-a](https://angular.io)
