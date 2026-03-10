# MU Dev Archive — Implementation Plan

## 1. Project Overview

**Project Name:** MU Dev Archive  
**Goal:** Build a public archive/showcase platform where students can submit and display their web projects, and visitors can browse them like a lightweight Codecanyon-style gallery.

Each project will:
- Appear as a card in the archive
- Show thumbnail, title, short description, tech stack, and developer info
- Allow visitors to open the live demo
- Optionally allow inline preview if the target site allows embedding
- Show developer/team details and contact links

This project will be built **live in front of students**, so the implementation must be:
- Easy to explain
- Modular
- Beginner-observable
- Incremental
- Deployable on **Vercel Hobby**

---

## 2. Core Product Vision

MU Dev Archive is not just a project gallery. It should become:
- A **student project showcase platform**
- A **department archive of web programming work**
- A **portfolio discovery platform** for junior developers
- A **teaching example** for real-world MERN architecture

---

## 3. Technology Stack

We will use the **MERN stack**, but adapted properly for **Vercel Hobby**.

### Frontend
- React
- Next.js (recommended instead of plain React for routing, SSR/SEO, and easy Vercel deployment)
- Tailwind CSS
- Axios or Fetch API

### Backend
- Node.js
- Express-style route logic through **Next.js API routes** or **Vercel serverless functions**

### Database
- MongoDB Atlas
- Mongoose

### Authentication
- NextAuth.js or JWT-based custom auth
- For simplicity and teaching clarity, start with **JWT + role-based auth** or **NextAuth credentials provider**

### File/Image Storage
- Prefer **Cloudinary** for thumbnails/screenshots
- Do **not** store uploaded files inside Vercel filesystem

### Hosting
- Vercel Hobby plan
- MongoDB Atlas free/shared tier
- Cloudinary free tier

---

## 4. Important Architecture Decision

Because the full project will be hosted on **Vercel Hobby**, we should **not** build a traditional always-running Express server.

### Recommended practical approach
Use:
- **Next.js frontend**
- **API routes / serverless functions** for backend logic
- **MongoDB Atlas** as the database

### Why
Vercel Hobby is excellent for:
- Frontend hosting
- Serverless APIs
- Small to medium classroom projects

It is **not ideal** for:
- Long-running background workers
- Heavy file processing
- WebSocket-heavy real-time systems
- Traditional persistent Express servers

### Conclusion
We will still follow **MERN concepts**, but the backend will be implemented in a **serverless-friendly Node/Express-style architecture**.

This keeps the project:
- Fully deployable on Vercel
- Easy for students to understand
- Realistic for free-tier constraints

---

## 5. Development Philosophy

This project will be built while teaching students, so follow these rules:

1. **Build phase by phase**
2. **Keep each class/demo focused on one visible outcome**
3. **Do not over-engineer early**
4. **Ship an MVP first**
5. **Use clean folder structure from day one**
6. **Add features only after the base flow works**
7. **Prefer simple code over clever code**
8. **Keep backend and frontend responsibilities clearly separated**
9. **Write code that students can read and reproduce**
10. **Deploy early and keep the live link working**

---

## 6. Primary User Roles

### 1) Visitor
Can:
- Browse projects
- Search and filter
- View project details
- Open live demo
- View developer/team info
- Contact developer through provided links

### 2) Student Developer
Can:
- Register/login
- Create a profile
- Submit a project
- Edit own project
- Add links, screenshots, and team members

### 3) Admin
Can:
- Approve or reject projects
- Edit metadata
- Feature projects
- Hide broken/inappropriate projects
- Manage categories and tags

---

## 7. MVP Scope (Must Build First)

The first release should include only the minimum useful features.

### Public Features
- Home page
- Explore projects page
- Project cards grid
- Project details page
- Developer profile page
- Search projects
- Filter by category / tech stack / batch
- Open live demo in new tab

### Student Features
- Register/login
- Submit project form
- Edit own profile
- Edit own project

### Admin Features
- Admin login
- Review submitted projects
- Approve / reject projects
- Mark project as featured

### Non-negotiable MVP data per project
- Title
- Slug
- Short description
- Full description
- Thumbnail
- Live URL
- Tech stack
- Category
- Developer/team info
- Approval status

---

## 8. Phase-wise Delivery Plan

## Phase 1 — Project Foundation
Goal: create the base code structure and deploy a working shell.

Tasks:
- Initialize Next.js project
- Configure Tailwind CSS
- Set up ESLint / Prettier
- Set up environment variables
- Connect MongoDB Atlas
- Create basic folder structure
- Create reusable layout, navbar, footer
- Deploy first version to Vercel

Deliverable:
- Live deployed skeleton app

---

## Phase 2 — Public Archive UI
Goal: visible public browsing experience.

Tasks:
- Home page
- Explore projects page
- Project card component
- Project details page
- Developer profile page
- Category badges
- Search UI
- Filter UI

Deliverable:
- Visitors can browse static/mock project data first

---

## Phase 3 — Database + Real Data
Goal: replace mock data with MongoDB data.

Tasks:
- Design Mongoose models
- Create seed data or insert sample projects
- Build API routes for project listing and details
- Connect frontend pages to real API

Deliverable:
- Projects are loaded from database

---

## Phase 4 — Authentication + Student Submission
Goal: allow students to create and manage entries.

Tasks:
- Register/login flow
- Role support (student, admin)
- Protected routes
- Submit project form
- Edit project form
- Profile edit form

Deliverable:
- Students can submit projects

---

## Phase 5 — Admin Review System
Goal: moderation workflow.

Tasks:
- Admin dashboard
- Pending projects list
- Approve/reject actions
- Feature/unfeature action
- Hide/archive project action

Deliverable:
- Admin can control published content

---

## Phase 6 — Polish + Stability
Goal: improve usability and presentation.

Tasks:
- Better loading states
- Empty states
- Error handling
- Responsive design fixes
- Image optimization
- Link validation
- Basic SEO metadata

Deliverable:
- Clean public release suitable for demonstration

---

## 9. Optional Phase 2+ Features

These should be added only after the MVP is stable.

- Team projects with multiple developers
- Batch-wise archive pages
- Semester/course-wise archive pages
- Featured projects section
- Faculty picks
- View counters
- Contact form with spam protection
- Bookmark/favorite system
- Demo video support
- GitHub repository links
- Broken link checker
- Project awards/badges

---

## 10. Recommended Folder Structure

```txt
mu-dev-archive/
├─ public/
├─ src/
│  ├─ app/
│  │  ├─ (public)/
│  │  │  ├─ page.tsx                 # home
│  │  │  ├─ projects/
│  │  │  │  ├─ page.tsx              # explore page
│  │  │  │  └─ [slug]/page.tsx       # project details
│  │  │  ├─ developers/
│  │  │  │  └─ [username]/page.tsx   # developer profile
│  │  ├─ dashboard/
│  │  │  ├─ page.tsx
│  │  │  ├─ projects/
│  │  │  └─ profile/
│  │  ├─ admin/
│  │  │  ├─ page.tsx
│  │  │  └─ projects/
│  │  ├─ api/
│  │  │  ├─ auth/
│  │  │  ├─ projects/
│  │  │  ├─ users/
│  │  │  └─ admin/
│  ├─ components/
│  │  ├─ layout/
│  │  ├─ ui/
│  │  ├─ cards/
│  │  ├─ forms/
│  │  └─ sections/
│  ├─ lib/
│  │  ├─ db.ts
│  │  ├─ auth.ts
│  │  ├─ validators.ts
│  │  └─ utils.ts
│  ├─ models/
│  │  ├─ User.ts
│  │  ├─ Project.ts
│  │  ├─ Category.ts
│  │  └─ Tag.ts
│  ├─ services/
│  ├─ hooks/
│  ├─ types/
│  └─ constants/
├─ .env.local
├─ package.json
└─ README.md
```

---

## 11. Core Data Models

## User
```ts
{
  name,
  username,
  email,
  passwordHash,
  role, // student | admin
  department,
  batch,
  bio,
  skills: [],
  profileImage,
  github,
  linkedin,
  portfolio,
  facebook,
  phone,
  createdAt,
  updatedAt
}
```

## Project
```ts
{
  title,
  slug,
  shortDescription,
  fullDescription,
  thumbnail,
  screenshots: [],
  liveUrl,
  githubUrl,
  videoUrl,
  techStack: [],
  category,
  tags: [],
  course,
  batch,
  semester,
  teamType, // individual | team
  developers: [], // references to users
  contactEmail,
  status, // draft | pending | approved | rejected | archived
  isFeatured,
  createdBy,
  approvedBy,
  createdAt,
  updatedAt
}
```

## Category
```ts
{
  name,
  slug,
  description
}
```

---

## 12. Minimum API Plan

### Public APIs
- `GET /api/projects`
- `GET /api/projects/[slug]`
- `GET /api/developers/[username]`
- `GET /api/categories`

### Student APIs
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/projects`
- `PATCH /api/projects/[id]`
- `GET /api/me`
- `PATCH /api/me`

### Admin APIs
- `GET /api/admin/projects?status=pending`
- `PATCH /api/admin/projects/[id]/approve`
- `PATCH /api/admin/projects/[id]/reject`
- `PATCH /api/admin/projects/[id]/feature`
- `PATCH /api/admin/projects/[id]/archive`

---

## 13. Key Pages to Build

### Public
1. Home
2. Explore Projects
3. Project Details
4. Developer Profile
5. Category Archive (optional in MVP)

### Student
6. Login/Register
7. Dashboard
8. Submit Project
9. Edit Project
10. Edit Profile

### Admin
11. Admin Dashboard
12. Pending Projects
13. Approved Projects
14. Categories Management (later)

---

## 14. Home Page Section Plan

Recommended sections:
- Hero section
- Search bar
- Featured projects
- Latest projects
- Browse by category
- Top technologies
- Top developers / active contributors
- Call to action for student submissions

Keep the home page simple in the first version.

---

## 15. Project Card Content

Each project card should show:
- Thumbnail
- Title
- Short description
- Category badge
- Tech stack badges
- Developer name(s)
- Batch or course label
- “View Details” button
- “Live Demo” button

Optional later:
- Featured badge
- New badge
- View count

---

## 16. Project Details Page Content

The project details page should include:
- Project title
- Short summary
- Main thumbnail / screenshot gallery
- Full description
- Tech stack
- Features list
- Live demo button
- GitHub button (optional)
- Video demo (optional)
- Developer/team section
- Contact links
- Related projects

### Preview note
Not all student projects will allow iframe embedding due to browser security headers. Therefore:
- Always keep **Open Live Demo** as the primary action
- Treat inline preview as optional enhancement

---

## 17. Submission Workflow

### Student flow
1. Student creates account or logs in
2. Student fills profile information
3. Student submits project
4. Project goes to `pending`
5. Admin reviews
6. Admin approves/rejects
7. Approved project becomes public

### Admin review checks
- Live URL works
- Project title/description are acceptable
- Thumbnail exists
- Links are safe
- No offensive or copied content

---

## 18. Validation Rules

Every project submission should validate:
- Title required
- Slug auto-generated and unique
- Short description required
- Live URL required and valid
- At least one tech stack item
- Thumbnail required
- Category required
- Developer info present

Optional but recommended:
- GitHub URL
- Video URL
- Screenshots

---

## 19. Security Rules

Must implement:
- Password hashing with bcrypt
- JWT/session protection
- Role-based access control
- Input validation with Zod or Joi
- URL validation
- Sanitization for text fields
- Rate limiting on auth/submission routes if possible
- Safe external links with `rel="noopener noreferrer"`

Do not trust client-side validation alone.

---

## 20. Database and Hosting Notes

### MongoDB Atlas
Use Atlas because Vercel serverless works well with it.

### Vercel notes
Because Vercel serverless functions are stateless:
- Use a reusable DB connection helper
- Keep API handlers lightweight
- Avoid heavy processing inside API routes

### File uploads
Do not upload large files directly into Vercel runtime.
Use:
- Cloudinary upload widget, or
- Client-to-Cloudinary direct upload flow

---

## 21. Environment Variables

Expected variables:

```env
MONGODB_URI=
JWT_SECRET=
NEXT_PUBLIC_APP_URL=
CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=
```

If using NextAuth:

```env
NEXTAUTH_URL=
NEXTAUTH_SECRET=
```

---

## 22. Teaching-Friendly Build Order

Because this will be shown to students, follow this order:

### Class/Demo 1
- Explain product idea
- Create Next.js app
- Set up Tailwind
- Build navbar/footer/home skeleton

### Class/Demo 2
- Create project cards UI
- Build explore page using mock data

### Class/Demo 3
- Build project details page with dynamic route

### Class/Demo 4
- Set up MongoDB Atlas and Mongoose
- Fetch real project data

### Class/Demo 5
- Create register/login flow

### Class/Demo 6
- Build submit project form

### Class/Demo 7
- Create admin approval workflow

### Class/Demo 8
- Polish UI, deploy, and explain production concerns

This sequence helps students see visible progress every session.

---

## 23. UI/UX Guidance

The visual style should feel modern but manageable.

Recommended direction:
- Clean spacing
- Simple cards
- Strong typography hierarchy
- Responsive layout
- Consistent buttons and badges
- Minimal color palette
- Good empty states and loading states

Do not try to make it overly fancy in the first version.
Focus on:
- Clarity
- Reusability
- Readability

---

## 24. Performance Guidance

Since this is on Vercel Hobby, optimize from the start.

- Use Next.js `Image`
- Compress thumbnails
- Paginate project listings later if needed
- Avoid unnecessary client-side fetching
- Prefer server rendering for public pages when practical
- Cache safe public reads where possible
- Keep bundle size under control

---

## 25. SEO and Discoverability

Basic SEO should be included even in MVP.

- Proper page titles
- Meta descriptions
- Open Graph image support
- Slug-based project URLs
- Developer profile URLs
- Search-engine-friendly public pages

---

## 26. Things to Avoid Early

Do not build these in the first version:
- Real-time chat
- Notifications system
- Complex analytics dashboard
- Payment system
- Full comments/reviews system
- Very granular RBAC
- Microservices
- Advanced state management unless necessary

The first goal is a strong, working archive platform.

---

## 27. Suggested Git Workflow

Use clean, small commits so students can follow the evolution.

Example branches:
- `main`
- `dev`
- `feature/homepage`
- `feature/project-listing`
- `feature/project-details`
- `feature/auth`
- `feature/submission`
- `feature/admin-review`

Commit style:
- `feat: add homepage hero section`
- `feat: build project card component`
- `feat: connect mongodb atlas`
- `feat: add student project submission form`
- `fix: handle missing project thumbnail`

---

## 28. Launch Checklist

Before public release:
- App deployed on Vercel
- MongoDB connection stable
- Auth works
- Project submission works
- Admin approval works
- Public project pages render correctly
- Mobile view is usable
- External links work safely
- Required metadata is present
- Error states are handled

---

## 29. Immediate Execution Plan

Start with the following exact order:

1. Initialize project with Next.js + Tailwind
2. Set up folder structure
3. Build public UI using static mock data
4. Create reusable project card and project details page
5. Connect MongoDB Atlas
6. Create Mongoose models
7. Replace mock data with API-driven data
8. Add authentication
9. Add project submission flow
10. Add admin review flow
11. Polish and deploy

---

## 30. Final Direction for Cursor

When implementing this project, Cursor should follow these rules:

1. Respect the Vercel Hobby limitations
2. Use **Next.js + MongoDB Atlas + serverless API routes**
3. Keep the code modular and beginner-readable
4. Prioritize MVP over advanced features
5. Avoid unnecessary dependencies
6. Use clean reusable components
7. Implement features in the planned order
8. Prefer small, safe diffs
9. Do not redesign the architecture without strong reason
10. Keep the project demo-friendly and classroom-friendly

---

## 31. Recommended Next Step

After this plan, the next document to create should be:
- `agent.md` or `cursor-rules.md`

That file should define:
- Coding rules
- Folder discipline
- Naming conventions
- API design conventions
- UI consistency rules
- Deployment constraints
- “Do not over-engineer” principles

---

## 32. Summary

MU Dev Archive should be built as a **teaching-first, portfolio-ready, Vercel-friendly MERN showcase platform**.

The correct strategy is:
- Keep architecture simple
- Build in phases
- Use serverless-friendly backend patterns
- Start with strong public browsing and project submission
- Add admin moderation
- Polish only after the main flow works

This will make the project:
- Practical for students
- Affordable on free tiers
- Easy to deploy
- Easy to explain in class
- Strong enough to become a real academic showcase platform
