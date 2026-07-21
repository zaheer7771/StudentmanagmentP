# School Management System

A full-featured **School Management System** built with **ASP.NET Core 8 MVC**, **Entity Framework Core**, and **SQL Server**, using **ASP.NET Core Identity** for role-based authentication (Admin / Teacher / Student).

## Features

- **Role-based access control** — Admin, Teacher, and Student roles with distinct dashboards and permissions
- **Student management** — full CRUD with class assignment, search
- **Teacher management** — full CRUD, subject and class-teacher assignment
- **Class management** — sections/grades with an assigned class teacher and roster
- **Subject management** — linked to a teacher and a class
- **Enrollments** — enroll students into subjects with duplicate-enrollment protection
- **Attendance** — mark attendance per class/date in bulk, filter and review history, live attendance %
- **Exam results** — record marks per subject/exam with automatic letter-grade calculation
- **Admin dashboard** — student/teacher/class counts, today's attendance %, students-per-class breakdown
- **Student/Teacher personal dashboards** — students see their own results & attendance; teachers see their subjects and classes led

## Tech Stack

- ASP.NET Core 8 MVC (C#)
- Entity Framework Core 8 (Code-First)
- SQL Server / LocalDB
- ASP.NET Core Identity
- Bootstrap 5 (via CDN)

## Project Structure

```
SchoolManagementSystem/
├── Controllers/       # MVC controllers (Students, Teachers, Classes, Subjects, Attendance, ExamResults, Enrollments, Account, Dashboard)
├── Models/             # EF Core entities + ApplicationUser (extends IdentityUser)
├── ViewModels/          # Login, Register, Dashboard view models
├── Data/                # ApplicationDbContext + DbInitializer (role/admin seeding)
├── Views/               # Razor views (Bootstrap-styled)
└── wwwroot/             # Static assets (site.css)
```

## Getting Started

### Prerequisites
- [.NET 8 SDK](https://dotnet.microsoft.com/download)
- SQL Server (LocalDB, Express, or full) — LocalDB ships with Visual Studio

### 1. Restore packages
```bash
cd SchoolManagementSystem
dotnet restore
```

### 2. Configure the connection string
Edit `appsettings.json` if you're not using LocalDB:
```json
"ConnectionStrings": {
  "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=SchoolManagementDb;Trusted_Connection=True;MultipleActiveResultSets=true;TrustServerCertificate=True"
}
```

### 3. Create the database
```bash
dotnet tool install --global dotnet-ef   # if not already installed
dotnet ef migrations add InitialCreate
dotnet ef database update
```

### 4. Run the app
```bash
dotnet run
```
Navigate to `https://localhost:{port}`.

### 5. Log in
A default Admin account is seeded automatically on first run:
- **Email:** `admin@school.local`
- **Password:** `Admin@12345`

> Change this password immediately in any real deployment. Use **New Account** (Admin nav menu) to create Teacher and Student logins, optionally linked to an existing Teacher/Student record.

## Notes for Resume / Portfolio

This project demonstrates:
- Clean N-tier structure (Models / Data / Controllers / Views)
- Code-First EF Core with Fluent API relationship configuration (1-to-many, many-to-many via join entity, cascade/restrict delete rules, unique indexes)
- ASP.NET Core Identity integration with custom user fields and role-based authorization (`[Authorize(Roles = "...")]`)
- Server-side validation with Data Annotations
- Practical UI/UX: search/filter, bulk attendance entry, computed grade logic

## License
Free to use for personal portfolio and learning purposes.
