# Projekt zaliczeniowy z przedmiotu Web Development 23/24

Aplikacja to-do stworzona za pomocą stacku **MEVN**.

### MEVN tech stack

- MongoDB
- Express.js
- Vue.js
- Node.js

Dla uruchominia backendu i frontednu niezbędny jest Node.js <https://nodejs.org/en/download>.

### Uruchomienie backendu

Serwis `mongod` musi być zainstalowany i uruchomiony w  tle, w moim przypadku za pomocą poniższych poleceń.

``` zsh
brew install mongodb-community
brew services start mongodb-community
```

Dalej należy uruchomić serwer Express.js wraz z bazą danych MongoDB.

```zsh
cd backend
node server.js
```

Serwer backend: `http://localhost:8080/`

Baza danych: `mongodb://localhost:27017/mevn-todo_db`

### Uruchomienie frontendu

```zsh
cd frontend
npm run serve
```

Aplikacja działa pod adresem `http://localhost:8081/`

### Lista metod REST API

#### POST `/api/tutorials` - tworzy nowe Todo

#### GET `/api/tutorials` - zwraca wszystkie Todo

#### GET `/api/tutorials/:id` - zwraca Todo według id

#### PUT `/api/tutorials/:id` - aktualizuje Todo według id

#### DELETE `/api/tutorials/:id` - usuwa Todo według id

#### DELETE `/api/tutorials` - usuwa wszystkie Todo

#### GET `/api/tutorials?title=[keyword]` - szuka wszystkie Todo, których tytuł zawiera słowo kluczowe
