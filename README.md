# Employee Leave Management System (Front‑End Demo)

A basic **Employee Leave Management System** for a small company (around 50 employees) built with **HTML, CSS, and JavaScript**.  
All logic runs in the browser using `localStorage` to simulate a backend.  
An optional **MySQL setup script** is provided separately for real employee credentials, but it is **not wired into the front‑end**.

---

## Features

- **User Authentication (Front‑End Demo Only)**
  - Demo users (employees & managers) seeded in the browser using JavaScript.
  - Simple login form, role-based dashboards (employee vs manager).
  - Logout button returns to the login screen.

- **Leave Request Submission (Employees)**
  - Form fields: leave type, start date, end date, reason.
  - Validation:
    - All fields must be filled.
    - End date cannot be before start date.
    - Start date cannot be in the past.
  - Requests are stored in `localStorage` with status `pending`.

- **Leave Approval Workflow (Managers)**
  - Managers see a list of **pending requests** routed to them.
  - Can **approve** or **reject** requests and add optional comments.
  - Leave balances are automatically reduced when a request is approved (except `unpaid` type).

- **Leave Balances**
  - Each user has balances for `vacation`, `sick`, `unpaid`, `other`.
  - Balances are shown as badges on the employee dashboard.
  - On approval, corresponding balance is decreased.

- **Leave Calendar**
  - Employee view: calendar showing **pending + approved** requests across the team.
  - Manager view: calendar showing **approved** requests for that manager.
  - Month navigation (previous/next) for both calendars, with today's date highlighted.

- **Employee Analytics Dashboard**
  - Animated mini-charts (pure CSS/JS) for:
    - **% utilization of leave quota** per leave type and overall.
    - **Most popular leave months** (top months by approved leave days).
    - **Absenteeism trend** (last 6 months of approved leave days).
  - Smooth card entrance animations and hover effects for a more engaging UI.

- **Manager Analytics (Chart.js)**
  - Separate **Analytics** tab on the manager dashboard (Overview + Analytics tabs).
  - Uses **Chart.js** (via CDN, no build step) to render:
    - Doughnut chart of **leave by type** across the manager's team.
    - Bar chart of **most popular months** by approved leave days.
    - Line chart for **absenteeism trend** over the last 6 months.
  - Manager-level aggregates are **pre‑computed and cached** in `localStorage` whenever:
    - A manager logs in.
    - A request is approved or rejected.

- **Code Organization**
  - `index.html` – structure, layout, and manager tabs.
  - `styles.css` – styling, responsive design, animations, and chart-related styles.
  - `app.js` – business logic, routing, analytics, aggregates, and `localStorage` data handling.
  - `mysql_setup.sql` – optional MySQL database script (not connected to the front‑end).

---

## Technology Stack

- **Front‑end**: HTML5, CSS3, Vanilla JavaScript (no frameworks).
- **State & persistence**: Browser `localStorage`.
- **Optional backend data**: MySQL (only via `mysql_setup.sql`, not connected in this demo).

---

## Project Structure

```text
f:\Leave M System\
  ├─ index.html        # Main HTML entry point
  ├─ styles.css        # Global styles
  ├─ app.js            # Front-end logic (auth, leave, calendar)
  └─ mysql_setup.sql   # Optional MySQL DB + 50 seeded employees
```

---

## Running the Front‑End Demo

1. **Clone or copy** this folder to your machine.
2. Open `index.html` directly in a modern browser:
   - On Windows you can double-click `index.html`, or
   - Serve it with any static server (e.g., VS Code Live Server).
3. Use one of the **demo accounts**:

   - Employees:
     - `alice / password123`
     - `bob / password123`
     - `charlie / password123`
   - Managers:
     - `manager1 / password123`
     - `manager2 / password123`

> Note: These demo accounts are stored in `localStorage` and are **not related** to the MySQL data.

---

## Optional: MySQL Employee Table (Not Wired to UI)

The file `mysql_setup.sql` contains:

- Database creation for `leave_management_demo`.
- `employees` table with:
  - `employee_code` (e.g., `E001`–`E050`),
  - `full_name`,
  - `role` (`employee` / `manager`),
  - `password_hash` (SHA2-256 hash of `"password123"`).
- Inserts for **50 employee records**.

### How to use the SQL script

1. Open **MySQL Workbench** (or any client).
2. Load `mysql_setup.sql`.
3. Execute the script to create the database and seed employees.

This script is meant for:

- Experimenting with a real database of 50 employees.
- Later connecting a proper backend (Node.js, PHP, etc.) to this UI.

The current project **does not** include backend code or an API call from `app.js` to MySQL.

---

## Possible Next Steps (If You Add a Backend)

- Replace the in-browser `localStorage` logic with real REST API calls:
  - `/login` – validate username/password from MySQL.
  - `/leave-requests` – create, list, and update requests.
  - `/balances` – fetch and update leave balances.
  - `/calendar` – return aggregated leave data.
- Connect to MySQL using the database created from `mysql_setup.sql`.
- Implement proper password hashing & verification on the server side.

---

## Disclaimer

This project is intended as a **learning/demo application**:

- Authentication is **not secure** (pure front‑end with demo users).
- No real server-side validation or authorization is implemented.
- Do **not** use this as-is in production without a proper backend and security hardening.

