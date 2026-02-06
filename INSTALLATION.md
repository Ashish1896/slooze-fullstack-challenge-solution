INSTALLATION.md# Installation & Setup Guide

## Prerequisites
- Node.js v16 or higher
- npm or yarn
- Git

## Quick Start (5 minutes)

### 1. Clone the Repository

```bash
git clone https://github.com/Ashish1896/slooze-fullstack-challenge-solution.git
cd slooze-fullstack-challenge-solution
```

### 2. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create environment file
echo 'DATABASE_URL="file:./dev.db"' > .env
echo 'JWT_SECRET="your-super-secret-jwt-key-change-this"' >> .env
echo 'JWT_EXPIRATION="7d"' >> .env

# Run Prisma migrations
npx prisma migrate dev --name init

# Seed database with mock data
npx prisma db seed

# Start the backend
npm run start:dev
```

Backend will be available at: `http://localhost:3001`
GraphQL Playground: `http://localhost:3001/graphql`

### 3. Frontend Setup

In a new terminal:

```bash
cd frontend

# Install dependencies
npm install

# Create environment file
echo 'NEXT_PUBLIC_GRAPHQL_URL=http://localhost:3001/graphql' > .env.local

# Start the frontend
npm run dev
```

Frontend will be available at: `http://localhost:3000`

## Login Credentials

Use these accounts to test the application:

### Admin Account
- **Email**: admin@slooze.com
- **Password**: Admin@123
- **Country**: INDIA
- **Permissions**: All features

### Manager Account
- **Email**: manager@slooze.com
- **Password**: Manager@123
- **Country**: AMERICA
- **Permissions**: View restaurants, create orders, checkout, cancel orders

### Member Account
- **Email**: user@slooze.com
- **Password**: User@123
- **Country**: INDIA
- **Permissions**: View restaurants, create orders only

## Troubleshooting

### Port Already in Use

If port 3001 or 3000 is already in use:

**Backend** (change port in main.ts or use):
```bash
PORT=3002 npm run start:dev
```

**Frontend** (Next.js will ask or use):
```bash
PORT=3001 npm run dev
```

### Database Issues

Reset the database:

```bash
cd backend
rm dev.db
npx prisma migrate dev --name init
npx prisma db seed
```

### GraphQL Connection Issues

1. Verify the backend is running on port 3001
2. Check CORS is enabled in NestJS
3. Update `NEXT_PUBLIC_GRAPHQL_URL` in frontend `.env.local`

## Development Commands

### Backend

```bash
cd backend

# Start in watch mode
npm run start:dev

# Build for production
npm run build

# Run linter
npm run lint

# Run tests
npm test
```

### Frontend

```bash
cd frontend

# Development server
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Run linter
npm run lint
```

## Architecture

### Backend Structure

```
backend/
├── src/
│   ├── auth/           # Authentication & authorization
│   ├── restaurant/     # Restaurant management
│   ├── order/         # Order management
│   ├── payment/       # Payment methods
│   └── app.module.ts  # Main module
├── prisma/
│   └── schema.prisma  # Database schema
└── package.json
```

### Frontend Structure

```
frontend/
├── pages/
│   ├── _app.tsx       # App wrapper
│   ├── login.tsx      # Login page
│   └── dashboard.tsx  # Main dashboard
├── components/        # React components
├── graphql/          # GraphQL queries
└── package.json
```

## Database

### Mock Data Seeding

The application includes seed data for:

**Restaurants**:
- 5 restaurants in India
- 5 restaurants in America

**Menu Items**:
- 50+ menu items across all restaurants

**Users**:
- 3 test accounts (admin, manager, member)

## GraphQL Examples

### Query Restaurants

```graphql
query {
  restaurants {
    id
    name
    country
    menuItems {
      id
      name
      price
    }
  }
}
```

### Create Order

```graphql
mutation {
  createOrder(
    restaurantId: "restaurant-id"
    items: ["item-1", "item-2"]
    quantities: [2, 1]
  ) {
    id
    totalPrice
    status
  }
}
```

## Production Deployment

### Deploy Backend

1. Build the application: `npm run build`
2. Set environment variables on your hosting platform
3. Run: `npm run start:prod`

**Recommended Platforms**:
- Vercel
- Heroku
- Railway
- Render

### Deploy Frontend

1. Build: `npm run build`
2. Deploy to Vercel, Netlify, or similar

**Environment Variables**:
- `NEXT_PUBLIC_GRAPHQL_URL` - Your backend GraphQL endpoint

## Support

For issues or questions:
- Email: careers@slooze.xyz
- GitHub Issues: [Create an issue](https://github.com/Ashish1896/slooze-fullstack-challenge-solution/issues)

## License

MIT
