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

