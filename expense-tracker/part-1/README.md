## Part 1 Description
In this part, you will configure frontend and backend repositories, create a library of reusable components, work with responsive design, practice client-browser interaction, work with data validation, create your first CRUD, work with a database

<!-- ## Starter Repositories
You can fork these repositories to get started. They contain basic tests. If you don't find a repository with the stack you need, create a repository yourself
  - [API](https://github.com/petproject-dev/expense-tracker-backend-part-1) - Express.js
  - [UI](https://github.com/petproject-dev/expense-tracker-frontend-part-1) - React -->

## Backend

<details>
  <summary>Task 1: Setup Environment</summary>

  ---

  **Description:**

  Prepare the development environment for the project. Create the necessary project structure, initialize the development configuration, and ensure basic tools are set up to streamline the workflow.

  **Acceptance Criteria:**

  - A development environment is initialized with appropriate configuration.
  - A basic project structure is created (e.g., with a folder for source files).
  - A script is available to start the project in development mode.
  - Upon running the project, it outputs "Hello, World!" to verify successful setup.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Use `npm init` to initialize the project.
  - Set up TypeScript with `tsconfig.json` and enable strict mode (`strict: true`).
  - Install `ts-node-dev` for hot reloading.
  - Organize the project structure with a `src/` directory and an entry point like `src/index.ts`.
  - Add a dev script in package.json to run the project using ts-node-dev.
  </details>


---

</details>

<details>
  <summary>Task 2: Create a Basic REST API</summary>

  ---

  **Description:**

  Set up a basic REST API with at least one route to verify the routing and response handling functionality.

  **Acceptance Criteria:**

  - A basic route `GET /ping` is implemented.
  - The route responds with a predefined message (e.g., `{"message":"pong"}`).
  - The application uses a configurable port.
  - A file for environment variables (`.env`) is created, and sensitive data is excluded from version control.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Install and use express for routing.
  - Use `dotenv` to load environment variables and configure a port (e.g., `PORT=8080`).
  - Add `.env` to `.gitignore` and create a `.env.example` file with placeholder values.
  - Add `config/index.ts` file for configuring environment variables.
  - Set up `src/app.ts` to centralize middleware and routing.
  </details>

  <br />

  **Materials:**

  - [REST](https://restfulapi.net/)
  - [Environment variable](https://en.wikipedia.org/wiki/Environment_variable)

---

</details>

<details>
  <summary>Task 3: Implement Linting and Formatting</summary>

  ---

  **Description:**

  Set up tools to enforce consistent code quality and style across the project.

  **Acceptance Criteria:**

  - Linting is set up using a linter.
  - Formatting is handled automatically using a formatter.
  - Pre-configured commands check and fix linting and formatting issues.
  - Editor configuration ensures consistent behavior across different IDEs.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Install eslint with TypeScript support (`@typescript-eslint/parser` and `@typescript-eslint/eslint-plugin`).
  - Use `eslint-config-prettier` to integrate ESLint with Prettier.
  - Install prettier and create a .prettierrc file with formatting rules.
  - Add scripts into the `package.json`:
    - `build` – build the project
    - `lint` – check the project using eslint rules
    - `lint:fix` – check the project using eslint rules and fix errors
    - `format` – formatting project using prettier rules
    - `start` – start the project in production mode
  - Use `husky` and `lint-staged` to enforce linting/formatting on `pre-commit`.
  </details>

  <br />

  **Materials:**

  - [How to Use Linters and Code Formatters in Your Projects](https://www.freecodecamp.org/news/using-prettier-and-jslint/)

---

</details>

<details>
  <summary>Task 4: Set Up SQLite Database (Raw Queries)</summary>

  ---

  **Description:**

  Initialize and configure a SQLite database for storing project data. Set up a basic schema and implement raw queries to interact with the database.

  This step is added for educational purposes so that you understand what is hidden under the hood of an ORM. The following tasks will remove most of the code.

  **Acceptance Criteria:**

  - SQLite driver is installed.
  - A database connection is established, and an initial schema is created.
  - The schema includes a table for expenses.
    - id (integer, primary key)
    - name (text)
    - amount (real)
    - currency (text)
    - category (text)
    - date (datetime)
  - Basic endpoints allow adding and retrieving expense records.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Use the `better-sqlite3` package for efficient SQLite interaction.
  - Initialize the database in `src/db/db.service.ts` and ensure connection errors are handled.
  - Implement raw queries for inserting and selecting records in the `src/app.ts` file.
  </details>


---

</details>

<details>
  <summary>Task 5: Set Up SQLite Database (ORM)</summary>

  ---

  **Description:**

  Set up an ORM for database interaction to simplify schema management and querying.

  **Acceptance Criteria:**

  - The ORM is installed and configured.
  - A schema is defined, and migrations are used to update the database.
  - Basic database operations use the ORM.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Use prisma for ORM and schema management.
  - Initialize Prisma with `npx prisma init` and configure the database URL in `.env`.
  - Define the expenses model in `prisma/schema.prisma`.
  - Use npx prisma migrate dev to apply schema changes.
  - Generate the Prisma client and use it in the exist endpoints.
  </details>

  <br />

  **Materials:**

  - [What is an ORM?](https://www.prisma.io/dataguide/types/relational/what-is-an-orm)

---

</details>

<details>
  <summary>Task 6: Create Route for Adding Expenses</summary>

  ---

  **Description:**

  Set up routes for basic Create operation on the expenses table.

  **Acceptance Criteria:**

  - Route for adding expenses are implemented:
    - `POST /api/expenses` Creates new expense record.
  - Data is validated to ensure correctness before saving to the database.
  - A modular structure is established for `controllers`, `services`, `repositories`, and `entities`.
  - Middleware for error handling and validation is implemented.
  - The application structure matches the defined project layout.
  - Processing 404 status code defined.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Use express to define routes and middleware.
  - Place the business logic for expenses in `expenses.service.ts`.
  - Implement database interaction methods in `expenses.repository.ts`.
  - Use a DTO (Data Transfer Object) in `expenses/dto` to define the shape of - request payloads.
  - Create an `expenses.entity.ts` file to define the database model or schema.
  - Use middleware (`helpers/middlewares/validator.ts`) to validate incoming - requests.
  - Implement centralized error handling in `helpers/middlewares/errorHandler.ts`
  - Code structure is following:
```
    │   app.ts
    │   index.ts
    ├───config
    │       index.ts
    ├───db
    │       db.service.ts
    ├───expenses
    │   │   expenses.controller.ts
    │   │   expenses.repository.ts
    │   │   expenses.service.ts
    │   ├───dto
    │   │       create-expense.dto.ts
    │   └───entity
    │           expense.entity.ts
    └───helpers
        │   Exception.ts
        └───middlewares
                errorHandler.ts
                validator.ts
```
  </details>

  <br />

  **Materials:**

  - [Services, Controllers and Repositories. An Introduction](https://gabrielgomes61320.medium.com/services-controllers-and-repositories-an-introduction-241ac52cdd93)
  - [Understanding the Building Blocks of a Web Application: Routes, Controllers, Services, Repositories, and Databases](https://codewithmatt.hashnode.dev/understanding-the-building-blocks-of-a-web-application-routes-controllers-services-repositories-and-databases)


---

</details>

<details>
  <summary>Task 7: Create Endpoint for getting list of expenses</summary>

  ---

  **Description:**

  Set up route for retrieving expenses from the database. Include operations for fetching all expenses (with optional pagination and filtering).

  **Acceptance Criteria:**

  - Route for retrieving expenses are implemented:
    - `GET /api/expenses` Fetches and returns all expenses with optional query parameters:
      - Pagination: `limit` and `offset`.
      - Filtering: `fromDate` and `toDate` based on the date field.
  - Response include appropriate HTTP status codes and data.
  - Modular structure follows the established pattern.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Prepare all the necessary data in the `expenses.controller.ts`.
  - Implement business logic for fetching expenses in `expenses.service.ts`.
  - Handle database queries in `expenses.repository.ts`.
  </details>

  **Materials:**

  - [A guide to REST API pagination](https://www.merge.dev/blog/rest-api-pagination)

---

</details>

<details>
  <summary>Task 8: Create endpoint for getting expense by id</summary>

  ---

  **Description:**

  Set up route for retrieving expense from the database. Include operation for fetching a specific expense by ID.

  **Acceptance Criteria:**

  - Routes for retrieving expenses are implemented:
    - `GET /api/expenses/:id` Fetches a specific expense by its ID.
  - Responses include appropriate HTTP status codes and data.
  - Modular structure follows the established pattern.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Prepare all the necessary data in the `expenses.controller.ts`.
  - Implement business logic for fetching expenses in `expenses.service.ts`.
  - Handle database queries in `expenses.repository.ts`.
  </details>

---

</details>

<details>
  <summary>Task 9: Create Routes for Updating and Deleting Expenses</summary>

  ---

  **Description:**

  Set up route for updating expense records in the database. Ensure that only specified fields are updated during PATCH operations.

  **Acceptance Criteria:**

  - Route for updating expense are implemented:
      - `PATCH /api/expenses/:id` Updates specific fields of an expense.
  - Data is validated to ensure correctness before processing requests.
  - Responses include appropriate HTTP status codes and data.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Prepare all the necessary data in the `expenses.controller.ts`.
  - Implement business logic for fetching expenses in `expenses.service.ts`.
  - Handle database queries in `expenses.repository.ts`.
  - Use DTOs in `expenses/dto` to validate request payloads and parameters.
  - Use middleware (`helpers/middlewares/validator.ts`) for data validation.
  </details>

---

</details>

<details>
  <summary>Task 10: Create Route for Deleting Expenses</summary>

  ---

  **Description:**

  Set up route for deleting expense records in the database

  **Acceptance Criteria:**

  - Route for deleting expenses are implemented:
      - `DELETE /api/expenses/:id` Deletes an expense by its ID.
  - Response include appropriate HTTP status code.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Prepare all the necessary data in the `expenses.controller.ts`.
  - Implement business logic for fetching expenses in `expenses.service.ts`.
  - Handle database queries in `expenses.repository.ts`.
  </details>

---

</details>

<details>
  <summary>Task 11: Implement Basic Logging</summary>

  ---

  **Description:**

  Add logging functionality to track significant events (e.g., expense creation, updates, and errors). Ensure logs are accessible in both development and production environments.

  **Acceptance Criteria:**

  - Logs are added for key actions:
    - Successful expense creation, updates, and deletions.
    - Errors during request handling.
  - Logs are displayed in the console during development.
  - Logs are written to a file in production.

  **Technology-related requirements:**

  <details>
  <summary>NodeJS</summary>

  - Use a logging library like winston or pino.
  - Place logging configuration in helpers/Logger.ts.
  - Code structure is following:
```
  │   app.ts
  │   index.ts
  ├───config
  │       index.ts
  ├───db
  │       db.service.ts
  ├───expenses
  │   │   expenses.controller.ts
  │   │   expenses.repository.ts
  │   │   expenses.service.ts
  │   ├───dto
  │   │       create-expense.dto.ts
  │   │       update-expense.dto.ts
  │   └───entity
  │           expense.entity.ts
  └───helpers
      |    dateUtils.ts
      │   Exception.ts
      │   Logger.ts
      └───middlewares
              errorHandler.ts
              validator.ts
```
  </details>

  <br />

  **Materials:**

  - [REST API Logging](https://romanglushach.medium.com/java-rest-api-logging-best-practices-and-guidelines-bf5982ee4180)

---

</details>

<details>
  <summary>Task 12: Final step</summary>

  ---

  - Open a pull request for the `master` branch and send the solution to the code review

  ---

</details>

## Frontend

<details>
  <summary>Task 1: Setup Development Environment</summary>

  ---

  **Description:**

  Prepare the development environment for the project. Initialize the necessary configurations for a smooth development process, including TypeScript setup and project structure organization.

  **Acceptance Criteria:**

  - A development environment is initialized with appropriate configuration.
  - TypeScript is installed and properly configured (`tsconfig.json` is set up).
  - Project structure is organized (e.g., `src/` for source files).
  - Running a development command starts the project in dev mode.
  - Configure TypeScript paths for cleaner imports.

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  - Use [Vite](https://vite.dev/guide/) for initialization.
  </details>

---

</details>

<details>
  <summary>Task 2: Implement Linting and Formatting</summary>

---

  **Description:**

  Set up linting and formatting to maintain consistent code quality across the project. Configure ESLint, Prettier, and Stylelint, along with EditorConfig to ensure consistency.

  **Acceptance Criteria:**

  - ESLint is installed and configured.
  - Prettier is installed and integrated with ESLint.
  - Stylelint is installed for CSS linting.
  - EditorConfig is set up with rules for indentation, line endings, etc.
  - Scripts added:
      - `lint` - Checks the project for linting issues.
      - `lint:fix` - Fixes linting issues.
      - `stylelint` - Checks the project for css linting issues.
      - `stylelint:fix` - Fixes css linting issues.
      - `format` - Formats code based on Prettier rules.

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  - Use plugins such as `eslint-plugin-react` for React-specific linting.
  - Configure `stylelint-config-standard` for CSS linting.

  </details>

  <br/>

  **Materials:**

  <details>
  <summary>React</summary>

  - [Supercharge Your React Development with Vite, ESLint, and Prettier in VSCode](https://dev.to/topeogunleye/building-a-modern-react-app-with-vite-eslint-and-prettier-in-vscode-13fj)
  - [Using ESLint + Husky + Lint-staged](https://medium.com/@bkn020612/using-eslint-husky-lint-staged-6d6609b02fc2)

  </details>

---

</details>

<details>
  <summary>Task 3: Create Logo component</summary>

---

  **Description:**
  Develop foundational reusable component that can be utilized across the application.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=2-19420&m=dev&t=GKFeiEqjFghP7rf5-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  ```jsx
  <Logo />
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>
---

</details>

<details>
  <summary>Task 4: Create Loader component</summary>

---

  **Description:**
  Develop foundational reusable component that can be utilized across the application.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=1-3471&m=dev&t=AyMjf1BcxpIwHBXC-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  ```jsx
  <Loader />
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>
---

</details>

<details>
  <summary>Task 5: Create Button component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. A standard button with support for different states(e.g., disabled, active).

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=2-19193&m=dev&t=GKFeiEqjFghP7rf5-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  ```jsx
  <Button disabled onClick={handleClick}>Click me</Button>
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>

  ---

</details>

<details>
  <summary>Task 6: Create Input Label component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. The label appears above many of our components. This should be a stylized label html tag with all the standard label features.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=2-19389&m=dev&t=GTL1yhChXxd9Efzr-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  - Example:

  ```jsx
  <>
    <InputLabel>Name</InputLabel>

    <InputLabel htmlFor="name1">Name</InputLabel>
  </>
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>

  ---

</details>

<details>
  <summary>Task 7: Create Input component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. A text input field with validation and style support.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=2-19412&m=dev&t=ra9tjWdp5aVmkqRH-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  ```jsx
  <>
    <Input />
    <Input helperText="Error message" />
    <Input
      type="text"
      placeholder="Enter name"
      defaultValue={name}
      error
      helperText="Error message"
      onChange={handleChange} />
  </>
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>

  ---

</details>

<details>
  <summary>Task 8: Create Icon component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. A component for rendering SVG icons.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=7-5669&m=dev&t=ra9tjWdp5aVmkqRH-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  - Create an `Icon` component for rendering SVG icons, with a name prop for specifying the icon and size for scaling.

  ```jsx
  <>
    <Icon iconName="plus" size={15} color="white" />
    <Icon iconName="plus" />
  </>
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>

  ---

</details>

<details>
  <summary>Task 9: Create Date Picker component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. A component for selecting date. This component is complex and its styles does not necessarily match the design. You can use standard `<input type="date" />`

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=71-5906&m=dev&t=AyMjf1BcxpIwHBXC-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  - Implement a `DatePicker` component for selecting the date, with support for a value prop and onChange callback.
  ```jsx
  <DatePicker
    value={selectedDate}
    onChange={handleDateChange} />
  <DatePicker />
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>

  ---

</details>

<details>
  <summary>Task 10: Create Table component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. A customizable `Table`, `TableHead`, `TableBody`, `TableRow`, `TableCell` components. Since we have a responsive design and it is complex with styling in the form that we offer, you can use `divs`. But if you feel that you can handle it, you can use standard table tags

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=2-19441&m=dev&t=ra9tjWdp5aVmkqRH-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  ```jsx
  <Table>
    <TableHead>
      <TableRow>
        <TableCell>Column<TableCell>
      </TableRow>
    </TableHead>
    <TableBody>
      <TableRow>
        <TableCell>Column<TableCell>
      </TableRow>
    </TableBody>
  </Table>
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>

  ---

</details>

<details>
  <summary>Task 11: Create Menu component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. Component for displaying menu items after click.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=3-13999&m=dev&t=cvakLOlrrBuwZq9F-4)

  **Technology-related requirements:**
  <details>
  <summary>React</summary>

  - Implement a `Menu` and `MenuItem` components.
  ```jsx
  <Menu>
    <MenuItem onClick={handleEdit}>Edit</MenuItem>
    <MenuItem onClick={handleDelete}>Delete</MenuItem>
  </Menu>
  ```
  </details>

  <br />

  **Materials:**

  - [HTML Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp)

  <details>
  <summary>React</summary>

  - [Your First Component](https://react.dev/learn/your-first-component)
  - [Building Reusable UI Components](https://medium.com/cstech/building-reusable-ui-components-with-react-best-practices-and-patterns-24b6fe921347)
  </details>

  ---

</details>

<details>
  <summary>Task 12: Create Button Icon component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. Reuse the previously created icon component

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=2-19187&m=dev&t=GKFeiEqjFghP7rf5-4)

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  ```jsx
  <IconButton>
    <Icon icon="close" color="white" size={12} />
  </IconButton>
  ```
  </details>

  ---

</details>

<details>
  <summary>Task 13: Create Icon Radio component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. Reuse the previously created icon component.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=4-34033&m=dev&t=GTL1yhChXxd9Efzr-4)

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  ```jsx
  <IconRadio name="category">
    <Icon icon="credits" size={24} />
  </IconRadio>
  ```
  </details>

  ---

</details>

<details>
  <summary>Task 14: Create Category Group component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. Based on the `IconRadio` and `Icon` components, create a CategoryGroup component. When you click on the icon it should be activated. User can only select one category

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=4-34103&m=dev&t=cvakLOlrrBuwZq9F-4)

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  ```jsx
  <>
    <CategoryGroup defaultValue="mobile" />
    <CategoryGroup />
  </>
  ```
  </details>

  ---

</details>

<details>
  <summary>Task 15: Create Input with Currency component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. An extension of the standard input, displaying the selected currency.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=2-19408&m=dev&t=ra9tjWdp5aVmkqRH-4)

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  ```jsx
  <>
    <InputWithCurrency />
    <InputWithCurrency
      id="name4"
      defaultValue="123"
      selectProps={{ defaultValue: 'USD' }} />
    <InputWithCurrency
      id="name4"
      onChange={handleAmountChange}
      defaultValue="123"
      selectProps={{
        defaultValue: 'USD',
        onChange: handleCurrencyChange }} />
  </>
  ```
  </details>

  ---

</details>

<details>
  <summary>Task 16: Create Date Picker Range component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. A component for selecting dates. To change the range date, you need to click on one of the date and a ready-made date picker component should appear

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=3-2073&m=dev&t=ra9tjWdp5aVmkqRH-4)

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  ```jsx
  <DatePickerRange
    from={fromDate}
    to={toDate}
    onChange={handleUpdateDateRange} />
  ```
  </details>

  ---

</details>

<details>
  <summary>Task 17: Create Expense Table component</summary>

  ---

  **Description:**
  Develop foundational reusable component that can be utilized across the application. Component for displaying expenses based on an already implemented `Table` component.

  **Acceptance Criteria:**
  - [Design Link](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=1-3551&m=dev&t=AyMjf1BcxpIwHBXC-4)
  - If there is no data, then a message with an image should be displayed as in the [design](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=1-3601&m=dev&t=XWnEQbC9qTwXBf01-4)
  - If there is no data and a request response is expected, then a [stub should be displayed](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=1-3585&m=dev&t=XWnEQbC9qTwXBf01-4)
  - If there is initial data, but a new portion of data is expected to be loaded, then the [spinner](https://www.figma.com/design/rLNUulPqnl0jhhnXeGDxEb/Expense-tracker?node-id=1-3471&m=dev&t=XWnEQbC9qTwXBf01-4) is displayed

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  ```jsx
  <ExpenseTable />
  ```
  </details>

  ---

</details>


<details>
  <summary>Task 18: Implement Sidebar Component</summary>

---

  **Description:**

  Create a Sidebar component that appear after clicking `plus` button

  **Acceptance Criteria:**

  - The sidebar open button is rendered in the lower right corner.
  - When user click the button, a sidebar appears on the right
  - Sidebar styles and content match the design.
  - The sidebar contains a form for creating a new expense record. The logic for creating a record at this step does not need to be done
  - *The sidebar appear with smooth animation.
  - *When the user clicks outside the `Sidebar` or presses the esc key, the component should close.

  **Materials:**

  - [CSS Animations](https://www.w3schools.com/css/css3_animations.asp)

---

</details>


<details>
  <summary>Task 19: Implement Layout Component</summary>

---

  **Description:**

  Create a Layout component that includes Header and Sidebar

  **Acceptance Criteria:**

  - A layout component has been created which is a general wrapper for the application.
  - A header component is implemented and displayed on the layout.
  - The layout is a wrapper and can be added to any of the future pages.

---

</details>


<details>
  <summary>Task 20: Build Responsive Layout</summary>

  ---

  **Description:**

  Implement a responsive design for the application that adapts to different screen sizes, ensuring usability on both mobile and desktop devices.

  **Acceptance Criteria:**

  - The application layout adjusts seamlessly between mobile, tablet, and desktop views. The tablet version is not included in the design. Style it however you see fit.
  - Key components, are responsive and match the design.

---

</details>

 <details>
  <summary>Task 21: Display Expenses Table</summary>

  ---

  **Description:**

  `ExpenseTable` component is already created. Connect data to it and display component on the screen

  **Acceptance Criteria:**

  - If no expenses are available, a placeholder message is displayed.
  - If expenses are loading, a skeleton is shown.
  - Pagination implemented. When the user scrolls to the end of the screen, a new piece of data should be loaded. When new data is loaded, a spinner should appear at the bottom of the table.
  - Filtering is implemented. The user selects a range of dates and the table is redrawn taking into account the selected dates.
  - *When the user clicks outside the `DatePickerRange` or presses the esc key, the component should close.

  **Endpoints:**

  - `GET /api/expenses` - Fetch all expenses.
    - `limit` - Number of records per page.
    - `offset` - Offset for pagination.
    - `fromDate` -and toDate: Filter by date range.

  **Materials:**

  - [Client-Server Overview](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Server-side/First_steps/Client-Server_overview)
  - [How to implement infinite scrolling in Javascript](https://www.educative.io/answers/how-to-implement-infinite-scrolling-in-javascript)
  - [Event loop](https://www.youtube.com/watch?v=8aGhZQkoFbQ)

  <details>
  <summary>React</summary>

  - [How to Create Infinite Scrolling in React Using the Intersection Observer API](https://www.freecodecamp.org/news/infinite-scrolling-in-react/)
  </details>

---

</details>

<details>
  <summary>Task 22: Implement Add Expense Functionality</summary>

  ---

  **Description:**

  Create a form for adding a new expense. The form should be accessible through a right sidebar that opens when clicking the "+" button.

  **Acceptance Criteria:**

  - A button triggers the display of a right sidebar with the form.
  - The form includes fields for Name, Payment amount, Category and Date.
  - Submitting the form sends data to the backend and updates the table.
  - Data validation has been added to the form. All fields are required and correspond to the type specified in the database. When user click on the submit button, if the field has an invalid value, an error message should be displayed under the input and also the input should have a red border.
  - *The sidebar appear with smooth animation.
  - *In case of error, the input should have a shaking animation.
  - *Animate the appearance of a new record in the table

  **Endpoints:**

  - `POST /api/expenses` - Add a new expense.

  **Technology-related requirements:**

  <details>
  <summary>React</summary>

  - Use controlled components for form handling.
  - Validate form inputs with `yup`.
  - Use `react-hook-form` for work with forms.
  </details>

  <br />

  **Materials:**

  - [Client-side form validation](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation)
---

</details>


<details>
  <summary>Task 23: Add Update and Delete Expense Features</summary>

  ---

  **Description:**

  Implement functionality to update or delete an expense from the table.

  **Acceptance Criteria:**

  - An "Edit" button allows modification of expense details.
  - A "Delete" button removes the expense from the list and updates the backend. Use modal for confirming deletion.
  - In the mobile version there is no menu button, so when user click on a row, display a modal window with an Edit and Delete buttons.
  - *Animate deleting a table record.
  - *When the user clicks outside the modal window or presses the esc key, the component should close.
  - *Animate the appearance and disappearance of a modal window.
  - *Handle optimistic updates for better user experience.

  **Endpoints:**

  - `PATCH /api/expenses/:id` - Update an expense.
  - `DELETE /api/expenses/:id` - Delete an expense.

  **Materials:**

  - [What is Optimistic UI?](https://javascript.plainenglish.io/what-is-optimistic-ui-656b9d6e187c)

---

</details>


<details>
  <summary>Task 24: Final step</summary>

  ---

  - Open a pull request for the `master` branch and send the solution to the code review

  ---

</details>

## Solution
If you've already finished working on this part or are stuck, these repositories might be useful to you.
  - [API](https://github.com/petproject-dev/expense-tracker-backend-part-2) - Express.js
  - [UI](https://github.com/petproject-dev/expense-tracker-frontend-part-2) - React

## Next Steps
If you're ready to move forward, you can proceed to [next project part](../part-2/README.md).

## Found an Issue?
We strive to make the project as clear and helpful as possible. If you notice any errors, inconsistencies, or unclear instructions, please open a Pull Request in this repository with your suggested fixes or improvements. Your feedback helps improve the learning experience for everyone!

Happy coding, and good luck with this part of the project!
