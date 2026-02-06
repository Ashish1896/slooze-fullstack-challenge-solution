# Slooze Full-Stack Challenge Solution

> A full-stack role-based food ordering web application built with **NestJS**, **GraphQL**, **Prisma**, **Next.js**, **TypeScript**, and **Apollo Client**.

## 🎯 Overview

This is a comprehensive solution for the Slooze Take-Home Challenge - a full-stack food ordering platform with role-based access control and country-specific restrictions.

### Features Implemented

✅ **Role-Based Access Control (RBAC)**
- Admin: Full system access
- Manager: Order & restaurant management
- Member: Basic ordering capabilities

✅ **Country-Based Access Model**
- Users restricted to their assigned country (India/America)
- Restaurants accessible only from users' country

✅ **Core Features**
- View restaurants & menu items (All roles)
- Create orders with multiple items (All roles)
- Checkout & payment (Admin & Manager only)
- Cancel orders (Admin & Manager only)
- Payment method management (Admin only)

✅ **Mock Data**
- Pre-populated restaurants in India & America
- Mock menu items for each restaurant

## 🛠 Tech Stack

### Backend
- **NestJS** - Modern Node.js framework
- **GraphQL** - Query language for APIs
- **Prisma** - ORM for database
- **SQLite** - Lightweight database
- **JWT** - Authentication
- **bcrypt** - Password hashing

### Frontend
- **Next.js** - React framework
- **TypeScript** - Type safety
- **Apollo Client** - GraphQL client
- **Tailwind CSS** - Styling

## 📁 Project Structure

```
.
├── backend/
│   ├── src/
│   │   ├── auth/
│   │   │   ├── auth.service.ts
│   │   │   ├── jwt.guard.ts
│   │   │   └── roles.guard.ts
│   │   ├── restaurant/
│   │   │   └── restaurant.resolver.ts
│   │   ├── order/
│   │   │   └── order.resolver.ts
│   │   ├── payment/
│   │   │   └── payment.resolver.ts
│   │   ├── app.module.ts
│   │   └── main.ts
│   ├── prisma/
│   │   └── schema.prisma
│   ├── package.json
│   └── .env
│
├── frontend/
│   ├── pages/
│   │   ├── login.tsx
│   │   ├── dashboard.tsx
│   │   └── _app.tsx
│   ├── components/
│   │   ├── RestaurantList.tsx
│   │   ├── OrderForm.tsx
│   │   └── PaymentManager.tsx
│   ├── graphql/
│   │   └── queries.ts
│   ├── package.json
│   └── .env.local
│
├── README.md
└── .gitignore
```

## 🚀 Getting Started

### Prerequisites
- Node.js >= 16
- npm or yarn

### Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Set up database
npx prisma migrate dev --name init

# Seed mock data (optional)
npx prisma db seed

# Start development server
npm run start:dev
```

Backend will run on `http://localhost:3001` with GraphQL playground at `http://localhost:3001/graphql`

### Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Set up environment variables
echo "NEXT_PUBLIC_GRAPHQL_URL=http://localhost:3001/graphql" > .env.local

# Start development server
npm run dev
```

Frontend will run on `http://localhost:3000`

## 📝 Environment Variables

### Backend (.env)
```
DATABASE_URL="file:./dev.db"
JWT_SECRET="your_jwt_secret_key"
JWT_EXPIRATION="7d"
```

### Frontend (.env.local)
```
NEXT_PUBLIC_GRAPHQL_URL=http://localhost:3001/graphql
```

## 🔐 Authentication

### Sample Users for Testing

**Admin**
- Email: admin@slooze.com
- Password: Admin@123
- Country: INDIA

**Manager**
- Email: manager@slooze.com
- Password: Manager@123
- Country: AMERICA

**Member**
- Email: user@slooze.com
- Password: User@123
- Country: INDIA

## 🔄 API Endpoints (GraphQL)

### Queries

```graphql
# Get all restaurants in user's country
query GetRestaurants {
  restaurants {
    id
    name
    address
    country
    menuItems {
      id
      name
      price
      description
    }
  }
}

# Get user's orders
query GetOrders {
  orders {
    id
    restaurant {
      name
    }
    status
    totalPrice
    orderItems {
      menuItem {
        name
      }
      quantity
    }
  }
}
```

### Mutations

```graphql
# Create an order
mutation CreateOrder($restaurantId: String!, $items: [String!]!, $quantities: [Int!]!) {
  createOrder(restaurantId: $restaurantId, items: $items, quantities: $quantities) {
    id
    totalPrice
    status
  }
}

# Checkout order
mutation CheckoutOrder($orderId: String!) {
  checkoutOrder(orderId: $orderId) {
    id
    status
  }
}

# Cancel order
mutation CancelOrder($orderId: String!) {
  cancelOrder(orderId: $orderId) {
    id
    status
  }
}
```

## 🧪 Testing

### Test Flow

1. **Login** as Admin, Manager, or Member
2. **View Restaurants** - See only restaurants in your country
3. **Create Order** - Add items to cart
4. **Checkout** - Complete order (Admin/Manager only)
5. **Cancel Order** - Cancel pending orders (Admin/Manager only)
6. **Manage Payments** - Add payment methods (Admin only)

## 🔒 Security Features

- JWT-based authentication
- Password hashing with bcrypt
- Role-based route guards
- Country-level access control
- GraphQL field-level security

## 📚 Database Schema

The Prisma schema includes:
- **User** - User accounts with roles and country
- **Restaurant** - Restaurants by country
- **MenuItem** - Menu items for restaurants
- **Order** - User orders
- **OrderItem** - Items in orders (junction table)
- **PaymentMethod** - User payment methods

## 🚧 Extension: Relational Access Model (Re-BAC)

For the bonus extension, implement Re-BAC by:
1. Adding relation definitions to Prisma schema
2. Creating a relation evaluation engine
3. Implementing graph-based access control

## 📦 Deployment

### Deploy Backend (Vercel, Heroku, Railway)

```bash
# Build the project
npm run build

# Start production server
npm run start:prod
```

### Deploy Frontend (Vercel, Netlify)

```bash
# Vercel
vercel

# Or Netlify
netlify deploy
```

## 📞 Support

For questions or issues, reach out to **careers@slooze.xyz**

## 📄 License

MIT - See LICENSE file for details

---

**Built with ❤️ for Slooze Careers Challenge**
