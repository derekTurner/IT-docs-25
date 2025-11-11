# React Router

React router has a [framework](https://reactrouter.com/start/modes#framework) mode to develop a full stack application.  Documentatio is available on the react router site.

On the Stackoverflow survey or 2025 React Router has not been mentioned.  The framework is subject to changes as it is developed further.  However, it is a good starting point for full stack applications.


Remix can be downloaded with a number of ready made [variant stacks](https://github.com/remix-run/react-router-templates) supporting different databases and features.  I will use the minimum stack to develop from here, but you can investigate any of these alternatives.

The best introduction to React Router is the [Address book tutorial](https://reactrouter.com/tutorials/address-book#setup) and this should be run in a docker container using Vite for consistancy with other notes.

## Container for remix default page

Start by creating a new Github repository "AddressBook25" from Github desktop.

![new repository](images/newRep.png)

Name the new repository AddressBook25.

![AddressBook25](images/AddressBook25.png)


Create the repository.

Publish the empty repository to github.

Open the new folder in visual studio code.

> CTRL + SHIFT + P

Open folder in container.

![open folder](images/openfolder.png)

Select the folder AddressBook25.

Choose to add the configuration to the workspace so that it will be transferred to github and easily passed across to other machines.

![save config to workspace](images/toworkspace.png)

Choose a node.js and typescript configuiration.

![nodejs and typescript](images/nodetypescript.png)

Select node version 22.  Remember that node version manager can be used to install different versions of node locally.


![bookworm](images/bookworm.png)

No additional features are required.

![no additional features](images/noadditional.png)

You will be offered github dependabot.  This is an alert system which identifies when the repository is using a software dependency with a known vunerability.  That is a good security feature.  However, we will not use this for the time being as it may lead to updates out of sync with these notes.

![no dependabot](images/nodependabot.png)

Allow time for the container to download software required.

In a new terminal

> npm install -D vite

```bash
added 13 packages in 7s

5 packages are looking for funding
  run `npm fund` for details
npm notice
npm notice New major version of npm available! 10.8.3 -> 11.6.2
npm notice Changelog: https://github.com/npm/cli/releases/tag/v11.6.2
npm notice To update run: npm install -g npm@11.6.2
npm notice 
```
Update  npm as suggested.

> npm install -g npm@11.6.2

```bash
added 1 package in 4s

28 packages are looking for funding
  run `npm fund` for details
```

Now install and initialise vite

> npm install

```bash
added 1 package, and audited 15 packages in 969ms

5 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```

> npm init vite

```bash
Need to install the following packages:
create-vite@6.5.0
Ok to proceed? (y) 
```

>y

Set project name to 'contacts'

```bash
│
◆  Project name:
│  contacts█
└
```

Select React as the framework

```bash
◆  Select a framework:
│  ○ Vanilla
│  ○ Vue
│  ● React
│  ○ Preact
│  ○ Lit
│  ○ Svelte
│  ○ Solid
│  ○ Qwik
│  ○ Angular
│  ○ Marko
│  ○ Others
└
```

Select React Router as the variant

```bash
◆  Select a variant:
│  ○ TypeScript
│  ○ TypeScript + SWC
│  ○ JavaScript
│  ○ JavaScript + SWC
│  ● React Router v7 ↗ (npm create react-router@latest)
│  ○ TanStack Router ↗
│  ○ RedwoodSDK ↗
└
```

This will request an installation of create react router.

```bash
Need to install the following packages:
create-react-router@7.9.5
Ok to proceed? (y) 
```

> y
 
Wait for software to download ... this was a long wait, there ar some warnings about depracated code.

```bash
> npx
> "create-react-router" contacts


         create-react-router v7.9.5
      ◼  Directory:
         Using contacts as project directory

      ◼  Using default template
         See https://github.com/remix-run/react-router-templates for more
      ✔  Template copied

   git   Initialize a new git repository? (recommended)
        ○ Yes  ● No 
```
Select NO for git repository as one is already set up.

```bash
   deps   Install dependencies with npm? (recommended)
         ● Yes  ○ No 
```


Select yes for dependencies and wait for download

```bash
      ✔  Dependencies installed

  done   That's it!

 Enter your project directory using cd ./contacts
 Check out README.md for development and deploy instructions.

 Join the community at https://rmx.as/discord
```
At the end of the process there should be a package.json file in the root folder which holds the vite dependency for any project in the folder.

```json
{
  "devDependencies": {
    "vite": "^6.4.1"
  }
}
```
In the contacts folder there is a package.json file which holds the dependencies and scripts for the project.

```json
{
  "name": "contacts",
  "private": true,
  "type": "module",
  "scripts": {
    "build": "react-router build",
    "dev": "react-router dev",
    "start": "react-router-serve ./build/server/index.js",
    "typecheck": "react-router typegen && tsc"
  },
  "dependencies": {
    "@react-router/node": "^7.9.2",
    "@react-router/serve": "^7.9.2",
    "isbot": "^5.1.31",
    "react": "^19.1.1",
    "react-dom": "^19.1.1",
    "react-router": "^7.9.2"
  },
  "devDependencies": {
    "@react-router/dev": "^7.9.2",
    "@tailwindcss/vite": "^4.1.13",
    "@types/node": "^22",
    "@types/react": "^19.1.13",
    "@types/react-dom": "^19.1.9",
    "tailwindcss": "^4.1.13",
    "typescript": "^5.9.2",
    "vite": "^7.1.7",
    "vite-tsconfig-paths": "^5.1.4"
  }
}
```

> cd contacts

> npm install

```bash
node ➜ /workspaces/AdressBook25 (main) $ cd contacts
node ➜ /workspaces/AdressBook25/contacts (main) $ npm install
npm warn EBADENGINE Unsupported engine {
npm warn EBADENGINE   package: 'vite@7.2.2',
npm warn EBADENGINE   required: { node: '^20.19.0 || >=22.12.0' },
npm warn EBADENGINE   current: { node: 'v22.9.0', npm: '10.8.3' }
npm warn EBADENGINE }
```
Time to install a more recent version of node.js.  Use nvm to install version 22.19.0.

>curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

> nvm install --lts

```bash
Installing latest LTS version.
Downloading and installing node v24.11.0...
Downloading https://nodejs.org/dist/v24.11.0/node-v24.11.0-linux-x64.tar.xz...
################################################################### 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v24.11.0 (npm v11.6.1)
```
Try again in contacts folder.

> npm install

```bash
added 65 packages, and audited 343 packages in 1s

57 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
```
The installation is complete.

Add the --host flag to the dev script in the package.json file.

```json
 "scripts": {
    "build": "react-router build",
    "dev": "react-router dev --host",
    "start": "react-router-serve ./build/server/index.js",
    "typecheck": "react-router typegen && tsc"
  },
```  

## Test the default react router site

> npm run dev

![default site](images/DefaultSite.png)


This is not the address book tutorial site, but it shows that the remix framework is working.

## Tutorial site

>cd ..

> npx create-react-router@latest --template remix-run/react-router/tutorials/address-book

```bash
        create-react-router v7.9.5

   dir   Where should we create your new project?
         ./contacts
```
Select the contacts folder.

```bash
   ◼  Template:
         Using remix-run/react-router/tutorials/address-book...
      ✔  Template copied
```        
Then

```bash
 overwrite   Your project directory contains files that will be overwritten by
             this template (you can force with `--overwrite`)

             Files that would be overwritten:
               .gitignore
               app
               app/app.css
               app/root.tsx
               app/routes.ts
               and 7 more...

             Do you wish to continue?
             
             ● Yes  ○ No 
```             
Select yes to overwrite the existing files.

```bash
   git   Initialize a new git repository? (recommended)
        ○ Yes  ● No 
```
Select NO for git repository as one is already set up.

```bash
   deps   Install dependencies with npm? (recommended)
         ● Yes  ○ No 
```
Wait ...

```bash
      ✔  Dependencies installed

  done   That's it!

 Enter your project directory using cd ./contacts
 Check out README.md for development and deploy instructions.

 Join the community at https://rmx.as/discord
 ```

 >cd contacts

Restore --host to dev script in package.json file.

```json
  "scripts": {
    "build": "cross-env NODE_ENV=production react-router build",
    "dev": "react-router dev --host",
    "start": "cross-env NODE_ENV=production react-router-serve ./build/server/index.js",
    "typecheck": "react-router typegen && tsc"
  },
```

> npm run dev

The address book tutorial site should now be displayed in its starting form.

![first contact](images/firstcontact.png)

## Explore the project files


The project folder contains the following files:

![project files](images/projectfiles.png)

Below these are the configuration files.

** vite.config.ts **
```typescript
import { reactRouter } from "@react-router/dev/vite";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [reactRouter()],
});
```
Note that the reactRouter plugin runs in vite. 

**tsconfig.json**
```json
{
  "include": [
    "**/*",
    "**/.server/**/*",
    "**/.client/**/*",
    ".react-router/types/**/*"
  ],
  "compilerOptions": {
    "lib": ["DOM", "DOM.Iterable", "ES2022"],
    "types": ["node", "vite/client"],
    "target": "ES2022",
    "module": "ES2022",
    "moduleResolution": "bundler",
    "jsx": "react-jsx",
    "rootDirs": [".", "./.react-router/types"],
    "baseUrl": ".",
    "esModuleInterop": true,
    "verbatimModuleSyntax": true,
    "noEmit": true,
    "resolveJsonModule": true,
    "skipLibCheck": true,
    "strict": true
  }
}
```

The tsconfig.json file is the configuration file for typescript.  This is used to set up the project to use typescript.  Note that the target is set to es2022 and the module is set to es2022.  This is to ensure that the project is compatible with browsers that support es2020.  The features of ECMAscript update annually.  EcmaScript 2022 features are summarised by [w3 schools ECMAScript 2022](https://www.w3schools.com/js/js_2022.asp).

Vite takes care of building the project and running it so typescript is set to "noEmit:true.

## Tutorial

From here the [tutorial online](https://reactrouter.com/tutorials/address-book#setup) can be followed.

The file app/root.tsx is the first component rendered and it contains the global layout for the application. 

```javascript
import {
  Form,
  Scripts,
  ScrollRestoration,
  isRouteErrorResponse,
} from "react-router";
import type { Route } from "./+types/root";

import appStylesHref from "./app.css?url";

export default function App() {
  return (
    <>
      <div id="sidebar">
        <h1>React Router Contacts</h1>
        <div>
          <Form id="search-form" role="search">
            <input
              aria-label="Search contacts"
              id="q"
              name="q"
              placeholder="Search"
              type="search"
            />
            <div
              aria-hidden
              hidden={true}
              id="search-spinner"
            />
          </Form>
          <Form method="post">
            <button type="submit">New</button>
          </Form>
        </div>
        <nav>
          <ul>
            <li>
              <a href={`/contacts/1`}>Your Name</a>
            </li>
            <li>
              <a href={`/contacts/2`}>Your Friend</a>
            </li>
          </ul>
        </nav>
      </div>
    </>
  );
}

// The Layout component is a special export for the root route.
// It acts as your document's "app shell" for all route components, HydrateFallback, and ErrorBoundary
// For more information, see https://reactrouter.com/explanation/special-files#layout-export
export function Layout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <head>
        <meta charSet="utf-8" />
        <meta
          name="viewport"
          content="width=device-width, initial-scale=1"
        />
        <link rel="stylesheet" href={appStylesHref} />
      </head>
      <body>
        {children}
        <ScrollRestoration />
        <Scripts />
      </body>
    </html>
  );
}

// The top most error boundary for the app, rendered when your app throws an error
// For more information, see https://reactrouter.com/start/framework/route-module#errorboundary
export function ErrorBoundary({
  error,
}: Route.ErrorBoundaryProps) {
  let message = "Oops!";
  let details = "An unexpected error occurred.";
  let stack: string | undefined;

  if (isRouteErrorResponse(error)) {
    message = error.status === 404 ? "404" : "Error";
    details =
      error.status === 404
        ? "The requested page could not be found."
        : error.statusText || details;
  } else if (
    import.meta.env.DEV &&
    error &&
    error instanceof Error
  ) {
    details = error.message;
    stack = error.stack;
  }

  return (
    <main id="error-page">
      <h1>{message}</h1>
      <p>{details}</p>
      {stack && (
        <pre>
          <code>{stack}</code>
        </pre>
      )}
    </main>
  );
}
```

The function App() returns the sidebar component for the application.  This contains a form to search contacts and a form to add a new contact.  There is also a navigation component which contains links to two contacts.

The function Layout() is a special export for the root route.  It acts as the document's "app shell" for all route components.  

To create a route to match the url /contacts/1 a new file routes.tsx is created in the app/routes folder.

** routes.tsx **
```javascript
import type { RouteConfig } from "@react-router/dev/routes";
import { route } from "@react-router/dev/routes";

export default [
  route("contacts/:contactId", "routes/contact.tsx"),
] satisfies RouteConfig;
```
If a route follows the pattern contacts/123 then the value 123 will be passed to the contactId parameter in the route.

The toute targets the route module contact.tsx which is created in the app/routes folder.

** app/routes/contct.tsx**
```javascript
import { Form } from "react-router";

import type { ContactRecord } from "../data";

export default function Contact() {
  const contact = {
    first: "Your",
    last: "Name",
    avatar: "https://placecats.com/200/200",
    twitter: "your_handle",
    notes: "Some notes",
    favorite: true,
  };

  return (
    <div id="contact">
      <div>
        <img
          alt={`${contact.first} ${contact.last} avatar`}
          key={contact.avatar}
          src={contact.avatar}
        />
      </div>

      <div>
        <h1>
          {contact.first || contact.last ? (
            <>
              {contact.first} {contact.last}
            </>
          ) : (
            <i>No Name</i>
          )}
          <Favorite contact={contact} />
        </h1>

        {contact.twitter ? (
          <p>
            <a
              href={`https://twitter.com/${contact.twitter}`}
            >
              {contact.twitter}
            </a>
          </p>
        ) : null}

        {contact.notes ? <p>{contact.notes}</p> : null}

        <div>
          <Form action="edit">
            <button type="submit">Edit</button>
          </Form>

          <Form
            action="destroy"
            method="post"
            onSubmit={(event) => {
              const response = confirm(
                "Please confirm you want to delete this record.",
              );
              if (!response) {
                event.preventDefault();
              }
            }}
          >
            <button type="submit">Delete</button>
          </Form>
        </div>
      </div>
    </div>
  );
}

function Favorite({
  contact,
}: {
  contact: Pick<ContactRecord, "favorite">;
}) {
  const favorite = contact.favorite;

  return (
    <Form method="post">
      <button
        aria-label={
          favorite
            ? "Remove from favorites"
            : "Add to favorites"
        }
        name="favorite"
        value={favorite ? "false" : "true"}
      >
        {favorite ? "★" : "☆"}
      </button>
    </Form>
  );
}
```

... continue to follow the tutorial online on the react router site ...



