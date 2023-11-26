# Handle FE errors

## Description

Focusing on error handling on the front end (Vite-React App). Approach to error handling on a backend web server may be different.

On the front end, there are a couple tools for exception handling. The most well known is the **ErrorBoundary** pattern, which can catch uncaught runtime exceptions in a React sub-tree. It can be configured to render a fallback UI in this case.

There are many ways to handle the errors:

1. Use an ErrorBoundary to catch top level synchronous runtime exceptions
2. Keep using try/catch to wrap async code like network calls. Rely on this for most network requests where the type of exception doesn't matter
3. For known errors that the client is expected to handle it, such as validation errors where the server may return an error code that impacts the UI, use a Result data type for strong type handling

Handling errors in a Vite-React application is crucial to ensure a smooth user experience and make debugging easier. Here are some best practices for error handling in React:

## Use an ErrorBoundary

We are used the ErrorBoundary for handle the FE errors. NPM package is provide the lib **react-error-boundary** for handle the FE errors with render a fallback UI.

### Getting started

```
npm install react-error-boundary
# or
yarn add react-error-boundary
```

### API

**ErrorBoundary** component:

Wrap an ErrorBoundary around other React components to "catch" errors and render a fallback UI.

```jsx
const GenericFallback = (props) => {
  const { error, ...resetErrorBoundary } = props;
  // Call resetErrorBoundary() to reset the error boundary and retry the render.

  return (
    <div>
      <h1 className="text-2xl m-3 text-gray-500">Oops, something went wrong!</h1>
      <p className="text-base text-gray-600">{error.message}</p>
    </div>
  );
};

const ErrorBoundaryProvider = ({ children }) => {
  
  const onErrorLog = (error, info) => {
    // Do something with the error, e.g. log to an external API
    // Set/Report the error
  };

  const onReset = (details) => {
    // Reset the state of your app so the error doesn't happen again
  };

  return (
    <ErrorBoundary onError={onErrorLog} onReset={onReset} FallbackComponent={GenericFallback}>
      {children}
    </ErrorBoundary>
  );
};

// Wrap components with the Error Boundary
<ErrorBoundaryProvider>
   {/* Your components */}
</ErrorBoundaryProvider>;
```

> Note: Error boundaries only catch errors in the components below them in the tree.

## Use try/catch

Handle Network Request Errors:

For network calls, usually an useEffect hook is used some async method, wrapped in a try/catch. If it fails, set the state to error, which can then be rendered. This works well for most cases where the error messaging is generic. Handling specific errors is more difficult because the developer needs to cast the error object to a specific one prior to handling that exception. Something like `if (e instanceof MySpecificError) {...}` . This suffers from issues such as 1) lack of type safety, and 2) coupling to implementation details of called functions. If someone were to refactor an underlying function to throw a different exception, things would break at runtime because of this coupling. Also without type safety, there's no indication to the developer that they should be handling a specific type of error.

Example:

```js
const main = async () => {
  try {
    const user = await fetchUser();
    const postResult = await createPost({
      userId: user.id,
      name: BAD_POST_NAME,
    });
  } catch (error) {
    console.log('Error: ', error);
  }
};

main();
```

Walking through a couple failure cases:

- If `fetchUser` fails, a generic error is shown
- If `createPost` fails, a generic error is shown

Other scenarios which are usefull for handle the FE errors:

1. **Error Logging**:
   Consider implementing error logging to keep track of errors that occur in your application. Services like Sentry or LogRocket can help you monitor and debug errors in production.


2. **User-Friendly Error Messages**:
   Display user-friendly error messages when something goes wrong. Avoid exposing technical details to users, but make sure to log those details for debugging purposes.

## Consequences

More consistent error handling that is both practical and type safe.
