# Learning Management System (LMS) Project

This project is a simple Learning Management System (LMS) module built as part of a MERN Stack Development Intern assignment. The application features separate Admin and User views, enabling course management and enrollment functionality.

---

## Project Overview

This repository serves as a central reference for both the frontend and backend applications of the LMS module. The project is divided into two separate repositories:

- **Frontend Repository**: Built using Next.js, TypeScript, and Tailwind CSS.
  - [Frontend GitHub Repository](https://github.com/hritikkkkk/LMS-CLIENT)
  - [Deployed Frontend Application](https://lms-client-orpin-phi.vercel.app/)

- **Backend Repository**: Built using Node.js, Express.js, and MongoDB.
  - [Backend GitHub Repository](https://github.com/hritikkkkk/LMS-SERVER)
  - [Deployed Backend API](https://lms-server-x7wd.onrender.com/admin/courses)

---

## Features

### Admin View:
1. **Dashboard**:
   - Displays all courses with options to add, edit, or delete them.
2. **Add/Edit Course Page**:
   - A form to add or update course details such as Title, Description, Duration, and Instructor Name.

### User View:
1. **Course Catalog**:
   - Displays all available courses with search and filter options (by Title, Duration, or Instructor).
2. **Course Details Page**:
   - Displays detailed information about a selected course and includes an "Enroll" button.
3. **My Enrolled Courses Page**:
   - Displays a list of courses the user has enrolled in.

---

## Tech Stack

### Frontend:
- **Framework**: Next.js
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **API Integration**: Axios

### Backend:
- **Server Framework**: Express.js
- **Database**: MongoDB (using Mongoose ODM)
- **Authentication**: JWT-based authentication

---

## Predefined Admin and User Credentials:

- **Admin:**
  - userId: `hritikk.7827`

- **User:**
  - userId: *Type any username. A new user is created automatically.*

---



---

## Setting Up the Application

### Frontend Setup

1. Clone the frontend repository:
   ```bash
   git clone https://github.com/hritikkkkk/LMS-CLIENT
   cd LMS-CLIENT
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Configure the API base URL in `.env.local`:
   ```env
   NEXT_PUBLIC_API_URL=https://lms-server-x7wd.onrender.com
   ```
4. Start the development server:
   ```bash
   npm run dev
   ```
5. Access the application at `http://localhost:3000`.

### Backend Setup

1. Clone the backend repository:
   ```bash
   git clone https://github.com/hritikkkkk/LMS-SERVER
   cd LMS-SERVER
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Configure environment variables in `.env`:
   ```env
   PORT=5000
   MONGO_URI=your-mongodb-connection-string
   JWT_SECRET=your-secret-key
   JWT_EXPIRY =jwt-expiry
   ```
4. Start the server:
   ```bash
   npm run start
   ```
5. The API will run on `http://localhost:5000`.

---

## Database Schema

### Courses Collection:
```javascript
const courseSchema = new mongoose.Schema({
  title: { type: String, required: true },
  description: String,
  duration: String,
  instructor: String,
  createdBy: { type: String, required: true },
});
```

### Users Collection:
```javascript
const UserSchema = new mongoose.Schema({
  userId: { type: String, required: true, unique: true },
  role: { type: String, enum: [ADMIN, USER], default: USER },
  enrolledCourses: [{ type: mongoose.Schema.Types.ObjectId, ref: "Course" }],
});
```

---

## Routes

### Admin Routes:
```javascript
// Adds a new course
router.post(
  "/courses",
  authenticate,
  authorizeRole("admin"),
  CourseController.AddCourse
);

// Fetches all courses
router.get("/courses", CourseController.getAllCourse);

// Fetches details of a single course
router.get("/course/:id", CourseController.getCourse);

// Fetches all courses created by the admin
router.get("/adminCourses", authenticate, CourseController.getAdminCourse);

// Updates an existing course
router.put(
  "/courses/:id",
  authenticate,
  authorizeRole("admin"),
  CourseController.updateCourse
);

// Deletes a course
router.delete(
  "/courses/:id",
  authenticate,
  authorizeRole("admin"),
  CourseController.deleteCourse
);
```

### User Routes:
```javascript
// Logs in the user
router.post("/login", UserController.userLogin);

// Enrolls the user in a course
router.post("/enroll/:courseId", authenticate, UserController.userEnroll);

// Checks if the user is enrolled in any course
router.get("/check-enrollment", authenticate, UserController.checkEnroll);

// Fetches all courses the user has enrolled in
router.get("/enrolledCourses", authenticate, UserController.enrolledCourses);
```

---

## Additional Notes

1. The project includes detailed comments in the codebase for better understanding.
2. Authentication middleware ensures secure role-based access.
3. API endpoints are thoroughly tested using **Postman**.
4. The frontend is mobile-responsive and optimized for various screen sizes.
5. Bonus features such as search and filtering are implemented for enhanced usability.

---

We hope you enjoy exploring the project as much as we enjoyed building it! 😊
