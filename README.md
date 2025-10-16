# 🎓 Graduation Project: DIVO

## 💡 Project Overview

DIVO is a comprehensive platform designed to provide a community-driven space for technical support, peer-to-peer assistance, and a centralized database for common technical issues. It features a robust backend API supporting user profiles, a full-featured community forum (posts, likes, comments, shares), a ticketing system for specialized support ("Help Sessions"), web scraping for product pricing, and a curated database for Windows error codes.

This project was developed as a requirement for the **Software Industry and multimedia** program.

-----

## ⚙️ Technologies Used

| Category | Technology | Description |
| :--- | :--- | :--- |
| **Backend** | **Node.js** | JavaScript runtime environment. |
| **Framework** | **Express.js** | Minimalist web application framework for Node.js. |
| **Database** | **MongoDB** | NoSQL database for flexible data storage. |
| **Authentication** | **JWT (JSON Web Tokens)** | For secure, state-less authentication. |
| **File Storage** | **Cloudinary** | For cloud-based image and video storage (used with Multer). |
| **Web Scraping** | **[Mention a specific library like Puppeteer/Cheerio if you used one]** | Used for price comparison/data extraction from e-commerce sites. |
| **Email** | **Gmail** | Used for contact forms and password reset functionality. |

-----

## 🚀 Getting Started

Follow these instructions to set up and run the project locally.

### Prerequisites

You need the following installed:

  * **Node.js** (v14.x or later recommended)
  * **npm** (Node Package Manager)
  * **MongoDB** (Local instance or Atlas connection string)

### Installation

1.  **Clone the repository:**

    ```bash
    git clone [Your Repository URL]
    cd [Project Folder Name]
    ```

2.  **Install dependencies:**

    ```bash
    npm install
    ```

3.  **Configure Environment Variables:**
    Create a file named `.env` in the root directory and add your configuration variables. At minimum, you'll need:

    ```
    PORT=5000
    MONGO_URI="[Your MongoDB Connection String]"
    JWT_SECRET="[A long, secure random string]"
    CLOUDINARY_CLOUD_NAME="[Your Cloud Name]"
    CLOUDINARY_API_KEY="[Your API Key]"
    CLOUDINARY_API_SECRET="[Your API Secret]"
    # Add other variables for email service, etc.
    ```

4.  **Run the application:**

    ```bash
    npm start
    # or if using nodemon:
    npm run dev
    ```

    The API should now be running at `http://localhost:[PORT]` (default: `http://localhost:5000`).

-----

## 🌐 API Documentation

The API follows a RESTful architecture, utilizing multiple endpoints for different functionalities. All API endpoints are prefixed with `/api/`.

### 1\. User & Authentication (`/api/users` & `/api/specialists`)

| Endpoint | Method | Description | Access |
| :--- | :--- | :--- | :--- |
| `/api/users/register` | `POST` | Register a new user. | Public |
| `/api/users/login` | `POST` | Log in a user. | Public |
| `/api/users/:id` | `GET` | Get a specific user's profile. | Auth |
| `/api/users/:id` | `DELETE` | Delete a user. | Admin |
| `/api/users/upload/profile-image` | `POST` | Upload a user's profile image. | Auth |
| **Specialist** | | | |
| `/api/specialists/register` | `POST` | Register a new specialist. | Public |
| `/api/specialists/login` | `POST` | Log in a specialist. | Public |
| `/api/specialists` | `GET` | Get all specialists (paginated). | Admin/Specialist |

\<hr\>

### 2\. Password Management (`/api/auth`)

| Endpoint | Method | Description | Access |
| :--- | :--- | :--- | :--- |
| `/api/auth/forgot-password` | `POST` | Initiates password reset (sends OTP). | Public |
| `/api/auth/verify-otp` | `POST` | Verifies the received OTP. | Public |
| `/api/auth/reset-password` | `POST` | Resets the user's password. | Public |

\<hr\>

### 3\. Community Forum (`/api/community/posts`)

| Endpoint | Method | Description | Access |
| :--- | :--- | :--- | :--- |
| `/` | `GET` | Get all posts (supports pagination: `?page=&limit=`). | Public |
| `/:id` | `GET` | Get a single post by ID. | Public |
| `/` | `POST` | Create a new post. | Auth |
| `/upload` | `POST` | Upload an image for a post. | Auth |
| `/:id/like` | `PATCH` | Like a post. | Auth |
| `/:id/unlike` | `PATCH` | Unlike a post. | Auth |
| `/:id/addcomments` | `POST` | Add a comment to a post. | Auth |
| `/:id/comments` | `GET` | Get all comments for a post. | Public |
| `/:postId/comments/:commentId` | `DELETE` | Delete a specific comment. | Auth |
| `/:id` | `DELETE` | Delete a post. | Auth |

\<hr\>

### 4\. Help Sessions/Ticketing (`/api/helpSessions`)

This module manages technical support requests.

| Endpoint | Method | Description | Access |
| :--- | :--- | :--- | :--- |
| `/` | `POST` | Create a new help session/support request. | Auth |
| `/` | `GET` | Get all help sessions. | Admin/Specialist |
| `/:id` | `GET` | Get a specific help session. | Admin/Specialist |
| `/technician/:id/status` | `PATCH` | Update session status and assign a technician. | Admin/Specialist |
| `/technician/:id/note` | `PATCH` | Add a note to a session. | Admin/Specialist |

\<hr\>

### 5\. Windows Error Database (`/api/windowsError`)

| Endpoint | Method | Description | Access |
| :--- | :--- | :--- | :--- |
| `/` | `GET` | Get all Windows errors. | Public |
| `/search?code=[code]` | `GET` | Search for an error by code. | Public |
| `/` | `POST` | Create a new Windows error entry. | Public |
| `/:id` | `PATCH` | Update an error entry. | Admin |
| `/:id` | `DELETE` | Delete an error entry. | Admin |

\<hr\>

### 6\. E-Commerce Scraping (`/api/scrape`)

Endpoints to fetch product information/prices from various e-commerce platforms.

| Endpoint | Method | Description | Access |
| :--- | :--- | :--- | :--- |
| `/scrapeAll` | `GET` | Scrape data from all configured stores. | Public |
| `/amazon` | `GET` | Scrape data from Amazon. | Public |
| `/jumia` | `GET` | Scrape data from Jumia. | Public |
| `/shiko` | `GET` | Scrape data from ShikoStore. | Public |
| `/cairoSales` | `GET` | Scrape data from Cairo Sales. | Public |
| `/maxHardware` | `GET` | Scrape data from Max Hardware. | Public |

\<hr\>

### 7\. Service Shops (`/api/serviceShops`)

| Endpoint | Method | Description | Access |
| :--- | :--- | :--- | :--- |
| `/shops` | `GET` | Get all service shops (all). | Public |
| `/` | `GET` | Get service shops (paginated). | Public |
| `/` | `POST` | Create a new service shop entry. | Admin |
| `/:id` | `PATCH` | Update a service shop. | Admin |
| `/:id` | `DELETE` | Delete a service shop. | Admin |

-----

## 🔒 Security & Middleware

The API implements the following security measures and middleware:

  * **`requireAuth`**: Ensures the user is logged in by validating a **JWT** in the request header. This protects most user-specific actions.
  * **`requireAdmin`**: Restricts access to administrative tasks (e.g., deleting a user, managing service shops) to users with the Admin role.
  * **`requireAdminOrSpecialist`**: Grants access to both Admin and Specialist roles for actions related to help session management.
  * **`combinedAuth`**: Middleware likely used to check for authentication across multiple user types (e.g., general user, admin, specialist).
  * **`multer`**: Used for handling **`multipart/form-data`** and uploading images/videos to Cloudinary before saving the URL to the database.

-----

## 📞 Contact

For any questions or feedback, please contact:

  * **Hany Elsayed Moghera** - hmougera@gmail.com
