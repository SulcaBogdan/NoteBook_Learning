# Variabilele in Postman

Variabilele în Postman sunt valori dinamice pe care le poți utiliza pentru a simplifica și a face mai eficientă gestionarea cererilor API. Ele îți permit să reutilizezi valori comune, cum ar fi URL-urile de bază, cheile API, token-urile de autentificare și altele, fără a trebui să le scrii de fiecare dată manual.

### Tipuri de variabile în Postman

1. **Global variables**: Aceste variabile sunt disponibile în toate colecțiile și mediile Postman. Sunt utile pentru valori care trebuie să fie accesibile universal în sesiunile Postman.

2. **Environment variables**: Aceste variabile sunt specifice unui mediu de lucru (de exemplu, dezvoltare, testare, producție). Ele te ajută să gestionezi diferite configurații și să schimbi rapid setările între diferite medii.

3. **Collection variables**: Aceste variabile sunt specifice unei colecții și pot fi utilizate de toate cererile din acea colecție.

4. **Data variables**: Aceste variabile sunt folosite în timpul rulării testelor de performanță sau a seturilor de cereri cu Postman Runner, permițându-ți să folosești un set de date pentru testarea în masă.

5. **Local variables**: Aceste variabile sunt definite și utilizate în cadrul unei cereri sau scripturi de testare și nu sunt disponibile în afara acestora.

### Cum să folosești variabilele în Postman

#### Definirea variabilelor

1. **Global variables**:
   - Accesează "Manage Environments" din iconița de setări (roată dințată).
   - Selectează tab-ul "Globals" și adaugă variabilele dorite.

2. **Environment variables**:
   - Creează sau editează un mediu accesând "Manage Environments".
   - Adaugă variabilele necesare în cadrul mediului respectiv.

3. **Collection variables**:
   - Deschide colecția dorită.
   - Accesează tab-ul "Variables" și adaugă variabilele dorite.

#### Utilizarea variabilelor în cereri

Poți folosi variabilele în URL-uri, header-e, corpuri de cerere și scripturi utilizând sintaxa `{{variableName}}`.

Exemplu:

1. **Setare variabilă globală**:
   - Nume: `baseUrl`
   - Valoare: `https://api.example.com`

2. **Utilizare variabilă în cerere**:
   ```plaintext
   {{baseUrl}}/users
   ```

### Setarea și accesarea variabilelor în scripturi

#### Scripturi pre-request

Aceste scripturi sunt executate înainte de trimiterea cererii și pot fi folosite pentru a seta valori dinamice.

```javascript
// Setare variabilă de mediu
pm.environment.set("userId", "12345");

// Setare variabilă globală
pm.globals.set("authToken", "abcdef123456");
```

#### Scripturi de testare

Aceste scripturi sunt executate după primirea răspunsului și pot fi folosite pentru a extrage și stoca valori din răspuns.

```javascript
// Obține răspunsul în format JSON
let response = pm.response.json();

// Setare variabilă din răspuns
pm.environment.set("userId", response.id);

// Verifică răspunsul și stochează un token de autentificare
if(response.token) {
    pm.globals.set("authToken", response.token);
}
```

### Exemplu practic

#### Definirea unui mediu

1. Creează un mediu numit "Development" și adaugă următoarele variabile:
   - `baseUrl`: `https://dev.api.example.com`
   - `authToken`: `12345`

#### Utilizarea variabilelor în cerere

URL-ul cererii:
```plaintext
{{baseUrl}}/users
```

Header-ul cererii:
```json
{
  "Authorization": "Bearer {{authToken}}"
}
```

#### Script pre-request pentru setarea variabilelor

```javascript
// Generarea unui ID de utilizator random și setarea sa ca variabilă de mediu
pm.environment.set("randomUserId", Math.floor(Math.random() * 1000));

// Setarea unui header personalizat
pm.request.headers.add({key: "Custom-Header", value: "Value"});
```

#### Script de testare pentru extragerea datelor din răspuns

```javascript
// Obține răspunsul în format JSON
let response = pm.response.json();

// Setează variabile din răspuns
pm.environment.set("userId", response.data.id);
pm.environment.set("userEmail", response.data.email);

// Verifică dacă token-ul de autentificare există și setează-l ca variabilă globală
if (response.token) {
    pm.globals.set("authToken", response.token);
}
```

### Concluzie

Variabilele în Postman sunt esențiale pentru a face cererile API mai flexibile și mai ușor de gestionat. Ele permit reutilizarea valorilor comune și schimbarea rapidă între diferite medii, facilitând dezvoltarea, testarea și automatizarea API-urilor.