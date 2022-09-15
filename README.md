# student-list-app
React MERN stack CRUD app

After getting set up and adding all of the code 

"Compiled with problems:X

ERROR in ./src/App.js 100:45-51

export 'Switch' (imported as 'Switch') was not found in 'react-router-dom' (possible exports: BrowserRouter, HashRouter, Link, MemoryRouter, NavLink, Navigate, NavigationType, Outlet, Route, Router, Routes, UNSAFE_LocationContext, UNSAFE_NavigationContext, UNSAFE_RouteContext, createPath, createRoutesFromChildren, createSearchParams, generatePath, matchPath, matchRoutes, parsePath, renderMatches, resolvePath, unstable_HistoryRouter, useHref, useInRouterContext, useLinkClickHandler, useLocation, useMatch, useNavigate, useNavigationType, useOutlet, useOutletContext, useParams, useResolvedPath, useRoutes, useSearchParams)"

Replaced 'Switch' with 'Routes' due to changes in react-router-dom v6 (from v5).

Compiled successfully! 

Browser displays the header Navbar but will Not display the form fields in the main content Container.

Console Warning: Matched leaf route at location "/create-student" does not have an element. This means it will render an <Outlet /> with a null value by default resulting in an "empty" page.

app.js = Updated each Route "component" to be "element" for react-router-dom v6.

ERROR: Warning: Functions are not valid as a React child. This may happen if you return a Component instead of <Component /> from render. Or maybe you meant to call this function rather than return it.

app.js = Forgot to update each Route element to return a Component like element={<CreateStudent />}

StudentForm = Added <label htmlFor="Name">Name</label> for each of the 3 form fields.
            = Removed FormControl from 'import { FormGroup, Button } from "react-bootstrap";' because it was never used. Which caused an esLint warning.

Terminal:
[nodemon] starting `node server.js`
/Users/robertgeorge2/projects/student-list-app/backend/node_modules/mongoose/lib/index.js:225
    throw new Error(`\`${key}\` is an invalid option.`);
    ^
Error: `useNewUrlParser` is an invalid option.
    at Mongoose.set (/Users/robertgeorge2/projects/student-list-app/backend/node_modules/mongoose/lib/index.js:225:11)

    Mongoose documentation > Migrating from 5.x to to 6.x
        "No More Deprecation Warning Options
        useNewUrlParser, useUnifiedTopology, useFindAndModify, and useCreateIndex are no longer supported options. Mongoose 6 always behaves as if useNewUrlParser, useUnifiedTopology, and useCreateIndex are true, and useFindAndModify is false. Please remove these options from your code."
        https://mongoosejs.com/docs/migrating_to_6.html#no-more-deprecation-warning-options

server.js:11-14 = Removed/Hidden
// Configure mongoDB Database
// mongoose.set('useNewUrlParser', true);
// mongoose.set('useFindAndModify', false);
// mongoose.set('useCreateIndex', true);
// mongoose.set('useUnifiedTopology', true);

App loaded.
I was able to create a new student.
I was able to view the Student List.
When I clicked the Edit button next to the most recently added Student I was taken to the edit-student page but it was blank. The CONSOLE listed an ERROR.
Uncaught TypeError: Cannot read properties of undefined (reading 'params')
    at edit-student.component.js:35:1
    at commitHookEffectListMount (react-dom.development.js:23150:1)

    edit-student.component.js
    Refactoring required due to changes in React Router v6 related to React Hooks in React v16.8
    See react-router/docs Upgrading from v5 = https://github.com/remix-run/react-router/blob/main/docs/upgrading/v5.md#advantages-of-route-element
    - useParams instead of passing (props)
    - Routes and Links are now relative
      - don't need match.url or match.path
    - useNavigate instead of useHistory

    Replaced "props.match.params.id" with "_id"
    Replaced route redirects like "props.history.push("/student-list")" with "navigate("/student-list")"
