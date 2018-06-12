## Prezentacja.

Prezentacja dotycząca Angular 5 jest dostępna tutaj:

## Zadanie

Poniżej przedstawiam tutorial do prostego zadania, z wykorzytaniem Angulara:

### 1. Środowisko:

Do zabawy wykorzytamy prosty edytor online [stacklitz](https://stackblitz.com/edit/angular-playground), aby nie tracić czasu na instalację Angulara*.

### 2. Treść zadania:

a. Pobieranie:

Pobierz plik zwierający bazową aplikację: [apka-zti-zip](https://drive.google.com/open?id=1DjPmLxAjRnreoLplSOVjamRISveB_VyB)

b. Przygotowanie aplikacji:

Rozpakuj plik, a następnie wejdź w edytor online [stacklitz](https://stackblitz.com/edit/angular-playground)
W edytorze są przygotowane poszczególne foldery i bazowe komponenty, jednak zastąp je tymi, które znajdują się w rozpakowanym przez Ciebie folderze, w katalogu **/src/**
- usuń wszystkie foldery i pliki **POMIJAJĄC: .angular-cli.json, main.ts, polyfills.ts** 
- zaznacz całą zarawtość folderu  **/src/** i przeciągnij

zawartość katalogów powinna wyglądać następująco:

![img-katalog](/images/katalog.png)
aplikacja wygląda następująco:
![img-apka](/images/apka.png)


WAŻNE! Plik **.angular-cli.json** powinien wyglądać następująco:

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

c. Stworzenie nowego komponentu - wyświetlenie detali postów

Cała aplikacja nie jest skomplikowana i zawiera jeden link do wszystkich postów (źródło [to api](https://jsonplaceholder.typicode.com))




----------------------------------------------------------------------------------------------------------------------------------------
* Dla ciekawskich, wszystko (instalacja + quickstart) jest pięknie wyjaśnione na stronie [Angular-a](https://angular.io)
