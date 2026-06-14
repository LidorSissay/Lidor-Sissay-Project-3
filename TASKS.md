# TASKS.md — Vacation Project

> עבודה לפי משימות קטנות, חד־משמעיות וניתנות לבדיקה.  
> אין לדלג יותר מ־2–3 משימות בלי commit.

---

## Phase 0 — Project Setup

### Task 0.1 — Create root project folders
**Goal:** Create the required submission structure.

**Steps:**
- Create root folder with the student full name in English.
- Inside it create:
  - `Database/`
  - `Backend/`
  - `Frontend/`

**Success criteria:**
- The project contains exactly these three main folders.
- The folder names use capital letters as required.

**Commit:** Yes  
**Commit message:** `chore: create project folder structure`

---

### Task 0.2 — Initialize Git repository
**Goal:** Track the project with Git.

**Steps:**
- Initialize Git in the root project folder.
- Add `.gitignore` files for backend and frontend.
- Ensure `node_modules` will not be committed.

**Success criteria:**
- `git status` works from the project root.
- `node_modules` is ignored.

**Commit:** Yes  
**Commit message:** `chore: initialize git repository`

---

## Phase 1 — Database Planning and Seed

### Task 1.1 — Choose database engine
**Goal:** Decide the database for the project.

**Decision:** Use MySQL.

**Success criteria:**
- README or notes mention MySQL as the selected database.

**Commit:** No

---

### Task 1.2 — Define database tables
**Goal:** Plan the database schema before coding.

**Tables:**
- `users`
- `vacations`
- `likes`

**Success criteria:**
- Each table has a clear list of columns.
- Relationships are clear:
  - user can like many vacations
  - vacation can have many likes

**Commit:** Yes  
**Commit message:** `docs: define database schema`

---

### Task 1.3 — Define users table
**Goal:** Specify the users table.

**Columns:**
- `id`
- `firstName`
- `lastName`
- `email`
- `password`
- `role`

**Rules:**
- `email` must be unique.
- `role` must be enum: `User`, `Admin`.

**Success criteria:**
- Schema includes unique email.
- Schema includes enum role.

**Commit:** No

---

### Task 1.4 — Define vacations table
**Goal:** Specify the vacations table.

**Columns:**
- `id`
- `destination`
- `description`
- `startDate`
- `endDate`
- `price`
- `imageName`

**Rules:**
- Price must not be negative.
- Price must not be greater than 10,000.
- End date must not be earlier than start date.

**Success criteria:**
- Schema contains all required vacation fields.
- Image is stored as filename only.

**Commit:** No

---

### Task 1.5 — Define likes table
**Goal:** Specify the likes relation table.

**Columns:**
- `userId`
- `vacationId`

**Rules:**
- A user can like the same vacation only once.
- Deleting a user or vacation should delete related likes.

**Success criteria:**
- Composite uniqueness is planned for `userId + vacationId`.

**Commit:** Yes  
**Commit message:** `docs: add vacation likes schema`

---

### Task 1.6 — Prepare seed data plan
**Goal:** Plan initial database data.

**Data required:**
- At least 12 vacations with realistic data.
- At least one admin user.
- Optional regular user.

**Success criteria:**
- Admin email and password are documented for README.
- 12 vacation destinations are selected.

**Commit:** No

---

## Phase 2 — Backend Skeleton

### Task 2.1 — Create Backend TypeScript project
**Goal:** Initialize backend project.

**Steps:**
- Create Node.js project inside `Backend/`.
- Configure TypeScript.
- Add dev script.

**Success criteria:**
- Backend starts with a basic TypeScript entry file.
- TypeScript compilation works.

**Commit:** Yes  
**Commit message:** `chore: initialize backend typescript project`

---

### Task 2.2 — Install backend dependencies
**Goal:** Add backend packages.

**Packages:**
- Express
- TypeScript support
- Sequelize
- MySQL driver
- Joi
- JWT package
- CORS
- config package

**Success criteria:**
- `package.json` contains required backend dependencies.
- Project still starts successfully.

**Commit:** No

---

### Task 2.3 — Create backend folder structure
**Goal:** Match the lecturer style.

**Folders:**
- `src/routers/`
- `src/controllers/`
- `src/models/`
- `src/middlewares/`
- `src/db/`
- `config/`

**Success criteria:**
- Backend structure is domain-ready.
- No business code is added yet.

**Commit:** Yes  
**Commit message:** `chore: add backend folder structure`

---

### Task 2.4 — Configure backend app bootstrap
**Goal:** Prepare the main Express app.

**Requirements:**
- Express app exists.
- CORS enabled.
- JSON body parser enabled.
- Not found middleware planned.
- Error middleware planned.

**Success criteria:**
- Backend runs and responds to a health route or basic route.

**Commit:** No

---

### Task 2.5 — Configure backend config files
**Goal:** Add environment-based configuration.

**Files:**
- `default.json`
- `development.json`
- `compose.json`
- `custom-environment-variables.json`

**Success criteria:**
- Port, database credentials, JWT key and sync setting are configurable.

**Commit:** Yes  
**Commit message:** `chore: add backend configuration files`

---

## Phase 3 — Backend Database Layer

### Task 3.1 — Create Sequelize connection
**Goal:** Connect backend to MySQL.

**Success criteria:**
- Backend logs successful database connection.
- Failed connection shows a clear error.

**Commit:** Yes  
**Commit message:** `feat: add sequelize database connection`

---

### Task 3.2 — Create User model
**Goal:** Add Sequelize model for users.

**Fields:**
- id
- firstName
- lastName
- email
- password
- role

**Success criteria:**
- Sequelize can sync the users table.
- Role is represented as enum.
- Email is unique.

**Commit:** No

---

### Task 3.3 — Create Vacation model
**Goal:** Add Sequelize model for vacations.

**Fields:**
- id
- destination
- description
- startDate
- endDate
- price
- imageName

**Success criteria:**
- Sequelize can sync the vacations table.
- Model field names are clear and consistent.

**Commit:** No

---

### Task 3.4 — Create Like model
**Goal:** Add Sequelize model for likes.

**Fields:**
- userId
- vacationId

**Success criteria:**
- Sequelize can sync the likes table.
- Associations between users, vacations and likes are defined.

**Commit:** Yes  
**Commit message:** `feat: add sequelize models`

---

### Task 3.5 — Register all models in Sequelize
**Goal:** Make all models active.

**Success criteria:**
- Backend startup creates or syncs all three tables.
- No model association errors appear.

**Commit:** No

---

## Phase 4 — Backend Middlewares

### Task 4.1 — Create body validation middleware
**Goal:** Validate request bodies with Joi.

**Success criteria:**
- Invalid body returns status 422.
- Error message is clear text.

**Commit:** No

---

### Task 4.2 — Create params validation middleware
**Goal:** Validate route parameters with Joi.

**Success criteria:**
- Invalid params return status 422.
- Valid params pass to controller.

**Commit:** No

---

### Task 4.3 — Create auth enforcement middleware
**Goal:** Protect private routes.

**Success criteria:**
- Request without token gets 401.
- Request with valid token reaches the next handler.
- User id and role are available to controllers.

**Commit:** Yes  
**Commit message:** `feat: add validation and auth middlewares`

---

### Task 4.4 — Create admin-only middleware
**Goal:** Protect admin routes.

**Success criteria:**
- Regular user receives 403 on admin routes.
- Admin user can access admin routes.

**Commit:** No

---

### Task 4.5 — Create error handling middlewares
**Goal:** Handle errors consistently.

**Requirements:**
- Not found middleware.
- Log error middleware.
- Error responder middleware.

**Success criteria:**
- Unknown route returns 404.
- Server errors return readable text.
- Frontend will not receive raw technical error objects.

**Commit:** Yes  
**Commit message:** `feat: add backend error handling`

---

## Phase 5 — Authentication API

### Task 5.1 — Create auth validators
**Goal:** Validate register and login inputs.

**Rules:**
- All fields required.
- Email must be valid.
- Password minimum length: 4.

**Success criteria:**
- Invalid auth requests return 422.

**Commit:** No

---

### Task 5.2 — Create register endpoint
**Goal:** Allow new users to register.

**Route:**
- `POST /auth/register`

**Success criteria:**
- New user is created.
- Duplicate email returns friendly error.
- Successful response returns JWT or user session data.

**Commit:** No

---

### Task 5.3 — Create login endpoint
**Goal:** Allow registered users to login.

**Route:**
- `POST /auth/login`

**Success criteria:**
- Correct credentials return JWT.
- Wrong credentials return friendly error.

**Commit:** Yes  
**Commit message:** `feat: add authentication api`

---

### Task 5.4 — Test auth endpoints in Postman
**Goal:** Verify auth manually.

**Tests:**
- Register valid user.
- Register duplicate email.
- Login valid user.
- Login wrong password.

**Success criteria:**
- All auth cases behave as expected.

**Commit:** No

---

## Phase 6 — Vacations API

### Task 6.1 — Create vacations validators
**Goal:** Validate vacation inputs.

**Rules:**
- Destination required.
- Description required.
- Dates required.
- Price between 0 and 10,000.
- Image required on create.
- Image optional on update.

**Success criteria:**
- Invalid vacation data returns 422.

**Commit:** No

---

### Task 6.2 — Create get vacations endpoint
**Goal:** Return vacations for logged-in users.

**Route:**
- `GET /vacations`

**Requirements:**
- Sorted by start date ascending.
- Include like count.
- Include whether current user liked each vacation.

**Success criteria:**
- Logged-in user receives vacations with like metadata.

**Commit:** No

---

### Task 6.3 — Add pagination support
**Goal:** Limit vacations per page.

**Rules:**
- 9 vacations per page.
- Use limit and offset.

**Success criteria:**
- Page 1 returns at most 9 vacations.
- Page 2 returns next vacations.

**Commit:** Yes  
**Commit message:** `feat: add vacations listing with pagination`

---

### Task 6.4 — Add vacation filters
**Goal:** Support single active filter.

**Filters:**
- all
- liked
- active
- future

**Success criteria:**
- Only one filter affects results at a time.
- Each filter returns correct vacations.

**Commit:** No

---

### Task 6.5 — Create single vacation endpoint
**Goal:** Fetch one vacation by id.

**Route:**
- `GET /vacations/:vacationId`

**Success criteria:**
- Existing vacation returns data.
- Missing vacation returns 404.

**Commit:** No

---

### Task 6.6 — Create add vacation endpoint
**Goal:** Admin can add vacation.

**Route:**
- `POST /vacations`

**Success criteria:**
- Admin creates vacation successfully.
- Regular user cannot create vacation.
- Past start dates are rejected.

**Commit:** Yes  
**Commit message:** `feat: add vacation filtering and creation`

---

### Task 6.7 — Create update vacation endpoint
**Goal:** Admin can update vacation.

**Route:**
- `PATCH /vacations/:vacationId`

**Rules:**
- Image optional.
- Past dates allowed on edit.

**Success criteria:**
- Existing vacation is updated.
- Missing vacation returns 404.
- Regular user cannot update.

**Commit:** No

---

### Task 6.8 — Create delete vacation endpoint
**Goal:** Admin can delete vacation.

**Route:**
- `DELETE /vacations/:vacationId`

**Success criteria:**
- Existing vacation is deleted.
- Related likes are deleted.
- Missing vacation returns 404.
- Regular user cannot delete.

**Commit:** Yes  
**Commit message:** `feat: add vacation update and delete`

---

## Phase 7 — Image Upload API

### Task 7.1 — Add image upload middleware
**Goal:** Support vacation image upload.

**Success criteria:**
- Uploaded image is saved in backend folder.
- Database stores only image filename.

**Commit:** No

---

### Task 7.2 — Serve vacation images statically
**Goal:** Allow frontend to display images.

**Success criteria:**
- Image URL opens in browser.
- Vacation card can use this URL.

**Commit:** Yes  
**Commit message:** `feat: add vacation image upload support`

---

## Phase 8 — Likes API

### Task 8.1 — Create add like endpoint
**Goal:** User can like a vacation.

**Route:**
- `POST /likes/:vacationId`

**Success criteria:**
- Like is created.
- Duplicate like is prevented.
- Admin cannot like.

**Commit:** No

---

### Task 8.2 — Create remove like endpoint
**Goal:** User can remove own like.

**Route:**
- `DELETE /likes/:vacationId`

**Success criteria:**
- Existing like is removed.
- Removing missing like does not crash.
- Admin cannot unlike.

**Commit:** Yes  
**Commit message:** `feat: add vacation likes api`

---

## Phase 9 — Reports and CSV API

### Task 9.1 — Create likes report endpoint
**Goal:** Admin can get likes count per vacation.

**Route:**
- `GET /reports/likes`

**Success criteria:**
- Admin receives destination and likes count.
- Regular user cannot access.

**Commit:** No

---

### Task 9.2 — Create CSV export endpoint
**Goal:** Admin can download vacation likes CSV.

**Route:**
- `GET /reports/likes/csv`

**Success criteria:**
- Response downloads CSV file.
- CSV contains `Destination,Likes` header.
- Regular user cannot access.

**Commit:** Yes  
**Commit message:** `feat: add reports and csv export api`

---

## Phase 10 — AI Recommendation API

### Task 10.1 — Add AI configuration
**Goal:** Configure LLM API key through environment variable.

**Success criteria:**
- Backend reads API key from environment.
- README explains how to provide the variable.

**Commit:** No

---

### Task 10.2 — Create AI recommendation endpoint
**Goal:** Return trip recommendation for selected vacation destination.

**Route:**
- `POST /ai/recommendation`

**Input:**
- vacation id or destination

**Success criteria:**
- Logged-in user receives readable recommendation.
- Missing API key returns clear friendly error.

**Commit:** Yes  
**Commit message:** `feat: add ai recommendation api`

---

## Phase 11 — MCP Server

### Task 11.1 — Create MCP project skeleton
**Goal:** Add MCP service folder.

**Location:**
- `MCP/` or `mcp/`

**Success criteria:**
- MCP service has its own package file and TypeScript setup.

**Commit:** No

---

### Task 11.2 — Connect MCP service to backend
**Goal:** Allow MCP to query backend data.

**Success criteria:**
- MCP can call backend endpoints.
- JWT is forwarded when needed.

**Commit:** No

---

### Task 11.3 — Add MCP question endpoint/tool
**Goal:** Support questions about database data.

**Example questions:**
- How many active vacations exist?
- What is the average vacation price?
- Which future vacations exist in Europe?

**Success criteria:**
- User can ask database-related question.
- Response is clear and based on database data.

**Commit:** Yes  
**Commit message:** `feat: add mcp database question service`

---

## Phase 12 — Frontend Skeleton

### Task 12.1 — Create React TypeScript project
**Goal:** Initialize frontend project.

**Success criteria:**
- Frontend starts with Vite.
- TypeScript works.

**Commit:** Yes  
**Commit message:** `chore: initialize frontend react project`

---

### Task 12.2 — Create frontend folder structure
**Goal:** Match project architecture.

**Folders:**
- `components/`
- `models/`
- `services/`
- `hooks/`
- `utils/`

**Success criteria:**
- Structure exists and is ready for features.

**Commit:** No

---

### Task 12.3 — Create layout components
**Goal:** Build app shell.

**Components:**
- App
- Layout
- Header
- Main
- Footer
- NotFound

**Success criteria:**
- App displays header, main and footer.
- Unknown route displays NotFound.

**Commit:** Yes  
**Commit message:** `feat: add frontend layout shell`

---

### Task 12.4 — Add frontend environment configuration
**Goal:** Configure backend URL.

**Files:**
- `.env.development`
- `.env.docker`

**Success criteria:**
- Frontend can read backend base URL from `VITE_` variable.

**Commit:** No

---

## Phase 13 — Frontend Auth

### Task 13.1 — Create frontend auth models
**Goal:** Define auth TypeScript models.

**Models:**
- User
- Credentials
- RegisterData
- JwtData or AuthUser

**Success criteria:**
- Auth components and services can import models.

**Commit:** No

---

### Task 13.2 — Create auth service
**Goal:** Connect frontend to auth API.

**Methods:**
- register
- login

**Success criteria:**
- Service can call backend auth endpoints.

**Commit:** No

---

### Task 13.3 — Create auth context
**Goal:** Store logged-in user state.

**Requirements:**
- Save JWT.
- Load JWT from localStorage.
- Logout clears JWT.

**Success criteria:**
- Refresh keeps user logged in.
- Logout clears session.

**Commit:** Yes  
**Commit message:** `feat: add frontend auth state`

---

### Task 13.4 — Create Login page
**Goal:** Allow existing users to login.

**Success criteria:**
- Required validation works.
- Invalid login shows friendly error.
- Successful login redirects to vacations page.

**Commit:** No

---

### Task 13.5 — Create Register page
**Goal:** Allow new users to register.

**Success criteria:**
- Required validation works.
- Invalid email is blocked.
- Password shorter than 4 is blocked.
- Duplicate email shows friendly error.
- Successful registration redirects to vacations page.

**Commit:** Yes  
**Commit message:** `feat: add login and register pages`

---

## Phase 14 — Frontend Routing and Navigation

### Task 14.1 — Create role-based menu
**Goal:** Show menu according to auth state and role.

**Rules:**
- Guest sees Login and Register.
- User sees Vacations, AI, MCP and Logout.
- Admin sees Admin Vacations, Reports, AI, MCP and Logout.

**Success criteria:**
- Menu changes correctly after login/logout.
- Full user name is displayed when logged in.

**Commit:** No

---

### Task 14.2 — Protect private frontend pages
**Goal:** Prevent guests from private pages.

**Success criteria:**
- Guest entering vacations route is redirected to login.
- Logged-in user can access vacations.

**Commit:** No

---

### Task 14.3 — Protect admin frontend pages
**Goal:** Prevent users from admin pages.

**Success criteria:**
- Regular user cannot access admin pages.
- Admin can access admin pages.

**Commit:** Yes  
**Commit message:** `feat: add role based navigation and guards`

---

## Phase 15 — Frontend Vacations

### Task 15.1 — Create vacation model
**Goal:** Define frontend vacation type.

**Fields:**
- id
- destination
- description
- startDate
- endDate
- price
- imageName
- likesCount
- isLiked

**Success criteria:**
- Vacation API response has matching frontend type.

**Commit:** No

---

### Task 15.2 — Create vacations service
**Goal:** Connect frontend to vacations API.

**Methods:**
- getVacations
- getVacation
- addVacation
- updateVacation
- deleteVacation

**Success criteria:**
- Service methods call correct backend routes.

**Commit:** No

---

### Task 15.3 — Create vacation card component
**Goal:** Display a single vacation.

**Requirements:**
- Image
- Destination
- Dates
- Description
- Price
- Likes count
- Like state for user

**Success criteria:**
- Card displays all required vacation data.

**Commit:** Yes  
**Commit message:** `feat: add vacation card component`

---

### Task 15.4 — Create vacations page
**Goal:** Display vacations list.

**Success criteria:**
- Logged-in user sees vacation cards.
- Vacations are sorted by start date.
- Loading and error states exist.

**Commit:** No

---

### Task 15.5 — Add pagination UI
**Goal:** Show 9 vacations per page.

**Success criteria:**
- Page buttons change visible vacations.
- Current page is clear to the user.

**Commit:** No

---

### Task 15.6 — Add filters UI
**Goal:** Allow single active filter.

**Filters:**
- All
- Liked
- Active
- Future

**Success criteria:**
- Clicking one filter cancels previous filter.
- Results update correctly.

**Commit:** Yes  
**Commit message:** `feat: add vacations page pagination and filters`

---

### Task 15.7 — Add like/unlike behavior
**Goal:** User can toggle like.

**Success criteria:**
- Like button creates like.
- Unlike removes like.
- Likes count updates.
- Admin does not see like buttons.

**Commit:** Yes  
**Commit message:** `feat: add vacation like interactions`

---

## Phase 16 — Frontend Admin Vacations

### Task 16.1 — Create admin vacations page
**Goal:** Display vacation cards for admin.

**Requirements:**
- Add button at top.
- Edit button on every card.
- Delete button on every card.
- No like buttons.

**Success criteria:**
- Admin sees management actions.
- Regular user cannot access.

**Commit:** No

---

### Task 16.2 — Create add vacation page
**Goal:** Admin can add vacation from UI.

**Success criteria:**
- All fields required.
- Price validation works.
- Past date is blocked.
- End date before start date is blocked.
- Image is required.
- Successful add redirects to admin vacations.

**Commit:** Yes  
**Commit message:** `feat: add admin vacation creation page`

---

### Task 16.3 — Create edit vacation page
**Goal:** Admin can edit vacation from UI.

**Success criteria:**
- Existing vacation data loads into form.
- Image is shown but not required.
- Price validation works.
- End date before start date is blocked.
- Past dates are allowed.
- Successful update redirects to admin vacations.

**Commit:** No

---

### Task 16.4 — Add delete confirmation
**Goal:** Prevent accidental vacation deletion.

**Success criteria:**
- Delete asks for confirmation.
- Cancel does not delete.
- Confirm deletes and refreshes list.

**Commit:** Yes  
**Commit message:** `feat: add admin vacation editing and deletion`

---

## Phase 17 — Frontend Reports and CSV

### Task 17.1 — Create reports service
**Goal:** Connect frontend to reports API.

**Methods:**
- getLikesReport
- downloadLikesCsv

**Success criteria:**
- Admin can request report data.

**Commit:** No

---

### Task 17.2 — Create reports page with chart
**Goal:** Display likes per vacation.

**Requirements:**
- X axis: destination.
- Y axis: likes count.

**Success criteria:**
- Chart displays correct report data.
- Admin only.

**Commit:** No

---

### Task 17.3 — Add CSV download button
**Goal:** Admin can download report CSV.

**Success criteria:**
- Clicking button downloads CSV file.
- CSV opens correctly in Excel.

**Commit:** Yes  
**Commit message:** `feat: add reports chart and csv download`

---

## Phase 18 — Frontend AI Recommendation

### Task 18.1 — Create AI service
**Goal:** Connect frontend to AI endpoint.

**Success criteria:**
- Service sends selected vacation or destination to backend.

**Commit:** No

---

### Task 18.2 — Create AI recommendation page
**Goal:** User can request trip recommendation.

**Requirements:**
- Select destination from existing vacations.
- Show recommendation on page.
- Show loading state.

**Success criteria:**
- Logged-in user gets recommendation.
- Friendly error appears if AI request fails.

**Commit:** Yes  
**Commit message:** `feat: add ai recommendation page`

---

## Phase 19 — Frontend MCP Page

### Task 19.1 — Create MCP service
**Goal:** Connect frontend to MCP/backend question endpoint.

**Success criteria:**
- Service can send question text.

**Commit:** No

---

### Task 19.2 — Create MCP page
**Goal:** User can ask questions about database data.

**Requirements:**
- Text input.
- Submit button.
- Response display.
- Loading state.

**Success criteria:**
- Logged-in user can ask a database-related question.
- Response is displayed clearly.

**Commit:** Yes  
**Commit message:** `feat: add mcp question page`

---

## Phase 20 — Docker

### Task 20.1 — Create database Docker setup
**Goal:** Run MySQL in Docker.

**Requirements:**
- Database container starts.
- Seed SQL can initialize database.

**Success criteria:**
- MySQL container is healthy.
- Database contains required tables and seed data.

**Commit:** No

---

### Task 20.2 — Create backend Dockerfile
**Goal:** Run backend in Docker.

**Success criteria:**
- Backend image builds successfully.
- Backend container connects to database container.

**Commit:** No

---

### Task 20.3 — Create frontend Dockerfile
**Goal:** Run frontend in Docker.

**Success criteria:**
- Frontend image builds successfully.
- Frontend is served through nginx or equivalent.

**Commit:** No

---

### Task 20.4 — Create docker-compose file
**Goal:** Run full system with one command.

**Command:**
- `docker compose up --build`

**Success criteria:**
- Database, backend and frontend start together.
- Frontend can call backend.
- Backend can call database.

**Commit:** Yes  
**Commit message:** `chore: add docker compose setup`

---

### Task 20.5 — Add AI environment variable to compose docs
**Goal:** Explain how to run compose with LLM API key.

**Success criteria:**
- README includes clear example for passing the AI key.

**Commit:** No

---

## Phase 21 — Postman

### Task 21.1 — Create Postman collection
**Goal:** Document and test backend API.

**Required groups:**
- Auth
- Vacations
- Likes
- Reports
- AI
- MCP

**Success criteria:**
- Every backend endpoint has a Postman request.

**Commit:** No

---

### Task 21.2 — Export Postman collection
**Goal:** Prepare required submission artifact.

**Location:**
- Save exported collection inside `Backend/`.

**Success criteria:**
- Postman JSON file exists in backend folder.

**Commit:** Yes  
**Commit message:** `docs: add postman collection`

---

## Phase 22 — README and Submission

### Task 22.1 — Create root README
**Goal:** Explain project clearly.

**Must include:**
- Project description.
- Technologies.
- How to run locally.
- How to run with Docker.
- Admin email and password.
- AI environment variable example.
- GitHub link.

**Success criteria:**
- README is readable and formatted in Markdown.

**Commit:** No

---

### Task 22.2 — Verify seed SQL export
**Goal:** Ensure database submission is complete.

**Location:**
- `Database/`

**Success criteria:**
- SQL file contains schema and seed data.
- SQL includes admin user.
- SQL includes at least 12 vacations.

**Commit:** No

---

### Task 22.3 — Final manual test
**Goal:** Verify the entire system before submission.

**Checklist:**
- Register works.
- Login works.
- User vacations page works.
- Likes work.
- Filters work.
- Pagination works.
- Admin CRUD works.
- Reports work.
- CSV downloads.
- AI works or shows friendly config error.
- MCP works.
- Docker compose works.

**Success criteria:**
- No critical feature is broken.

**Commit:** Yes  
**Commit message:** `test: verify full project flow`

---

### Task 22.4 — Clean project before zip
**Goal:** Prepare final submission folder.

**Steps:**
- Delete backend `node_modules`.
- Delete frontend `node_modules`.
- Keep source files.
- Keep SQL export.
- Keep Postman export.
- Keep README.

**Success criteria:**
- No `node_modules` folders exist.
- Required folders remain intact.

**Commit:** No

---

### Task 22.5 — Create final zip
**Goal:** Prepare upload file.

**Success criteria:**
- One zip file contains the root project folder.
- Zip contains `Database`, `Backend`, `Frontend`.

**Commit:** No

---

## Commit Rule Reminder

Do not complete more than 2–3 tasks without a commit.  
Prefer committing after each completed feature slice or infrastructure milestone.
