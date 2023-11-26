# How to organize the directory structure

## Context

Discuss the folder structure of this vite-react app.

**Best project architecture** doesn't follow any particular project structure, and the positive thing about this is that it allows us to make up a structure to suit our needs. The discussion here is simply an opinionated way to structure a project. You can utilize some parts or all of them for your project.

### The folder structure looks like this:

- Assets Folder
- Layouts Folder
- Components Folder
- Contexts Folder
- Config Folder
- Pages/View Folder
- Middleware Folder
- Routes Folder
- Services Folders
- Utils Folder

We follow the folder structure like this:

```
project-name/
    |__ public/
    |__ src/
        |__ actions/
        |__ api/
        |__ assets/
            |__ scss/
            |__ images/
        |__ common/ (style related common files)
        |__ components/
        |__ contexts/
        |__ layouts/
            |__ PageMainSection/
        |__ routes/
            privateRoute.js
        |__ pages/
            |__ login/
                index.js
            |__ user/
                |__ userList/
                |__ userDetails/
            |__ product/
                |__ productList/
                |__ productDetails/
        |__ reducers/
        |__ sagas/
        |__ services/
        |__ utils/
            |__ api/
            |__ cookies/
            |__ store/
            constant.js
        App.jsx
        main.jsx (#or index.jsx)
    .env
    .gitignore
    index.html
    jsconfig.json
    package.json
    vite.config.js
    ...(other setup files)
```

### Description for folders

**Assets Folder**:

As the name says, it contains assets of our project. It consists of images and styling files. Here we can store our global styles. We are centralizing the project so we can store the page-based or component-based styles over here. But we can even keep style according to the pages folder or component folder also. But that depends on developer comfortability.

**Layouts Folder**:

As the name says, it contains layouts available to the whole project like main page-view section which is common for more than 1-2 pages etc. We can store the common layout page-view section here and call it.

**Components Folder**:

Components are the building blocks of any react project. This folder consists of a collection of UI components like buttons, modals, inputs, loader, header, footer, etc., that can be used across various files in the project. Each component should consist of a test file to do a unit test as it will be widely used in the project.

**Contexts Folder**:

As the name says, it contains all contexts of the whole project. Context provides a way to share values like these between components without having to explicitly pass a prop through every level of the tree. We can create the context-providers like auth-context, route-context, product-context etc,.

**Config Folder**:

This folder consists of a configuration file where we store environment variables in config.js. We will use this file to set up multi-environment configurations in your application.

**Pages Folder**:

The files in the pages folder indicate the route of the react application. Each file in this folder contains its route. A page can contain its subfolder. Each page has its state and is usually used to call an async operation. It usually consists of various components grouped.

**Middleware Folder**:

This folder consists of middleware that allows for side effects in the application. It is used when we are using redux with it. Here we keep all our custom middleware.

**Routes Folder**:

This folder consists of all routes of the application. It consists of private, protected, and all types of routes. Here we can even call our sub-route.

**Services Folder**:

All the folders related to redux in your project. Inside it, there are 3 folders named actions, reducers, and saga manage states. The actions and reducers will be called in almost all the pages, so create actions, reducers & sagas according to pages name.

**Utils Folder**:

Utils folder consists of some repeatedly used functions that are commonly used in the project. It should contain only common js functions & objects like dropdown options, regex condition/store, data formatting, etc.

## Consequences

Consistency in project folder structure for whole app.
