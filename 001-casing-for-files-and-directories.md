# Naming convention for files and directories

## Context

Discuss what casing to use in regarding the file / directory and component names

## Decision

Use kebab-case for app/lib names, camelCase for anything we define. Exceptions are made if the tool we use is opinionated about the casing. For example:

- Camel case for file / directory names, and pascal case for component names
- Pascal case for both file / directory names, and component names

Example:

### Camel case for file / directory names, and pascal case for component names

Use camelCase for file / directory name and PascalCase for component name:

```
src/
 |__ components
   |__ Button
     |__ index.js -> Button (Component Name)
 |__ api
   |__ index.js
   |__ user.js (api file)
 |__ reducer
   |__ index.js
   |__ user.js (user-reducer file)
 |__ utils
   |__ index.js
   |__ cookies
     |__ index.js (cookies file)
 |__ pages/view
   |__ user
     |__ userList
       |__ index.js -> UserList (Component Name)
     |__ userDetails
       |__ UserDetail.js -> UserDetail (Component Name)
   |__ product
     |__ productList
       |__ ProductDataList.js -> ProductList (Component Name)
     |__ productDetails
       |__ ProductDetail.js -> ProductDetail (Component Name)
```

### Pascal case for both file / directory names, and component names

Use PascalCase for both file / directory name and component names also. PascalCase used as Component-file name and PascalCase used for directory-name when define the basic / common components in directory.

```
src/
 |__ components
   |__ Button
     |__ index.js -> Button (Component Name)
   |__ Inputs
     |__ TextInput.js -> TextInput (Component Name)
     |__ Select.js -> SelectBox (Component Name)
```

## Consequences

Consistency with file/directory names and component names.
