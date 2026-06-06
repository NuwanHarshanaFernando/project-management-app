This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.


## Installing NPM Packages 

npm i @mui/material @emotion/react @emotion/styled @mui/x-data-grid lucide-react numeral date-fns axios recharts react-dnd react-dnd-html5-backend gantt-task-react

## Installing Typescript NPM Packages

npm i -D @types/node @types/uuid @types/numeral

## Installing Prettier plugin (It automatically sorts the tailwind classes)

npm i -D prettier prettier-plugin-tailwindcss

Then create .prettierrc file

## Installing tailwind-merge to merge certain classes for tailwind

npm i -D tailwind-merge

## Create darkMode property in tailwind.config.ts file
darkMode: "class",

## Create colors property in extend in tailwind.config.ts file
colors: {
    
}

Create dashboardWrapper.tsx file inside src/app folder

Create Navbar and Sidebar inside (components) folder in src/app folder

## Installing redux toolkit

npm i react-redux @reduxjs/toolkit redux-persist dotenv

Create redux.tsx file inside src/app folder

Copy and paste redux toolkit store with redux persist

## Handling the global reducer

Create state folder inside src directory
Create index.ts file inside the created state folder
Setup redux js toolkit in index.tsx file

Create state for 1-> light mode and dark mode, 2-> sidebarCollpsed or not

## Handling API calls

Create .env.local file inside client directory

NEXT_PUBLIC_API_BASE_URL=http://localhost:8000

Create api.ts inside state directory

## Link Redux with Nextjs application

Change DashboardWrapper to DashboardLayout and create a second Component called DashboardWrapper

Wrap DashboardLayout with StoreProvider which is from redux.tsx

Now we can use redux state inside DashboardWrapper

Define isSidebarCollaped and isDarkmode by useAppSelector() in DashboardWrapper.
Now we have access to these states.

## Change states from Navbar

Open Navbar -> index.tsx
dispatch by useAppDispatch() in Navbar

Changing state from lightMode to darkMode and vice versa by dispatching by the button in Navbar

## Change states from Sidebar

Create SidebarLink component in Sidebar/index.tsx

Add styles when Sidebar Collaped and Opened

## Server Side (Backend)

Create server directory 

Go to the server directory

npm init -y

It initiates package.json inside the server directory

## Installing type node dependencies

npm i -D ts-node typescript @types/node

npx tsc --init

It Created a new tsconfig.json  

Modify the .tsconfig file

## Installing prisma

npm i prisma @prisma/client

npx prisma init

It creates schema.prisma file

Copy and paste seedData folder in prisma folder

Create seed.ts file inside pisma folder

## Prisma
In .env

DATABASE_URL="postgresql://postgres:1234@localhost:5432/projectmanagement?schema=public"

To generate and connect prisma ->
npx prisma generate 

npx prisma migrate dev --name init

npm run seed

Cleared data from Team
Cleared data from Project
Cleared data from ProjectTeam
Cleared data from User
Cleared data from Task
Cleared data from Attachment
Cleared data from Comment
Cleared data from TaskAssignment
Seeded team with data from team.json
Seeded project with data from project.json
Seeded projectTeam with data from projectTeam.json
Seeded user with data from user.json
Seeded task with data from task.json
Seeded attachment with data from attachment.json
Seeded comment with data from comment.json
Seeded taskAssignment with data from taskAssignment.json

## In case of migration issue, to reset migration

npm prisma migrate reset

In pgAdmin -> projectmanagement -> Schemas -> Tables, there is data

Now the database is connected, now we can create our backend api using nodejs

## Installing packages for the backend

npm i express body-parser cors dotenv helmet morgan

express -> as server
body-parser -> to pass the requests
cors -> for cross origin issues
dotenv -> to manage env variables
helmet -> for sequire
morgan -> for API request login

## Installing typescript packages to run the application securely on node server

npm i -D rimraf concurrently nodemon @types/cors @types/express @types/morgan @types/node

Create src directory in server directory
Create index.ts file inside src directory

Run the backend server
npm run dev

Open a new terminal 
curl localhost:8000
It prints "This is a home route"

Create controllers directory inside src directory
Create projectController.ts file inside controllers directory

Create routes directory inside src directory

Create projectRoutes.ts file inside routes directory

Add this line inside projectRoutes.ts fils
router.get("/", getProjects);

Add this line inside index.tsx
'app.use("/projects", projectRoutes);'

curl http://localhost:8000/projects

It prints the project list

In ProjectController create createProject

Add this line inside projectRoutes.ts fils
router.post("/", createProject);

The error message is not descriptive:

export const createProject = async (
    req: Request,
     res: Response
): Promise<void> => {
    const { name, description, startDate, endDate } = req.body;
    try {
        const newProject = await prisma.project.create({
            data: {
                name,
                description,
                startDate,
                endDate
            }
        });
        res.status(201).json(newProject);
    } catch (error) {
        res.status(500).json({ message: "Error creating project" });
    }
}

To make it decriptive change this line:

   catch (error) {
        res.status(500).json({ message: "Error creating project" });
    }

    to that

    catch (error: any) {
        res.status(500).json({ message: `Error creating project: ${error.message}` });
    }


command for resetting id in database: 
`SELECT setval(pg_get_serial_sequence('"[DATA_MODEL_NAME_HERE]"', 'id'), coalesce(max(id)+1, 1), false) FROM "[DATA_MODEL_NAME_HERE]";`

In PgAdmin
On query Tool:
SELECT setval(pg_get_serial_sequence('"Project"', 'id'), coalesce(max(id)+1, 1), false) FROM "Project";

Then execute

In Postman application, POST teh request to create the new project
It gives the autoIncrementId and Post the new project without any error.


## Tasks

Inside controllers directory, create taskController.ts file

Create taskRoutes.ts file inside routes directory

Add this line inside index.ts
app.use("/tasks", taskRoutes);

curl http://localhost:8000/tasks?projectId=1

## Project Frontend

Go to src/state/api.ts file
Create interface Project as in projectController.ts in backend
Create interface Task as in taskController.ts in backend

Create enum Status and enum Priority

There are includes in getTasks in taskController.ts
           
            include:{
                author: true,
                assignee: true,
                comments: true,
                attachments: true,
            }

Therefore need to create Types of them too in api.ts

Create endpoints in api.ts

Create projects directory inside client/src/app
Create [id] folder insdide projects directory
Create page.tsx file inside [id] folder

Move (components) directory to the src directory
Change the name to components

Create ProjectHeader.tsx file inside projects directory

## Calling API end-points and get data
Set projects list in sidebar

Create Header directory in components directory
Create index.tsx file inside Header directory

Create BoardView directory inside projects directory
Inside it, create index.tsx file

## Grid view
Create ListView directory inside projects directory
Create index.tsx file inside ListView directory

Create another active tab for ListView inside page.tsx

Create TaskCard component

## Timeline View
Create TimelineView directory inside projects directory
Create index.tsx file inside TimelineView directory

Create another active tab for TimelineView inside page.tsx

Add class to the global.css

## Table View
Create another active tab for Table View inside page.tsx

Create TableView directory inside projects directory
Create index.tsx file inside TableView directory

Create lib folder inside src directory
Create utils.ts file inside lib folder

Define datagridClassNames in utils.ts file

## Projects Frontend Modals
Create Modal in ProjectHeader.tsx
Create Modal Component inside components directory

Create ModalNewProject directory inside projects directory
Inside it, create index.tsx

In page.tsx, use ModalNewTask

In ListView Header add a buttonComponent

Add buttonComponent in the TableView Header

Create ModalNewTask in components directory






















