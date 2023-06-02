---
theme: penguin
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Introduction to GraphQL
  Gamify Loyalty
drawings:
  persist: false
transition: slide-left
title: Introduction to GraphQL
colorSchema: dark
layout: intro
---

# Introduction to GraphQL 

Gamify Loyalty

<div class="flex justify-center">
  <img src="/logo.png" class="w-60 h-16 mt-8 shadow" />
</div>

<!--
En esta sesión, exploraremos qué es GraphQL, sus ventajas y cómo se compara con las API tradicionales.
-->

---
layout: text-image
media: /GraphQLLogo.png
---

# What is GraphQL?

- GraphQL: Query language for APIs

- Developed by Facebook in 2012

- Flexible way to fetch data

<!--
¿Qué es GraphQL?

GraphQL es un lenguaje de consulta y manipulación de datos para APIs.

Fue desarrollado por Facebook en 2012 y se hizo público en 2015.

Proporciona a los clientes una forma flexible de obtener solo los datos que necesitan y en la estructura deseada.
-->

---
layout: text-image
media: https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExZGRlMDBjMzI1MGYwM2QzYmMxZGQwNDU4NzNkNWMxNjliZWJiOWVhMyZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/Mab1lyzb70X0YiNLUj/giphy.gif
---

# How does GraphQL work?

- Single entry point 
  - /graphql
- Clients send queries
  - POST
- Server responds with requested data
  - JSON

<!--
¿Cómo funciona GraphQL?

En lugar de múltiples endpoints como en las APIs tradicionales, GraphQL tiene un solo punto de entrada.

Los clientes envían consultas al servidor GraphQL para especificar exactamente los datos que necesitan.

El servidor responde con los datos solicitados, generalmente en formato JSON.
-->

---
transition: slide-up
level: 1
layout: text-image
media: https://media1.giphy.com/media/pzmbXFDiRbEEk1vCtP/giphy.gif?cid=ecf05e475yzc529c9p8qvi3wihlxjik0ebclt47maord1w12&ep=v1_gifs_search&rid=giphy.gif&ct=g
---

# SDL

- GraphQL uses a Schema Definition Language
  - SDL
- SDL is a human-readable syntax for describing the GraphQL schema.

<!--
SDL (Lenguaje de Definición de Esquemas)

GraphQL utiliza un Lenguaje de Definición de Esquemas (SDL) para definir la estructura y capacidades de la API.
SDL es una sintaxis legible por humanos para describir el esquema de GraphQL.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Types in SDL

- Scalar Types
- Object Types
- Enum Types

::right::

```graphql {all|2|3|6|all}
type User {
  id: ID!
  name: String!
  age: Int
  email: String!
  role: UserRole!
}

enum UserRole {
  ADMIN
  USER
  GUEST
}
```

<!--
Definición de Tipos en SDL

Tipos Escalares: Representan tipos de datos primitivos como String, Int, Boolean, etc.

Tipos de Objeto: Definen la estructura de los datos devueltos por la API. Consisten en campos y sus tipos de retorno.

Tipos Enum: Definen un conjunto de valores posibles para un campo.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Fields in SDL

- Fields represent the properties or data that can be requested in a query.
- Each field has a name and a type.

::right::

```graphql {all|2|3|all}
type User {
  id: ID!
  name: String!
  age: Int
  email: String!
  role: UserRole!
}
```

<!--
Definición de Campos en SDL

- Los campos representan las propiedades o datos que se pueden solicitar en una consulta.
- Cada campo tiene un nombre y un tipo.
-->

---
layout: two-cols
level: 2
---

# Relationships in SDL

- GraphQL allows defining relationships between types.
- Relationships are represented using fields that reference other types.

::right::

```graphql {all|12|5|all}
type User {
  id: ID!
  name: String!
  email: String!
  posts: [Post!]!
}

type Post {
  id: ID!
  title: String!
  content: String!
  author: User!
}
```

<!--
Definición de Relaciones en SDL

GraphQL permite definir relaciones entre tipos.

Las relaciones se representan utilizando campos que hacen referencia a otros tipos.
-->

---
transition: slide-up
level: 1
layout: text-image
media: https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExNTY4ZjRhNjkxYzMzNjY1ZGQwNTg5MTYwMDU2M2QxMWIyZjY0M2JjOSZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/JIX9t2j0ZTN9S/giphy.gif
---

# GraphQL Operations

- Query  
  - Fetches data from the server

- Mutation  
  - Modifies data on the server

- Subscription  
  - Receives real-time updates from the server

<!--
Operaciones en GraphQL

- Query (Consulta): Se utiliza para obtener datos del servidor. Es similar a una petición GET en REST.

- Mutation (Mutación): Se utiliza para modificar datos en el servidor. Es similar a una petición POST, PUT o DELETE en REST.

- Subscription (Suscripción): Se utiliza para recibir actualizaciones en tiempo real desde el servidor.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Query

- Clients send queries to the server, specifying the desired fields.
- The server resolves the query against the schema and retrieves the requested data.
- The server responds with the requested data in JSON format.

::right::

```graphql {all|2|3|4-6|5|7-9|8|all}
query {
	User(id: '55') {
		name
		posts {
			title
		}
		followers(last: 2) {
			name
		}
	}
}
```

```json {all}
{
	"data": {
		"User": {
			"name": "Mary",
			"posts": [
				{ "title": "This is the title" }
			],
			"followers": [
				{ "name": "John" },
				{ "name": "Alice" },
			]
		}
	}
}
```

<!--
Ejecución de Query en GraphQL

Los clientes envían queries al servidor, especificando los campos deseados y las variables necesarias.

El servidor recibe la query, la resuelve contra el esquema definido y obtiene los datos solicitados.

El servidor responde con los datos solicitados, generalmente en formato JSON, coincidiendo con la estructura de la query.
-->

---
transition: slide-up
layout: two-cols
level: 2
---

# Mutation

- Clients send mutations to the server to modify data.
- The server validates and performs the requested modifications.
- The server responds with the updated data.

::right::

```graphql {all|1|2-4|2|3|all}
mutation {
	createUser(name: "Mark", age: 22) {
		id
	}
}
```

<!--
Ejecución de Mutation en GraphQL

Los clientes envían mutations al servidor para modificar datos.

El servidor recibe la mutación, la valida según el esquema definido y realiza las modificaciones solicitadas.

El servidor responde con los datos actualizados, permitiendo a los clientes verificar los cambios.
-->

---
layout: two-cols
level: 2
---

# Subscription

- Clients subscribe to specific events or data changes.
- The server establishes a persistent connection and sends real-time updates.
- Clients receive updates whenever the subscribed events occur or data changes.

::right::

```graphql {all|1|2-5|3-4|8-13|all}
subscription {
	newUser {
		name
		age
	}
}
```

```graphql {all|2-5|all}
{
	"newUser": {
		"name": "John",
		"age": 22
	}
}
```

<!--
Ejecución de Subscription en GraphQL

Los clientes se suscriben a eventos específicos o cambios de datos.

El servidor establece una conexión persistente con el cliente y le notifica cuando ocurren los eventos suscritos o hay cambios en los datos.

El servidor envía actualizaciones en tiempo real al cliente, manteniéndolo informado sobre los cambios que ocurren en el servidor.
-->

---
layout: text-image
media: https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzNjNDY3ZjFiNzQxMDRmYmViMTljYzljYzc5Mzc4MmI3ZmZmNTY0MyZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/Ot4U0KHw2fdvxJZ4jh/giphy.gif
---

# Advantages of GraphQL

- Efficiency: Fetch only needed data

- Flexibility: Structure data as desired

- Easy versioning

- Automatic documentation

<!--
Ventajas de GraphQL

Eficiencia: Los clientes pueden obtener exactamente los datos necesarios en una sola solicitud, evitando la sobrecarga de datos innecesarios.

Flexibilidad: Los clientes pueden especificar la estructura de los datos que desean, lo que permite una integración más fácil con las aplicaciones front-end.

Versionado sencillo: GraphQL facilita la evolución del esquema sin romper las implementaciones existentes.

Documentación automática: Con la ayuda de herramientas como GraphiQL, GraphQL puede generar automáticamente una documentación completa y precisa de la API.
-->

---
layout: text-image
media: https://media.tenor.com/GZtZgAQ0E4cAAAAd/excited-omg.gif
---

# Comparison with Traditional APIs

- Avoids overfetching

- Avoids underfetching

- Single entry point VS multiple:
  - /users/{id}
  - /users/{id}/posts
  - /users/{id}/followers

<!--
Comparación con las APIs tradicionales

Overfetching (sobrecarga): En las APIs tradicionales, los clientes a menudo reciben más datos de los necesarios. GraphQL evita esto al permitir a los clientes solicitar solo los campos requeridos.

Underfetching (subcarga): En las APIs tradicionales, los clientes pueden necesitar múltiples solicitudes para obtener todos los datos necesarios. GraphQL permite a los clientes obtener todos los datos en una sola solicitud.

Endpoints múltiples: Las APIs tradicionales pueden tener múltiples endpoints para diferentes recursos. GraphQL tiene un solo punto de entrada, lo que facilita la gestión y el descubrimiento de la API.
-->

---
layout: text-image
media: https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExMjc5YmUzYmYwOWY5ZjhmMDM1NjE2MmI1ZDY0YjMxZjdjYTg1NDhmMiZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/8vUEXZA2me7vnuUvrs/giphy.gif
---

# Disadvantages of Using GraphQL

- Learning curve

- Complex caching

- Query size control

- Lack of native support for all databases

- Migration from existing APIs

<!--
Desventajas de usar GraphQL

Mayor complejidad inicial: Curva de aprendizaje más pronunciada en comparación con las APIs tradicionales. Los desarrolladores deben familiarizarse con el lenguaje y entender cómo diseñar y estructurar el esquema de GraphQL correctamente.

Caché más compleja: Debido a la flexibilidad de las consultas en GraphQL, el almacenamiento en caché puede volverse más complejo. La caché se vuelve menos efectiva si las consultas son altamente personalizadas y cambian frecuentemente.

Necesidad de controlar el tamaño de las consultas: Si los clientes de GraphQL envían consultas complejas y anidadas, puede haber un riesgo de que las consultas se vuelvan ineficientes o demasiado grandes. Es importante establecer límites y controlar el tamaño de las consultas para garantizar un rendimiento óptimo.

Falta de soporte nativo para todas las bases de datos: GraphQL en sí mismo no proporciona una capa de almacenamiento de datos. Aunque se puede utilizar con varias bases de datos, algunas no tienen soporte nativo para GraphQL, lo que puede requerir la implementación de capas adicionales o adaptadores.

Migración desde APIs existentes: Si ya tienes una API existente, migrar a GraphQL puede requerir tiempo y esfuerzo significativos. Además, algunas funcionalidades de las APIs tradicionales, como la autenticación y la autorización, pueden requerir una implementación adicional en GraphQL.
-->

---
layout: text-image
media: https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExNmRmMmVlOTg0NzFhODUyNmY5MjNlMzgyNTliN2U0YTEyZDI0OTlhMSZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/3o7abKhOpu0NwenH3O/giphy.gif
---

# Conclusion

- GraphQL is efficient and flexible
- Allows clients to request only the data they need
- Robust ecosystem and community

<!--
GraphQL es un lenguaje de consulta y manipulación de datos para APIs.
Proporciona eficiencia y flexibilidad al permitir a los clientes obtener solo los datos necesarios y en la estructura deseada.

Se compara favorablemente con las APIs tradicionales al evitar el overfetching y el underfetching.

Cuenta con un ecosistema sólido y una comunidad activa.
-->

---
layout: new-section
---

# Demo

![Demo](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExYmI4ZWVlNTUyOTBiZmU0ZDlkNGIwZGRkNTc4NzI3M2VhNmZjOWQ4MSZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/d9O5lPyufbSfZzC1pq/giphy.gif)

---
layout: end
---

# QA

![QA](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExYzA2NjNmZmQ2NjdhNTdiMWRiYzcyOGMxMWM5OTZlMzFiNWE3YzZkOCZlcD12MV9pbnRlcm5hbF9naWZzX2dpZklkJmN0PWc/xT5LMB2WiOdjpB7K4o/giphy.gif)