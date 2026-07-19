# Search Civil - Digital Archive for Civil Cards

A digital archive system for civil cards with Next.js API and Vite + React frontend.

## Architecture

```
├── apps/
│   ├── api/          # Next.js 15 API Server
│   └── web/          # Vite + React Frontend
├── packages/
│   └── shared/       # Shared types and utilities
└── storage/          # File storage (images, PDFs)
```

## Prerequisites

- Node.js 18+
- MongoDB at 192.168.30.151:27017

## Setup

### 1. Install Dependencies

```bash
npm install
cd apps/api && npm install
cd ../web && npm install
```

### 2. Configure Environment

Edit `apps/api/.env`:

```env
MONGODB_URI=mongodb://192.168.30.151:27017/searchCivil
JWT_SECRET=your-secret-key
STORAGE_PATH=D:\searchCivil\storage
```

### 3. Seed Admin User

```bash
cd apps/api
npx tsx src/scripts/seed.ts
```

Default credentials:
- Email: admin@example.com
- Password: admin123

### 4. Start Development

```bash
# From root
npm run dev

# Or separately
cd apps/api && npm run dev    # API on port 3001
cd apps/web && npm run dev    # Frontend on port 5173
```

## Features

### User Roles

| Role | Permissions |
|------|-------------|
| Admin | Full access |
| Supervisor | Search, Add, Edit, Delete, Upload |
| Employee | Search, View, Upload, Edit own cards |
| Employee | Search only |

### Pages

- **Dashboard**: Statistics and recent activity
- **Search**: Search by civil number, contract, or name
- **Upload**: Single file upload with smart detection
- **Bulk Upload**: Import multiple files from folder
- **Citizens**: List and manage citizens
- **Citizen Details**: View all cards for a citizen
- **Document Viewer**: View images and PDFs
- **Companies**: Manage companies
- **Users**: User management (admin only)

### File Naming Convention

For smart upload, name files as:
- `123456789-2025.jpg` (Civil Number - Year)
- `123456789-2025.pdf`

### Storage Structure

```
storage/
├── images/
│   └── 2025/
│       └── 01/
│           └── 123456789-2025.jpg
├── pdfs/
│   └── 2025/
│       └── 123456789-2025.pdf
├── thumbnails/
└── backups/
```

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | /api/auth/login | Login |
| POST | /api/auth/register | Register (admin) |
| GET | /api/citizens | List citizens |
| POST | /api/citizens | Create citizen |
| GET | /api/citizens/:id | Get citizen with documents |
| PUT | /api/citizens/:id | Update citizen |
| DELETE | /api/citizens/:id | Delete citizen |
| GET | /api/search | Search citizens |
| POST | /api/upload | Upload document |
| POST | /api/bulk-upload | Bulk upload |
| GET | /api/documents | List documents |
| PUT | /api/documents | Update document |
| DELETE | /api/documents | Delete document |
| GET | /api/documents/:id | Get document file |
| GET | /api/companies | List companies |
| POST | /api/companies | Create company |
| GET | /api/users | List users |
| POST | /api/users | Create user |
| GET | /api/dashboard | Dashboard stats |
| POST | /api/backup | Create backup |
| GET | /api/backup | List backups |
