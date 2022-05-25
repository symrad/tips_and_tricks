# Typescript

## Partial
  
  Rende gli attributi di un'interfaccia opzionali
  ```typescript
  interface User{
    name:string;
    surname: string;
    age:string;
  }
  type PartialUser = Partial<User>
  const user:PartialUser = {
    name: 'Simone'
  }
  //no errors
  console.log(user);
  ```

## [Required](https://codesandbox.io/embed/quirky-johnson-ggxn6?expanddevtools=1&fontsize=14&hidenavigation=1&theme=dark)

  Rende tutti gli attributi di un'interfaccia obbligatori

## [Pick](https://codesandbox.io/embed/gifted-ardinghelli-90nse?expanddevtools=1&fontsize=14&hidenavigation=1&theme=dark)
  
  Permette di utilizzare una parte di attributi di un'interfaccia. Primo parametro l'interfaccia da cui partire, secondo parametro lista di attributi da includere.
  
  ```typescript
  interface Todo {
    title: string;
    description: string;
    completed: boolean;
  }

  type TodoPreview = Pick<Todo, "title" | "completed">;

  const todo: TodoPreview = {
    title: "Clean room",
    completed: false,
  };
  ```
  
## [Omit](https://codesandbox.io/embed/pedantic-framework-pe3xv?expanddevtools=1&fontsize=14&hidenavigation=1&theme=dark)
  
  Permette di omettere una parte di attributi di un'interfaccia. Primo parametro l'interfaccia da cui partire, secondo parametro lista di attributi da escludere.
  
## Rendere un oggetto immutabile
  Applicato su un oggetto, tutto l'oggetto diventa in sola lettura, funziona a tutti i livelli (fino a degree).
  Se applicato sull'array lo rende immutabile, non dando la possibità di aggiungere o rimuovere elementi oltre alla riassegnazione.
  
  ### as const
  ```typescript
  // 
  const user:PartialUser = {
    name: 'Simone',
    surname: 'Pippo',
    age: 30,
    education: {
      degree: '2'
    }
  } as const;
  // 
  const skills = ['javascript', typescript'];
  ```

  ### readonly
  
  Non agisce su sotto attributi (è possibile fare user.education.degree = '1') e non agisce su immutabilità di un array. 
  Per array permette di aggiungere e togliere elementi ma non di fare la riassegnazione ( non è possibile fare user.skills = [])
  
   ```typescript
  const user:PartialUser = {
    readonly name: 'Simone',
    readonly surname: 'Pippo',
    age: 30,
    readonly education: {
      degree: '2'
    }
    readonly skills: ['typescript', 'javascript']
  };
   ```
  
  ### ReadonlyArray
  
  Per fare in modo che un array sia completamente immutabile, non si può aggiungere o togliere elementi
  
  ```typescript
  const user:PartialUser = {
    readonly name: 'Simone',
    readonly surname: 'Pippo',
    age: 30,
    readonly education: {
      degree: '2'
    }
    skills: ReadonlyArray<string>
  };
   ```
   
  ### Ignorare valori null o undefined 
  
  ```typescript
  interface User = {
    name:string;
    surname:string;
    profession?:string;
  };
  const user = {
    name: 'Simone',
    surname: 'Pippo',
    profession: 'Engineer'
  };
  
  //mi da errore perchè potrebbe anche essere undefined, non essendo obbligatorio
  const profession:string = user.profession;
  
  //per evitare che si presenti l'errore usiamo l'operatore !
  const profession:string = user.profession!;
  ```
  
  ### [Creare tipo da un oggetto](https://codesandbox.io/embed/great-fog-dvdyu?expanddevtools=1&fontsize=14&hidenavigation=1&theme=dark)
  ```typescript
  const user = {
    name: "John Doe",
    age: 27
  };

  type User = typeof user;

  const user2: User = {
    age: 28,
    name: "Jane Doe"
  };
  ```
  
  ### [any vs unknow](https://codesandbox.io/embed/admiring-bas-g3mrh?fontsize=14&hidenavigation=1&theme=dark)
  se non si conosce il tipo della variabile è consigliabile utilizzare unknow e mettere un guardian per evitare possibili errori a runtime.
  se ad esempio mettessimo any su una variabile su cui poi andiamo a richiamare la funzione toUpperCase e se a runtime ci arrivasse un numero, avremmo un errore non gestito. Il number non ha la funzione toUpperCase().
  
  ```typescript
  function log(val: any) {
    // ERRORE se arriva un qualcosa che non è di tipo string
    console.log(val.toUpperCase());
  }
  ```
  
  per gestire questo possibile errore potremmo mettere val come unknown e fare dei controlli con delle guardie. Senza questi controlli o se non si specifica il tipo, la compilazione va in errore.
  
  ```typescript
  type Some = {
    something: () => void;
  };

  function log(val: unknown) {
    if (typeof val === 'string') {
      console.log(val.toUpperCase());
    }

    console.log((val as number) + 20);
    console.log((val as Some).something());
  }

  log({
     something: () => { 
       console.log() 
    }
  });
  ```
  
  
