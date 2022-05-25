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

## Required

  Rende tutti gli attributi di un'interfaccia obbligatori

## Pick
  
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
  
## Omit
  
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
  
