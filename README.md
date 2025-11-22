# 📦 Inventory Management System

A full-stack Inventory Management System built with **React + TypeScript** (Frontend) and **Node.js + Express** (Backend Microservices) using **MongoDB**.

## 🏗️ Project Structure

```
inventory-management-system/
├── client/                 # React Frontend
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vite.config.ts
├── server/                 # Node.js Backend (Microservices)
│   ├── backend-auth/       # Authentication Service (Port 5000)
│   ├── backend-products/   # Products Service (Port 5001)
│   ├── backend-receipt/    # Receipt Service (Port 5002)
│   ├── backend-deliveries/ # Delivery Service (Port 5003)
│   ├── backend-transfer/   # Transfer Service (Port 5004)
│   ├── backend-adjustment/ # Adjustment Service (Port 5005)
│   ├── backend-dashboard/  # Dashboard Service (Port 5006)
│   ├── shared/             # Shared middleware and utilities
│   ├── docker-compose.yml  # Docker configuration
│   └── package.json
├── package.json            # Root package.json with scripts
├── .gitignore
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- **Node.js** (v18 or higher)
- **npm** (v9 or higher)
- **MongoDB** (via Docker or local installation)
- **Docker & Docker Compose** (recommended)

### Installation

1. **Clone the repository:**
   ```bash
   git clone <your-repo-url>
   cd inventory-management-system
   ```

2. **Install all dependencies:**
   ```bash
   npm run install:all
   ```

   Or install separately:
   ```bash
   npm run install:client  # Frontend dependencies
   npm run install:server  # Backend dependencies
   ```

3. **Setup environment variables:**
   - Copy `.env.example` files in server services
   - Configure MongoDB connection strings
   - Set JWT secrets

   ```bash
   cd server
   cp backend-auth/env.example backend-auth/.env
   cp backend-products/env.example backend-products/.env
   # ... repeat for all services
   ```

### Running the Application

#### Option 1: Run Both Frontend & Backend Together (Recommended)

```bash
npm run dev
```

This will start:
- Frontend on `http://localhost:8080`
- All backend services on ports `5000-5006`

#### Option 2: Run Separately

**Terminal 1 - Backend:**
```bash
npm run dev:server
# Or with Docker:
npm run docker:up
```

**Terminal 2 - Frontend:**
```bash
npm run dev:client
```

#### Option 3: Docker Compose (Easiest)

```bash
npm run docker:up
```

Then in another terminal:
```bash
npm run dev:client
```

## 📝 Available Scripts

### Root Level Scripts

- `npm run dev` - Run both frontend and backend in development mode
- `npm run dev:client` - Run only frontend
- `npm run dev:server` - Run only backend
- `npm run build` - Build both frontend and backend for production
- `npm run start` - Start both in production mode
- `npm run docker:up` - Start all services with Docker Compose
- `npm run docker:down` - Stop all Docker services
- `npm run install:all` - Install dependencies for both client and server

### Client Scripts

- `npm run dev` - Start Vite dev server
- `npm run build` - Build for production
- `npm run preview` - Preview production build

### Server Scripts

- `npm run dev` - Start all microservices with nodemon
- `npm start` - Start all microservices in production mode

## 🔧 Environment Variables

### Frontend (.env in client/)

```env
VITE_API_AUTH_URL=http://localhost:5000
VITE_API_PRODUCTS_URL=http://localhost:5001
VITE_API_RECEIPT_URL=http://localhost:5002
VITE_API_DELIVERY_URL=http://localhost:5003
VITE_API_TRANSFER_URL=http://localhost:5004
VITE_API_ADJUSTMENT_URL=http://localhost:5005
VITE_API_DASHBOARD_URL=http://localhost:5006
```

### Backend Services (.env in each service folder)

Each service requires:

```env
PORT=5000  # Service-specific port
MONGODB_URI=mongodb://localhost:27017/inventory_db
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRES_IN=7d
```

For Docker:
```env
MONGODB_URI=mongodb://mongodb:27017/inventory_db
```

## 🌐 CORS Configuration

CORS is already configured in all backend services to allow requests from:
- `http://localhost:8080` (Frontend)
- `http://localhost:3000` (Alternative frontend port)

To modify CORS settings, edit the `cors()` middleware in each service's `src/index.js`:

```javascript
app.use(cors({
  origin: process.env.FRONTEND_URL || 'http://localhost:8080',
  credentials: true
}));
```

## 🔌 API Endpoints

### Authentication Service (Port 5000)
- `POST /auth/register` - Register new user
- `POST /auth/login` - Login user
- `GET /auth/profile` - Get user profile
- `POST /auth/forgot-password` - Request password reset
- `POST /auth/reset-password` - Reset password

### Products Service (Port 5001)
- `GET /products` - Get all products
- `POST /products` - Create product
- `GET /products/:id` - Get product by ID
- `PUT /products/:id` - Update product
- `DELETE /products/:id` - Delete product

### Other Services
See `server/API_ENDPOINTS_REFERENCE.md` for complete API documentation.

## 🗄️ Database

The system uses **MongoDB** as the database. 

### Using Docker (Recommended):
```bash
npm run docker:up
```

### Manual Setup:
1. Install MongoDB locally
2. Start MongoDB service
3. Update `MONGODB_URI` in all service `.env` files to: `mongodb://localhost:27017/inventory_db`

## 🐳 Docker Setup

The project includes Docker Compose configuration for easy setup:

```bash
# Start all services (MongoDB + Backend services)
npm run docker:up

# Stop all services
npm run docker:down

# Rebuild containers
npm run docker:build
```

## 🧪 Testing

### Health Checks

Check if services are running:

```bash
# Auth Service
curl http://localhost:5000/health

# Products Service
curl http://localhost:5001/health
```

## 📦 Building for Production

```bash
# Build both frontend and backend
npm run build

# Build only frontend
npm run build:client

# Build only backend
npm run build:server
```

## 🔐 Security Features

- JWT-based authentication
- Password hashing with bcrypt
- Role-based access control (admin, staff)
- CORS protection
- Input validation and sanitization

## 📚 Documentation

- **API Documentation**: `server/API_ENDPOINTS_REFERENCE.md`
- **Database Setup**: `server/DATABASE_SETUP.md`
- **Frontend Integration**: `server/FRONTEND_INTEGRATION_GUIDE.md`

## 🛠️ Tech Stack

### Frontend
- React 18
- TypeScript
- Vite
- Tailwind CSS
- Shadcn UI
- Axios
- React Router

### Backend
- Node.js
- Express.js
- MongoDB (Mongoose)
- JWT Authentication
- Microservices Architecture
- Docker

## 🐛 Troubleshooting

### Port Already in Use
If you get "port already in use" error:
```bash
# Windows
netstat -ano | findstr :5000

# Mac/Linux
lsof -i :5000
```

### Database Connection Issues
1. Ensure MongoDB is running
2. Check `MONGODB_URI` in `.env` files
3. For Docker, ensure containers are on the same network

### CORS Errors
1. Check CORS configuration in backend services
2. Verify frontend URL matches CORS allowed origins
3. Ensure backend services are running

## 📝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 👥 Authors

- Your Name

## 🙏 Acknowledgments

- Shadcn UI for the component library
- All contributors and open-source libraries used

---

**Happy Coding! 🚀**

For detailed setup instructions, see `HOW_TO_RUN.md`

