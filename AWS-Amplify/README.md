# AWS-Amplify-Masterclass
Fullstack App development using AWS Amplify

### Prequisites

```
Node.js v14.x or later : https://nodejs.org/en
npm v6.14.4 or later : https://www.npmjs.com/
git v2.14.1 or later : https://git-scm.com/

AWS Account : https://aws.amazon.com/

Amplify Cli : https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

```



#### Configure Amplify

```
amplify configure
```

#### Setup Reactjs project

```
npx create-react-app react-amplified

cd react-amplified

npm start
```

#### Initialize Amplify project

```
amplify init
```

#### Add API Backend 


```
amplify add api

amplify push
```

```
amplify status

amplify console api

amplify mock api
```

Try running a couple of mutations locally and then querying for the todos:

```
mutation createTodo {
  createTodo(input: {
    name: "Build an API"
    description: "Build a serverless API with Amplify and GraphQL"
  }) {
    id
    name
    description
  }
}

query listTodos {
  listTodos {
    items {
      id
      description
      name
    }
  }
}

```

#### Install Amplify packages

```
npm install aws-amplify
```
Open src/index.js and add the following code below the last import:

```
import { Amplify } from 'aws-amplify';
import awsExports from './aws-exports';
Amplify.configure(awsExports);
```

#### Frontend Integration

`src/App.js` and replace it with the following code:

```
/* src/App.js */
import React, { useEffect, useState } from 'react'
import { Amplify, API, graphqlOperation } from 'aws-amplify'
import { createTodo } from './graphql/mutations'
import { listTodos } from './graphql/queries'

import awsExports from "./aws-exports";
Amplify.configure(awsExports);

const initialState = { name: '', description: '' }

const App = () => {
  const [formState, setFormState] = useState(initialState)
  const [todos, setTodos] = useState([])

  useEffect(() => {
    fetchTodos()
  }, [])

  function setInput(key, value) {
    setFormState({ ...formState, [key]: value })
  }

  async function fetchTodos() {
    try {
      const todoData = await API.graphql(graphqlOperation(listTodos))
      const todos = todoData.data.listTodos.items
      setTodos(todos)
    } catch (err) { console.log('error fetching todos') }
  }

  async function addTodo() {
    try {
      if (!formState.name || !formState.description) return
      const todo = { ...formState }
      setTodos([...todos, todo])
      setFormState(initialState)
      await API.graphql(graphqlOperation(createTodo, {input: todo}))
    } catch (err) {
      console.log('error creating todo:', err)
    }
  }

  return (
    <div style={styles.container}>
      <h2>Amplify Todos</h2>
      <input
        onChange={event => setInput('name', event.target.value)}
        style={styles.input}
        value={formState.name}
        placeholder="Name"
      />
      <input
        onChange={event => setInput('description', event.target.value)}
        style={styles.input}
        value={formState.description}
        placeholder="Description"
      />
      <button style={styles.button} onClick={addTodo}>Create Todo</button>
      {
        todos.map((todo, index) => (
          <div key={todo.id ? todo.id : index} style={styles.todo}>
            <p style={styles.todoName}>{todo.name}</p>
            <p style={styles.todoDescription}>{todo.description}</p>
          </div>
        ))
      }
    </div>
  )
}

const styles = {
  container: { width: 400, margin: '0 auto', display: 'flex', flexDirection: 'column', justifyContent: 'center', padding: 20 },
  todo: {  marginBottom: 15 },
  input: { border: 'none', backgroundColor: '#ddd', marginBottom: 10, padding: 8, fontSize: 18 },
  todoName: { fontSize: 20, fontWeight: 'bold' },
  todoDescription: { marginBottom: 0 },
  button: { backgroundColor: 'black', color: 'white', outline: 'none', fontSize: 18, padding: '12px 0px' }
}

export default App
```

#### Run the application

```
npm start

```

#### Add Authentication module

```
amplify add auth

amplify push

```

#### Configure login UI

```
npm install @aws-amplify/ui-react

```

Open src/App.js and make the following changes:

```
import { withAuthenticator, Button, Heading } from '@aws-amplify/ui-react';
import '@aws-amplify/ui-react/styles.css';

```

```
/* src/App.js */
function App({ signOut, user }) { 
  // ... 
}


// ...
return (
  <div style={styles.container}>
    <Heading level={1}>Hello {user.username}</Heading>
    <Button onClick={signOut}>Sign out</Button>
    <h2>Amplify Todos</h2>
//...

export default withAuthenticator(App);

```

```
npm start

```

#### Deploy and Host the app

```
amplify add hosting
```

```
Select the plugin module to execute: Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)
Choose a type: Manual Deployment

```

```
amplify publish
```
