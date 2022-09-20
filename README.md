# student-list-app = Refactoring a React MERN stack CRUD app from React v15 to v18.2

This **Refactoring** project came about because the React MERN stack CRUD app tutorial I was following was NOT working locally on my Mac. Eventually I figured out that despite the date *"Last Updated: 10 Apr, 2022"* the code was actually not updated to work with the current versions of *React* and *React Router*.  

Meaning, the ***npm install*** references were ***generic*** instead of including the specific version numbers for the app to work, without refactoring, when installed at a later date.  

After I updated the code for the app to work locally a developer friend reminded me that **Refactoring** old/inherited code is a common task that is worth highlighting as a junior project.  

## GeeksforGeeks: tutorial => [How to build a basic CRUD app with Node.js and ReactJS ?](https://www.geeksforgeeks.org/how-to-build-a-basic-crud-app-with-node-js-and-reactjs/)

### **Front End:** Refactoring started after the Front End code was set up from the tutorial  
1. 'Compiled with problems:X'  
  'ERROR in ./src/App.js 100:45-51  
  export 'Switch' (imported as 'Switch') was not found in 'react-router-dom' (possible exports: BrowserRouter, HashRouter, Link, MemoryRouter, NavLink, Navigate, NavigationType, Outlet, Route, Router, Routes, UNSAFE_LocationContext, UNSAFE_NavigationContext, UNSAFE_RouteContext, createPath, createRoutesFromChildren, createSearchParams, generatePath, matchPath, matchRoutes, parsePath, renderMatches, resolvePath, unstable_HistoryRouter, useHref, useInRouterContext, useLinkClickHandler, useLocation, useMatch, useNavigate, useNavigationType, useOutlet, useOutletContext, useParams, useResolvedPath, useRoutes, useSearchParams)'  
  
  - Replaced `Switch` with `Routes` due to changes in *react-router-dom v6* (from *v5*).  

2. Browser displays the header Navbar but will **Not** display the form fields in the main content Container area.  

  - Console "WARNING: Matched leaf route at location "/create-student" does not have an element. This means it will render an `<Outlet />` with a null value by default resulting in an "empty" page."  
  
    - app.js = Updated each Route `component` to be an `element` for *react-router-dom v6*.  

3. Console "Warning: Functions are not valid as a React child. This may happen if you return a Component instead of `<Component />` from render. Or maybe you meant to call this function rather than return it."  

  - app.js = Update each Route `element` to return a Component like `element={<CreateStudent />}`  
  
  - StudentForm.js
     - Added `<label htmlFor="Name">Name</label>` for each of the 3 form fields.  
     - Removed `FormControl` from `import { FormGroup, Button } from "react-bootstrap";` because it was never used and it caused an esLint Warning.  

### **Back end:** Refactoring continued after the Back End code was set up from the tutorial

1. Terminal:  
  [ nodemon ] starting `node server.js`  
  /Users/robertgeorge2/projects/student-list-app/backend/node_modules/mongoose/lib/index.js:225  
  `throw new Error(` `\${key}\ is an invalid option.` `);`  
  `^`  
  Error: `useNewUrlParser` is an invalid option.  
  at Mongoose.set (/Users/robertgeorge2/projects/student-list-app/backend/node_modules/mongoose/lib/index.js:225:11)  

  - Mongoose documentation => [Migrating from 5.x to to 6.x](https://mongoosejs.com/docs/migrating_to_6.html#no-more-deprecation-warning-options)  
        "No More Deprecation Warning Options  
        useNewUrlParser, useUnifiedTopology, useFindAndModify, and useCreateIndex are no longer supported options. Mongoose 6 always behaves as if useNewUrlParser, useUnifiedTopology, and useCreateIndex are true, and useFindAndModify is false. Please remove these options from your code."  

    - server.js:11-14 = Remove/Hide the following because they are Not needed
    // Configure mongoDB Database  
    // mongoose.set('useNewUrlParser', true);  
    // mongoose.set('useFindAndModify', false);  
    // mongoose.set('useCreateIndex', true);  
    // mongoose.set('useUnifiedTopology', true);  

**C** - I can Create a New student.  
**R** - I can Read the Student List.  

2. When I clicked the "Edit" button next to a student on the Student List page I was taken to the Edit Student page but it was blank?  

  The CONSOLE listed an ERROR.  
  "Uncaught TypeError: Cannot read properties of undefined (reading 'params') at edit-student.component.js:35:1"  
  - edit-student.component.js  
    Refactoring required due to changes in *React Router v6* related to **React Hooks** (added in *React v16.8*)  
    - React-Router Advantages of route element => [Upgrading from v5](https://github.com/remix-run/react-router/blob/main/docs/upgrading/v5.md#advantages-of-route-element)  
      - `useParams` instead of passing `(props)`  
      - `Routes` and `Links` are now relative  
          -- `match.url` or `match.path` = NOT neded  
      - `useNavigate` instead of `useHistory`  
          -- Replaced `props.match.params.id` with `_id`  
          -- Replaced route redirects like `props.history.push("/student-list")` with `navigate("/student-list")`  

**U** - I can Edit a student.  
**D** - I can Delete a student.  

3. **Front End - UX Update** = Added `useNavigate` to create-student.component.js  
    - User Confusion = After a new student is created there is a Confirmation Alert but the form data fields remained populated?   
      - Due to the field data remaining in the form fields I was unsure if the new student data was actually added to the Student List/databse?  
      - Should I manually delete the data in each field to create another new student?  
      - I had to click the "Student List" nav link to visually confirm the new student was added to the database.  

        - **UX Fix** = After the Confirmation Alert, I added `useNavigate` (similar to what I did on the Edit Student page) to automatically redirect the user to the Student List page to see the list of students, including the new student that was just added.  