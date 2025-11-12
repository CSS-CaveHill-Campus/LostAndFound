# Lost and Found - UWI CaveHill

This project is a full-stack "Lost and Found" web application designed for the University of the West Indies, Cave Hill Campus. It serves as a foundational template for students to learn modern web development concepts, build upon, and implement their own unique solutions.

The goal is to provide a centralized online platform where students and staff can report items they've lost or found on campus, facilitating the return of belongings to their rightful owners.

## Features

The application will include the following core features:

-   User Authentication & Profiles: Users can sign up and log in using their university email. Each user will have a simple profile with their name and contact information.
-   Create Reports: Users can create two types of reports:
    -   Lost Item Report: For items they have lost.
    -   Found Item Report: For items they have found on campus.
-   Detailed Reporting: Reports will include key details such as:
    -   Item name and a detailed description.
    -   A category (e.g., Electronics, Books, ID Cards, Personal Belongings).
    -   The location where the item was lost or found.
    -   The date of the incident.
    -   An option to upload an image of the item.
-   View and Search Reports: A central dashboard will display all recent reports. Users can search for items by name or filter them by category and status (Lost/Found).
-   Commenting System: Users can comment on reports to ask for more information or to arrange a return.
-   Status Updates: The creator of a report can update its status to "Claimed" or "Returned" once an item has been recovered.

### Simple Future Enhancements

For students looking to expand the project, here are some simple but valuable features to consider:

-   Email Notifications: Automatically send an email to a user when someone comments on their report.
-   Admin Dashboard: A special view for campus administration to manage and remove inappropriate or outdated reports.
-   Map Integration: Use a simple map API (like Leaflet) to allow users to pin the location where an item was lost or found.

## Technology Stack

This project will be built using a modern, industry-standard technology stack that is great for learning and building scalable applications.

-   Frontend:
    -   React.js: A powerful library for building dynamic user interfaces.
    -   Next.js: A React framework that provides features like server-side rendering, static site generation, and a built-in API backend.
-   Backend:
    -   Next.js API Routes: We will use the backend capabilities of Next.js to create our REST API.
    -   Mongoose: An Object Data Modeling (ODM) library for MongoDB and Node.js, which helps in creating and validating our data structures.
-   Database:
    -   MongoDB: A flexible NoSQL database that is easy to get started with.

### Additional Tools & Libraries

To enhance the development process, we will be using these tools:

-   Styling: Chakra UI for building a clean and modern UI without writing a lot of custom CSS.
-   Authentication: NextAuth.js to easily add robust and secure user authentication (e.g., login with Google/university email).
-   State Management: Zustand or React Context API for managing global application state, such as the logged-in user's information.
-   Form Handling: React Hook Form to simplify form creation, validation, and submission.
-   Image Uploads: Images will be stored on the user's device for now.

## Architectural Details

This application follows a modern, component-based architecture for the frontend and a simple, scalable structure for the backend.

### Frontend Architecture

-   Components: The UI is broken down into small, reusable components (e.g., `Button`, `Input`, `ReportCard`).
-   Pages: Next.js uses a file-based routing system where each file or folder in the `app` directory becomes a route segment (e.g., `app/page.tsx` is the homepage).
-   Layouts: We will create a main `Layout` component to maintain a consistent look and feel (e.g., header, footer) across all pages.

The project will be structured as follows:

```
lost-and-found/
├── /public            # Any public resources like images
└── /src
    └── /app           # Application routes
        ├── /components    # Reusable UI components
        ├── /lib           # Helper functions, database connection
        └── /styles        # Global styles
```

### Backend & API Design

The backend will be a REST API built with Next.js API routes. This keeps the frontend and backend code in a single, unified project.

-   API Endpoints: We will define clear endpoints for each action. For example:
    -   `POST /api/items` - Create a new item report.
    -   `GET /api/items` - Get a list of all item reports.
    -   `GET /api/items?category=electronics` - Filter items by category.
    -   `PUT /api/items/[id]` - Update a specific itemThe project will be structured as follows: We will define schemas for our database collections to ensure data consistency.

User Schema:

```javascript
{
  id: String (UUID),
  name: String,
  email: { type: String, unique: true }, // Log in with School account
  number: String,
  createdAt: Date
}
```

Item Schema:

```javascript
{
  id: String (UUID),
  name: String,
  description: String,
  category: String,
  status: Status,
  location: String,
  imageUrl: String,
  reportedBy: { type: Schema.Types.ObjectId, ref: 'User' },
  createdAt: Date,
  updatedAt: Date
}
```

Comment Schema:

```javascript
{
  id: String (UUID),
  text: String,
  author: { type: Schema.Types.ObjectId, ref: 'User' },
  item: { type: Schema.Types.ObjectId, ref: 'Item' },
  createdAt: Date,
  updatedAt: Date
}
```

Status Enum:

```typescript
enum Status {
    Lost,
    Found,
    Claimed
}```
