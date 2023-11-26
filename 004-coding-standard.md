# Coding Standard

## Context

Discuss the rules regarding the coding standard for react app.

## Decision

The best coding practices and standards for react development. These are not hard and fast rules but common practices to write clean and consistent code. Most of them hold good for all frontend frameworks and not really specific to React.

Here are some coding practices which needs to follow in react project:

1.  Naming Conventions: 
    Document naming conventions for variables, functions, components, and files. This helps maintain a consistent and predictable structure in codebase.
   - React UI component’s names should be PascalCase.
    ```
    Example: LoginScreen.js
    ```

   - All other helper files should be camelCase. (non-component files)
    ```
    Example: commonUtils.js
    ```

   - All the folder names should be camelCase.
    ```
    Example: 
       components/
       api/
       utils/
    ```
    > Note: Check the [Naming convention](docs/architecture/decisions/001-casing-for-files-and-directories.mdr-files-and-directories.md) documentation for more details.

2.  Code Comments:
    Encourage developers to add comments explaining complex or non-obvious code sections. Include guidelines for writing meaningful comments in your coding standards documentation.


3.  Error Handling and Logging:
    Document how errors should be handled and logged in the application. Include guidance on error messages and how to report errors to a central system if applicable.
    > Note: Check the [Handle FE errors](docs/architecture/decisions/003-handle-error.mdisions/003-handle-error.md) documentation for more details.


4.  Folder Structure:
    Define a recommended project folder structure that makes it easy for developers to find and organize their code. Include examples and explanations in your documentation.

    > Note: Check the [How to organize the directory structure](docs/architecture/decisions/004-organize-the-directory-structure.mdthe-directory-structure.md) documentation for more details.

5.  Linting and Formatting:
    Integrate a linter and code formatter into the project to enforce the coding standards automatically. Popular tools for this in the React ecosystem include ESLint and Prettier.


6.  CSS files should be named the same as the component PascalCase. Global CSS which applies to all components should be placed in common-style folder and should be named in camelCase.

    ```
    Example:
        Card.css(for components),
        global.css(for global styles)
    ```

    > Note: _Avoid to add CSS file for styling. It is only used to override the styles for components of third-party library. Must use tailwind classes for styling._ Check the [Tailwind Standard](docs/architecture/decisions/002-tailwind-standards.md/002-tailwind-standards.md) documentation for more details.

7.  Test files should be named the same as the component or non-component file.
    ```
     Example:
        LoginScreen.test.js
        commonUtils.test.js
    ```
    > Note: Test cases are depend on project requirements. Not need to add compulsory.

### Some common basic rules to be kept in mind to write clean code:

1. Create multiple files instead of writing a big file. (Componentization of code: fix to small functionality for each file)
2. Place all your CSS files in one common folder if exists also avoid Inline CSS. (**Best practice is use Tailwind classes for css.**)
3. Use a linter to make your code easier to review. Follow strict linting rules. This in turn helps you write clean, consistent code.
4. Remove all the console.log. Keep the log statement if it is needed like show any promise errors.
5. Review your code before commit it.
6. Create many utility files that can help you remove duplicate code from multiple files.
7. Name your files logically according to the job that they perform.

   ```jsx
   // Example (file-name)
   Login.jsx

   // Code
   const Login = () => {
     // here write functions related to login

     return (
       <div>
         <h1>Login Form</h1>
         {/* Rest UI code for login form */}
       </div>
     );
   };
   ```

8. Use comments for every logical functions. Clean code is self-commenting(using the right variable names and function names).

   ```jsx
   /**
    * Use: Remove classes from base-styles
    * @param baseStylesArr: String[]. Default classes of tailwind in array of string format, like: ['p-1', 'm-1', 'w-full']
    * @param removeStylesArr: String[]. Classes of tailwind which you want to remove from default-classes. It is also in array of string format same as above baseStylesArr
    * @return: String[]. Filtered array of class-string.
    */
   export const removeCssClasses = (baseStylesArr, removeStylesArr) => {
     return baseStylesArr.filter((item) => !includes(removeStylesArr, item));
   };
   ```

9. Destructuring your props is a good way to help make your coder cleaner and more maintainable.
   ```jsx
   // Example
   const UserDetails = (props) => {
     const { id, userData, ...restProps } = props;
   };
   ```
   
10. Putting imports in an order
    - React import
    - Library imports (Alphabetical order)
    - Absolute imports from the project (Alphabetical order)
    - Import \* as
    - Import './[some file].[some extension]'

    Each kind should be separated by an empty line. This makes your imports clean and easy to understand for all the components, 3rd-party libraries, and etc.


11. Import particular methods/functions from lodash lib, don’t import whole methods.

    ```jsx
    /* import only required methods excepts import whole lib */

    // Use
    import { get, map, filter, isEmpty } from 'lodash';

    // Don't use
    import * as _ from 'lodash';
    ```

12. Use `material-icons` for all icons. (You can use MUI icons as components using `@mui/icons-material` lib in some cases if icon is not found / proper in google-material-icons list)

    Refer link for icon: [Google Material Icons](https://fonts.google.com/icons?icon.set=Material+Icons)

    Example:
    ```jsx
    // For serch icon
    <span class="material-icons-round">search</span>
    ```

13. Create common formik input components like `FormikTextInput`, `FormikPasswordInput` etc. and use it in Formik-form.
14. Cover success and failure test-case for all the logical functions, api response etc.,
15. Check the code and test positive and negative test-case for the code and then commit the code and create the PR. If you have any doubts or any test-case is remaining for the task then mention it in channel with details.
16. Create common module functions so we can use that everytime. Also it is easy to refactor that module function if require any lib changes.
   
    Example:
    ```jsx
    // common module function
    const useNavigateHook = () => {
       const navigate = useNavigate();

       const navigateTo = (routePath) => {
          navigate(routePath);
       }

       return { navigateTo };
    };

    // use module in component
    const MyComponent = () => {
      const { navigateTo } = useNavigateHook;

      const handleClick = () => {
        navigateTo('/home');
      };

      return (
         <div>
            My Component
            {/* ... */}
        
            <Button onClick={handleClick}>Go To Home</Button>
         </div>
      ) 
    };
    ```
17. Use `Enum`:

    `Enum Definition`: Enum (short for enumeration) is a data type in programming that consists of a set of named values, which represent distinct elements within a specific category or domain. Enums make your code more readable and maintainable by giving meaningful names to otherwise arbitrary values. 
    
    Example:
    ```jsx
    const DaysOfWeek = {
       MONDAY: 'Monday',
       TUESDAY: 'Tuesday',
       WEDNESDAY: 'Wednesday',
       THURSDAY: 'Thursday',
       FRIDAY: 'Friday',
       SATURDAY: 'Saturday',
       SUNDAY: 'Sunday',
    };
    ```
    `Enum Usage`: Enums are used to represent a finite set of related values or options within your code. You can use enums in various ways, such as in conditional statements, function parameters, and data structures, to make your code more self-explanatory and to reduce the risk of errors.
    
    `Maintainability`: When you need to add or modify values in a set of related constants, enums make it easier to make changes in one place, rather than searching for and updating every occurrence of a particular value throughout your codebase.

    Example: Usage of Enum
    ```jsx
     // Conditional Statements:
     const day = DaysOfWeek.MONDAY;
      
      if (day === DaysOfWeek.SATURDAY || day === DaysOfWeek.SUNDAY) {
      console.log('It\'s the weekend!');
      } else {
      console.log('It\'s a weekday.');
      } ;
    
     // Function Parameters:
      function setDayOfWeek(day) {
       // Perform actions based on the provided day (an enum value)
      }

      setDayOfWeek(DaysOfWeek.WEDNESDAY);
    
    // Data Structures:
     const weeklyTasks = {
         [DaysOfWeek.MONDAY]: 'Meeting',
         [DaysOfWeek.WEDNESDAY]: 'Report',
         [DaysOfWeek.FRIDAY]: 'Presentation',
         };
     console.log(weeklyTasks[DaysOfWeek.WEDNESDAY]);
    ```

### Some rules related to React Hooks:

- First declare all the props
- Second declare all the default hooks like navigate, dispatch, location, history and other …
- Third declare all the redux-states which is declared by useSelectors
- Forth declare all the component states which is declared by useState
- Fifth declare all the useEffects and if useEffect includes any functions then declare that function and then add useEffect under that function.
- Use useCallback() function for dispatch any actions

Example:

```jsx
const UserDetail = (props) => {
  // props
  const { id, onEdit, onClose } = props;

  // default hooks
  const dispatch = useDispatch();
  const navigate = useNavigate();

  // redux-state
  const userDetails = useSelector((state) => state.user.userDetail);

  // component-state
  const [showMore, setShowMore] = useState(false);

  // useEffect
  useEffect(() => {
    setShowMore(false);
  }, []);

  // useCallback function for disaptch the action
  const getUserDetails = useCallback(
    (id) => {
      dispatch(getUserDataById({ id }));
    },
    [dispatch],
  );

  useEffect(() => {
    getUserDetails(id);
  }, []);

  // normal function
  const handleClick = () => {
    navigate('/home');
  };

  return <div>{/* rest code for UI of User-detail */}</div>;
};
```

### Some rules related to CSS/style for clean code:

1. Use `rem` for style instead of `px` . (PX is used when u give the small size like 1 or 2 px like border-width. For font-size and line-height and other css styles use rem.)
2. Use flex-box and grid concepts excepts give manually margin and padding (margin-left, margin-right for arrange the UI in proper way.)

   Refer this for flex-box and grid style:

   - [https://tailwindcss.com/docs/flex](https://tailwindcss.com/docs/flex)
   - [https://tailwindcss.com/docs/grid-template-columns](https://tailwindcss.com/docs/grid-template-columns)

3. For the responsive design, you have to use a Grid row column Instead of a fixed height width.
4. CSS class names should use a standard naming convention (personally use kebab-case because it's used by most of the CSS framework classes) or any standard practice. Document with several conventions: [CSS naming conventions](https://www.freecodecamp.org/news/css-naming-conventions-that-will-save-you-hours-of-debugging-35cea737d849/).
