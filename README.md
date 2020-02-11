# Mirage JS Starter Kit

[From Mirage website](https://miragejs.com/):

> Mirage JS is an API mocking library that lets you build, test and share a complete working JavaScript application without having to rely on any backend services.

Their documentation is straight to the point but it only helps you setting up a simple server without any suggestion of folder organization. This starter kit keeps things separate into their own folders, introducing separation of concerns and making it easier to reason about all the parts.

---

## How to use it

### 1. Having started a React or Vue.js project, copy all the files to the src folder:

```
cd src && npx degit vedovelli/miragejs-starter-kit miragejs
```

[What is **degit**?](https://github.com/Rich-Harris/degit#readme)

This will create the `miragejs` folder inside `src`. You can use any folder name you find best.

**IMPORTANT**: do NOT omit the folder name in the degit command otherwise all starter kit's folders will be created inside your src folder, messing up your project organization.

### 2. Make sure all dependencies are installed:

```
npm install --save-dev miragejs faker
```

### 3. Make your project aware of Mirage JS:

**React**

```
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

if (process.env.NODE_ENV === "development") {
  // You can't use import in a conditional so we're using require() so no
  // Mirage JS code will ever reach your production build.
  require('./miragejs/server').makeServer();
}

ReactDOM.render(<App />, document.getElementById("root"));
```

**Vue.js**

```
import Vue from "vue";
import App from "./App.vue";
import router from "./router";
import store from "./store";

if (process.env.NODE_ENV === "development") {
  // You can't use import in a conditional so we're using require() so no
  // Mirage JS code will ever reach your production build.
  require('./miragejs/server').makeServer();
}

Vue.config.productionTip = false;

new Vue({
  router,
  store,
  render: h => h(App)
}).$mount("#app");
```

### 4. Calling the API

Inside any component of your application and using your favorite HTTP request's library make a call to `api/users`. You will receive back a list of 10 objects with the following shape:

```
{id: "1", name: "Some name", mobile: "+1 555 525636"}
```

Additionally if you call `api/products` you'll receive back a list of 3 objects with the following shape:

```
{
  id: "1",
  name: "Javascript coffee mug",
  description: "We are nothing without coffee",
  price: 3.5
},
```

Those routes operate with a `resource` meaning they accept all HTTP verbs involved in a CRUD operation.

### 5. Adding your own content

Lastly tweak `factories`, `fixtures` and `seeds` to accommodate your own needs.

---

## Folder structure

- `factories`: contains the blueprints for the content to be generated by mirage. It uses [faker](https://github.com/Marak/Faker.js#readme) to generate random but credible content;
- `fixtures`: contains predefined data to be served by Mirage. Use it if you have content to be served from JSON files;
- `models`: contains all models for the database entities. Every time you create a new resource or a new fixture, it is necessary to create a new model;
- `routes`: contains the routes for your API;
- `seeds`: contains the seeds for the data. They determine how many records should be generated and stored in the database. For that purpose they use the Factories.

## Example projects

To help you see it in action there are 2 example projects. For each one of them all instructions above were followed and the data is displayed in the interface.

**React**: [https://github.com/vedovelli/miragejs-starter-kit-react-example](https://github.com/vedovelli/miragejs-starter-kit-react-example)

**Vue.js**: [https://github.com/vedovelli/miragejs-starter-kit-vuejs-example](https://github.com/vedovelli/miragejs-starter-kit-vuejs-example)
