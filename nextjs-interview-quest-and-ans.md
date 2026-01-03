# Next.js Interview Questions and Answers

> Based on [roadmap.sh/nextjs](https://roadmap.sh/nextjs) - Comprehensive Interview Preparation Guide  
> Covering App Router, Pages Router, Full-Stack Development, Backend Integration, and More

---

## Table of Contents

1. [Next.js Fundamentals](#nextjs-fundamentals)
2. [App Router (Modern Router)](#app-router-modern-router)
3. [Pages Router](#pages-router)
4. [React Server Components](#react-server-components)
5. [Data Fetching Strategies](#data-fetching-strategies)
6. [Routing and Navigation](#routing-and-navigation)
7. [API Routes](#api-routes)
8. [Database Connections](#database-connections)
9. [ORM and Database Tools](#orm-and-database-tools)
10. [CRUD Operations](#crud-operations)
11. [Database Migrations](#database-migrations)
12. [Authentication](#authentication)
13. [Authorization](#authorization)
14. [Security Practices](#security-practices)
15. [Caching with Redis](#caching-with-redis)
16. [Message Brokers](#message-brokers)
17. [Middleware](#middleware)
18. [Server-Side Rendering (SSR)](#server-side-rendering-ssr)
19. [Static Site Generation (SSG)](#static-site-generation-ssg)
20. [Incremental Static Regeneration (ISR)](#incremental-static-regeneration-isr)
21. [Image Optimization](#image-optimization)
22. [Styling and CSS](#styling-and-css)
23. [TypeScript with Next.js](#typescript-with-nextjs)
24. [Performance Optimization](#performance-optimization)
25. [Error Handling](#error-handling)
26. [Testing](#testing)
27. [Deployment and DevOps](#deployment-and-devops)
28. [Advanced Topics](#advanced-topics)

---

## Next.js Fundamentals

### Q1. What is Next.js, and how does it differ from React?

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Web, Basics

**Answer:**

Next.js is a React framework that provides production-ready features for building full-stack web applications. Unlike React, which is a library for building user interfaces, Next.js extends React with:

**Key Differences:**

1. **Framework vs Library:** React is a library, Next.js is a complete framework
2. **Routing:** Next.js provides file-based routing out of the box
3. **Server-Side Rendering:** Built-in SSR, SSG, and ISR capabilities
4. **API Routes:** Can create backend API endpoints within the same project
5. **Optimizations:** Automatic code splitting, image optimization, font optimization
6. **Zero Configuration:** Works out of the box with sensible defaults

**Example - Basic Next.js App:**

```typescript
// app/page.tsx (App Router)
export default function Home() {
  return (
    <div>
      <h1>Welcome to Next.js</h1>
      <p>This is a server-rendered page</p>
    </div>
  );
}
```

---

### Q2. What are the main features of Next.js?

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Web

**Answer:**

**Core Features:**

1. **File-Based Routing:** Automatic routing based on file structure
2. **Server-Side Rendering (SSR):** Render pages on the server
3. **Static Site Generation (SSG):** Pre-render pages at build time
4. **Incremental Static Regeneration (ISR):** Update static pages without full rebuild
5. **API Routes:** Build backend APIs within Next.js
6. **Image Optimization:** Automatic image optimization with `next/image`
7. **Font Optimization:** Automatic font optimization
8. **Code Splitting:** Automatic code splitting for optimal performance
9. **TypeScript Support:** First-class TypeScript support
10. **Fast Refresh:** Instant feedback during development

---

### Q3. Explain the difference between Next.js Pages Router and App Router.

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, Routing

**Answer:**

**Pages Router (Traditional):**
- Uses `pages` directory
- File-based routing where each file is a route
- Uses `getStaticProps`, `getServerSideProps` for data fetching
- Supports `_app.js` and `_document.js` for customization
- Client Components by default

**App Router (Modern - Next.js 13+):**
- Uses `app` directory
- Supports nested layouts with `layout.tsx`
- Server Components by default
- Direct async data fetching in components
- Route Handlers instead of API routes
- Better support for React Server Components
- Streaming and Suspense support

**Example - Pages Router:**

```typescript
// pages/users/[id].tsx
import { GetServerSideProps } from 'next';

interface UserProps {
  user: { id: string; name: string };
}

export default function User({ user }: UserProps) {
  return <div>{user.name}</div>;
}

export const getServerSideProps: GetServerSideProps = async (context) => {
  const { id } = context.params!;
  // Fetch user data
  return { props: { user: { id, name: 'John' } } };
};
```

**Example - App Router:**

```typescript
// app/users/[id]/page.tsx
interface User {
  id: string;
  name: string;
}

async function getUser(id: string): Promise<User> {
  // Fetch user data
  return { id, name: 'John' };
}

export default async function UserPage({
  params,
}: {
  params: { id: string };
}) {
  const user = await getUser(params.id);
  return <div>{user.name}</div>;
}
```

---

## App Router (Modern Router)

### Q4. How does the App Router work in Next.js?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, Routing, App Router

**Answer:**

The App Router is Next.js's modern routing system introduced in version 13. It uses the `app` directory and React Server Components by default.

**Key Concepts:**

1. **File Conventions:**
   - `page.tsx` - Route segment UI
   - `layout.tsx` - Shared UI for a segment
   - `loading.tsx` - Loading UI
   - `error.tsx` - Error UI
   - `not-found.tsx` - Not found UI
   - `route.ts` - API route handler

2. **Nested Routing:** Folders create URL segments
3. **Layouts:** Shared layouts that persist across navigation
4. **Server Components:** Default rendering on the server

**Example - App Router Structure:**

```
app/
  layout.tsx          // Root layout
  page.tsx            // Home page (/)
  about/
    page.tsx          // About page (/about)
  users/
    layout.tsx        // Users layout
    page.tsx          // Users list (/users)
    [id]/
      page.tsx        // User detail (/users/[id])
```

**Example - Layout with TypeScript:**

```typescript
// app/layout.tsx
import type { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'My App',
  description: 'Next.js App Router Example',
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>
        <header>Navigation</header>
        {children}
        <footer>Footer</footer>
      </body>
    </html>
  );
}
```

---

### Q5. What are React Server Components in the App Router?

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Web, Server-Side Rendering, App Router

**Answer:**

React Server Components (RSC) are components that render exclusively on the server. They're the default in the App Router.

**Benefits:**

1. **Zero Client JavaScript:** No JS sent to client for Server Components
2. **Direct Database Access:** Can directly access databases and APIs
3. **Security:** Keep sensitive tokens and API keys on the server
4. **Performance:** Reduced bundle size and faster initial load
5. **Streaming:** Support for streaming and Suspense

**Server Component Example:**

```typescript
// app/products/page.tsx (Server Component)
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

async function getProducts() {
  return await prisma.product.findMany();
}

export default async function ProductsPage() {
  const products = await getProducts(); // Direct DB access
  
  return (
    <div>
      <h1>Products</h1>
      {products.map((product) => (
        <div key={product.id}>{product.name}</div>
      ))}
    </div>
  );
}
```

**Client Component Example:**

```typescript
// app/components/Counter.tsx
'use client'; // Directive to mark as Client Component

import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

---

### Q6. How do you create dynamic routes in the App Router?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, Routing, App Router

**Answer:**

Dynamic routes in App Router use square brackets `[]` in folder or file names.

**Types of Dynamic Routes:**

1. **Single Dynamic Segment:** `[id]`
2. **Catch-All Routes:** `[...slug]`
3. **Optional Catch-All:** `[[...slug]]`

**Example - Single Dynamic Route:**

```typescript
// app/users/[id]/page.tsx
interface User {
  id: string;
  name: string;
  email: string;
}

async function getUser(id: string): Promise<User> {
  const res = await fetch(`https://api.example.com/users/${id}`);
  return res.json();
}

export default async function UserPage({
  params,
}: {
  params: { id: string };
}) {
  const user = await getUser(params.id);
  
  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
}

// Generate static params for SSG
export async function generateStaticParams() {
  return [
    { id: '1' },
    { id: '2' },
  ];
}
```

**Example - Catch-All Route:**

```typescript
// app/docs/[...slug]/page.tsx
export default function DocsPage({
  params,
}: {
  params: { slug: string[] };
}) {
  const slug = params.slug.join('/');
  return <div>Documentation: {slug}</div>;
}
// Matches: /docs/a, /docs/a/b, /docs/a/b/c, etc.
```

---

## Pages Router

### Q7. How does data fetching work in the Pages Router?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, Data Fetching, Pages Router

**Answer:**

Pages Router uses special functions for data fetching:

1. **`getStaticProps`** - Static Generation (at build time)
2. **`getServerSideProps`** - Server-Side Rendering (on each request)
3. **`getStaticPaths`** - Define dynamic routes for SSG

**Example - getStaticProps (SSG):**

```typescript
// pages/products/[id].tsx
import { GetStaticProps, GetStaticPaths } from 'next';

interface Product {
  id: string;
  name: string;
  price: number;
}

export default function ProductPage({ product }: { product: Product }) {
  return (
    <div>
      <h1>{product.name}</h1>
      <p>${product.price}</p>
    </div>
  );
}

export const getStaticPaths: GetStaticPaths = async () => {
  return {
    paths: [{ params: { id: '1' } }, { params: { id: '2' } }],
    fallback: false, // or 'blocking' or true
  };
};

export const getStaticProps: GetStaticProps = async ({ params }) => {
  const product = await fetchProduct(params!.id as string);
  return {
    props: { product },
    revalidate: 60, // ISR: revalidate every 60 seconds
  };
};
```

**Example - getServerSideProps (SSR):**

```typescript
// pages/users/[id].tsx
import { GetServerSideProps } from 'next';

export const getServerSideProps: GetServerSideProps = async (context) => {
  const { id } = context.params!;
  const user = await fetchUser(id as string);
  
  if (!user) {
    return { notFound: true };
  }
  
  return {
    props: { user },
  };
};
```

---

## API Routes

### Q8. How do you create API routes in Next.js?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Backend, API, I/O Operations

**Answer:**

Next.js supports API routes in both routing systems:

**Pages Router API Routes:**

```typescript
// pages/api/users/route.ts
import type { NextApiRequest, NextApiResponse } from 'next';

type Data = {
  users: User[];
} | {
  error: string;
};

export default async function handler(
  req: NextApiRequest,
  res: NextApiResponse<Data>
) {
  if (req.method === 'GET') {
    const users = await getUsers();
    res.status(200).json({ users });
  } else if (req.method === 'POST') {
    const user = await createUser(req.body);
    res.status(201).json({ user });
  } else {
    res.status(405).json({ error: 'Method not allowed' });
  }
}
```

**App Router Route Handlers:**

```typescript
// app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET() {
  const users = await getUsers();
  return NextResponse.json({ users });
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  const user = await createUser(body);
  return NextResponse.json({ user }, { status: 201 });
}
```

**Example - Full CRUD with TypeScript:**

```typescript
// app/api/users/[id]/route.ts
import { NextRequest, NextResponse } from 'next/server';
import prisma from '@/lib/prisma';

export async function GET(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const user = await prisma.user.findUnique({
    where: { id: params.id },
  });
  
  if (!user) {
    return NextResponse.json({ error: 'User not found' }, { status: 404 });
  }
  
  return NextResponse.json(user);
}

export async function PUT(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const body = await request.json();
  const user = await prisma.user.update({
    where: { id: params.id },
    data: body,
  });
  return NextResponse.json(user);
}

export async function DELETE(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  await prisma.user.delete({
    where: { id: params.id },
  });
  return NextResponse.json({ message: 'User deleted' });
}
```

---

## Database Connections

### Q9. How do you connect Next.js to a PostgreSQL database?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Database, I/O Operations

**Answer:**

**Using Prisma ORM (Recommended):**

```typescript
// lib/prisma.ts
import { PrismaClient } from '@prisma/client';

const globalForPrisma = globalThis as unknown as {
  prisma: PrismaClient | undefined;
};

export const prisma = globalForPrisma.prisma ?? new PrismaClient({
  log: ['query', 'error', 'warn'],
});

if (process.env.NODE_ENV !== 'production') {
  globalForPrisma.prisma = prisma;
}
```

**Using Raw PostgreSQL Client:**

```typescript
// lib/db.ts
import { Pool } from 'pg';

const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  ssl: process.env.NODE_ENV === 'production' ? { rejectUnauthorized: false } : false,
});

export default pool;
```

**Example - Using Prisma in API Route:**

```typescript
// app/api/users/route.ts
import { NextResponse } from 'next/server';
import prisma from '@/lib/prisma';

export async function GET() {
  try {
    const users = await prisma.user.findMany({
      include: { posts: true },
    });
    return NextResponse.json(users);
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to fetch users' },
      { status: 500 }
    );
  }
}
```

---

### Q10. How do you connect Next.js to MongoDB?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Database, I/O Operations

**Answer:**

**Using Mongoose:**

```typescript
// lib/mongodb.ts
import mongoose from 'mongoose';

const MONGODB_URI = process.env.MONGODB_URI!;

if (!MONGODB_URI) {
  throw new Error('Please define MONGODB_URI in .env.local');
}

interface MongooseCache {
  conn: typeof mongoose | null;
  promise: Promise<typeof mongoose> | null;
}

declare global {
  var mongoose: MongooseCache | undefined;
}

let cached: MongooseCache = global.mongoose || { conn: null, promise: null };

if (!global.mongoose) {
  global.mongoose = cached;
}

async function connectDB() {
  if (cached.conn) {
    return cached.conn;
  }

  if (!cached.promise) {
    cached.promise = mongoose.connect(MONGODB_URI).then((mongoose) => {
      return mongoose;
    });
  }

  cached.conn = await cached.promise;
  return cached.conn;
}

export default connectDB;
```

**Example - User Model:**

```typescript
// models/User.ts
import mongoose, { Schema, Document } from 'mongoose';

interface IUser extends Document {
  name: string;
  email: string;
  createdAt: Date;
}

const UserSchema = new Schema<IUser>({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  createdAt: { type: Date, default: Date.now },
});

export default mongoose.models.User || mongoose.model<IUser>('User', UserSchema);
```

**Example - Using in API Route:**

```typescript
// app/api/users/route.ts
import { NextResponse } from 'next/server';
import connectDB from '@/lib/mongodb';
import User from '@/models/User';

export async function GET() {
  await connectDB();
  const users = await User.find({});
  return NextResponse.json(users);
}
```

---

## ORM and Database Tools

### Q11. How do you use Prisma ORM in Next.js?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Database, ORM

**Answer:**

**Setup Prisma:**

```bash
npm install prisma @prisma/client
npx prisma init
```

**Prisma Schema:**

```prisma
// prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        String   @id @default(cuid())
  email     String   @unique
  name      String?
  posts     Post[]
  createdAt DateTime @default(now())
}

model Post {
  id        String   @id @default(cuid())
  title     String
  content   String?
  published Boolean  @default(false)
  author    User     @relation(fields: [authorId], references: [id])
  authorId  String
  createdAt DateTime @default(now())
}
```

**Prisma Client Instance:**

```typescript
// lib/prisma.ts
import { PrismaClient } from '@prisma/client';

const prismaClientSingleton = () => {
  return new PrismaClient();
};

declare global {
  var prisma: undefined | ReturnType<typeof prismaClientSingleton>;
}

const prisma = globalThis.prisma ?? prismaClientSingleton();

export default prisma;

if (process.env.NODE_ENV !== 'production') globalThis.prisma = prisma;
```

**Example - CRUD Operations:**

```typescript
// app/api/users/route.ts
import { NextResponse } from 'next/server';
import prisma from '@/lib/prisma';

// Create
export async function POST(request: Request) {
  const body = await request.json();
  const user = await prisma.user.create({
    data: {
      email: body.email,
      name: body.name,
    },
  });
  return NextResponse.json(user, { status: 201 });
}

// Read All
export async function GET() {
  const users = await prisma.user.findMany({
    include: { posts: true },
  });
  return NextResponse.json(users);
}
```

---

### Q12. How do you use TypeORM in Next.js?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Database, ORM

**Answer:**

**Setup TypeORM:**

```typescript
// lib/typeorm.ts
import { DataSource } from 'typeorm';
import { User } from '@/entities/User';
import { Post } from '@/entities/Post';

let AppDataSource: DataSource | null = null;

export async function getDataSource(): Promise<DataSource> {
  if (AppDataSource?.isInitialized) {
    return AppDataSource;
  }

  AppDataSource = new DataSource({
    type: 'postgres',
    url: process.env.DATABASE_URL,
    entities: [User, Post],
    synchronize: process.env.NODE_ENV !== 'production',
  });

  await AppDataSource.initialize();
  return AppDataSource;
}
```

**Entity Definition:**

```typescript
// entities/User.ts
import { Entity, PrimaryGeneratedColumn, Column, OneToMany } from 'typeorm';
import { Post } from './Post';

@Entity()
export class User {
  @PrimaryGeneratedColumn('uuid')
  id!: string;

  @Column()
  email!: string;

  @Column({ nullable: true })
  name?: string;

  @OneToMany(() => Post, (post) => post.author)
  posts!: Post[];
}
```

---

## CRUD Operations

### Q13. How do you implement CRUD operations using static JSON files?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Backend, CRUD, I/O Operations

**Answer:**

**Read JSON File:**

```typescript
// lib/data.ts
import fs from 'fs/promises';
import path from 'path';

const dataFilePath = path.join(process.cwd(), 'data', 'users.json');

export async function getUsers(): Promise<User[]> {
  const fileContents = await fs.readFile(dataFilePath, 'utf8');
  return JSON.parse(fileContents);
}

export async function saveUsers(users: User[]): Promise<void> {
  await fs.writeFile(dataFilePath, JSON.stringify(users, null, 2));
}
```

**CRUD API Routes:**

```typescript
// app/api/users/route.ts
import { NextResponse } from 'next/server';
import { getUsers, saveUsers } from '@/lib/data';

// GET - Read all
export async function GET() {
  const users = await getUsers();
  return NextResponse.json(users);
}

// POST - Create
export async function POST(request: Request) {
  const body = await request.json();
  const users = await getUsers();
  
  const newUser = {
    id: Date.now().toString(),
    ...body,
    createdAt: new Date().toISOString(),
  };
  
  users.push(newUser);
  await saveUsers(users);
  
  return NextResponse.json(newUser, { status: 201 });
}
```

**Update and Delete:**

```typescript
// app/api/users/[id]/route.ts
import { NextResponse } from 'next/server';
import { getUsers, saveUsers } from '@/lib/data';

// PUT - Update
export async function PUT(
  request: Request,
  { params }: { params: { id: string } }
) {
  const body = await request.json();
  const users = await getUsers();
  
  const index = users.findIndex((u) => u.id === params.id);
  if (index === -1) {
    return NextResponse.json({ error: 'Not found' }, { status: 404 });
  }
  
  users[index] = { ...users[index], ...body };
  await saveUsers(users);
  
  return NextResponse.json(users[index]);
}

// DELETE
export async function DELETE(
  request: Request,
  { params }: { params: { id: string } }
) {
  const users = await getUsers();
  const filtered = users.filter((u) => u.id !== params.id);
  
  if (users.length === filtered.length) {
    return NextResponse.json({ error: 'Not found' }, { status: 404 });
  }
  
  await saveUsers(filtered);
  return NextResponse.json({ message: 'Deleted' });
}
```

---

### Q14. How do you implement CRUD operations with a database using Prisma?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Database, CRUD, ORM

**Answer:**

**Complete CRUD Example:**

```typescript
// app/api/posts/route.ts
import { NextResponse } from 'next/server';
import prisma from '@/lib/prisma';

// GET - Read all
export async function GET() {
  try {
    const posts = await prisma.post.findMany({
      include: { author: true },
      orderBy: { createdAt: 'desc' },
    });
    return NextResponse.json(posts);
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to fetch posts' },
      { status: 500 }
    );
  }
}

// POST - Create
export async function POST(request: Request) {
  try {
    const body = await request.json();
    const post = await prisma.post.create({
      data: {
        title: body.title,
        content: body.content,
        authorId: body.authorId,
      },
      include: { author: true },
    });
    return NextResponse.json(post, { status: 201 });
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to create post' },
      { status: 500 }
    );
  }
}
```

**Update and Delete:**

```typescript
// app/api/posts/[id]/route.ts
import { NextResponse } from 'next/server';
import prisma from '@/lib/prisma';

// GET - Read one
export async function GET(
  request: Request,
  { params }: { params: { id: string } }
) {
  try {
    const post = await prisma.post.findUnique({
      where: { id: params.id },
      include: { author: true },
    });
    
    if (!post) {
      return NextResponse.json({ error: 'Post not found' }, { status: 404 });
    }
    
    return NextResponse.json(post);
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to fetch post' },
      { status: 500 }
    );
  }
}

// PUT - Update
export async function PUT(
  request: Request,
  { params }: { params: { id: string } }
) {
  try {
    const body = await request.json();
    const post = await prisma.post.update({
      where: { id: params.id },
      data: {
        title: body.title,
        content: body.content,
        published: body.published,
      },
    });
    return NextResponse.json(post);
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to update post' },
      { status: 500 }
    );
  }
}

// DELETE
export async function DELETE(
  request: Request,
  { params }: { params: { id: string } }
) {
  try {
    await prisma.post.delete({
      where: { id: params.id },
    });
    return NextResponse.json({ message: 'Post deleted' });
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to delete post' },
      { status: 500 }
    );
  }
}
```

---

## Database Migrations

### Q15. How do you handle database migrations in Next.js with Prisma?

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Backend, Database, Migrations

**Answer:**

**Prisma Migrations:**

```bash
# Create migration
npx prisma migrate dev --name add_user_table

# Apply migrations in production
npx prisma migrate deploy

# Reset database
npx prisma migrate reset
```

**Migration Script:**

```typescript
// scripts/migrate.ts
import { execSync } from 'child_process';

const runMigrations = () => {
  try {
    execSync('npx prisma migrate deploy', { stdio: 'inherit' });
    console.log('Migrations applied successfully');
  } catch (error) {
    console.error('Migration failed:', error);
    process.exit(1);
  }
};

runMigrations();
```

**Example Migration:**

```prisma
// After schema change, Prisma generates:
// prisma/migrations/20240101000000_add_user_table/migration.sql

CREATE TABLE "User" (
  "id" TEXT NOT NULL,
  "email" TEXT NOT NULL,
  "name" TEXT,
  "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT "User_pkey" PRIMARY KEY ("id")
);

CREATE UNIQUE INDEX "User_email_key" ON "User"("email");
```

**Using in Production:**

```json
// package.json
{
  "scripts": {
    "migrate": "prisma migrate deploy",
    "postinstall": "prisma generate"
  }
}
```

---

## Authentication

### Q16. How do you implement authentication in Next.js using NextAuth.js?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Authentication, Security

**Answer:**

**Setup NextAuth.js:**

```bash
npm install next-auth
```

**NextAuth Configuration:**

```typescript
// app/api/auth/[...nextauth]/route.ts
import NextAuth from 'next-auth';
import CredentialsProvider from 'next-auth/providers/credentials';
import { PrismaAdapter } from '@next-auth/prisma-adapter';
import prisma from '@/lib/prisma';

export const authOptions = {
  adapter: PrismaAdapter(prisma),
  providers: [
    CredentialsProvider({
      name: 'Credentials',
      credentials: {
        email: { label: 'Email', type: 'email' },
        password: { label: 'Password', type: 'password' },
      },
      async authorize(credentials) {
        if (!credentials?.email || !credentials?.password) {
          return null;
        }
        
        const user = await prisma.user.findUnique({
          where: { email: credentials.email },
        });
        
        if (!user) return null;
        
        // Verify password (use bcrypt in production)
        const isValid = await verifyPassword(credentials.password, user.password);
        if (!isValid) return null;
        
        return {
          id: user.id,
          email: user.email,
          name: user.name,
        };
      },
    }),
  ],
  session: {
    strategy: 'jwt',
  },
  pages: {
    signIn: '/auth/signin',
  },
  callbacks: {
    async jwt({ token, user }) {
      if (user) {
        token.id = user.id;
      }
      return token;
    },
    async session({ session, token }) {
      if (session.user) {
        session.user.id = token.id as string;
      }
      return session;
    },
  },
};

const handler = NextAuth(authOptions);
export { handler as GET, handler as POST };
```

**Using in Server Components:**

```typescript
// app/profile/page.tsx
import { getServerSession } from 'next-auth';
import { authOptions } from '@/app/api/auth/[...nextauth]/route';
import { redirect } from 'next/navigation';

export default async function ProfilePage() {
  const session = await getServerSession(authOptions);
  
  if (!session) {
    redirect('/auth/signin');
  }
  
  return (
    <div>
      <h1>Profile</h1>
      <p>Email: {session.user?.email}</p>
    </div>
  );
}
```

**Using in Client Components:**

```typescript
// app/components/UserMenu.tsx
'use client';

import { useSession, signIn, signOut } from 'next-auth/react';

export default function UserMenu() {
  const { data: session, status } = useSession();
  
  if (status === 'loading') return <div>Loading...</div>;
  
  if (session) {
    return (
      <div>
        <p>Signed in as {session.user?.email}</p>
        <button onClick={() => signOut()}>Sign out</button>
      </div>
    );
  }
  
  return <button onClick={() => signIn()}>Sign in</button>;
}
```

---

### Q17. How do you implement JWT authentication manually in Next.js?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Authentication, Security

**Answer:**

**JWT Utilities:**

```typescript
// lib/jwt.ts
import jwt from 'jsonwebtoken';

const JWT_SECRET = process.env.JWT_SECRET!;

export function signToken(payload: { userId: string; email: string }): string {
  return jwt.sign(payload, JWT_SECRET, { expiresIn: '7d' });
}

export function verifyToken(token: string): { userId: string; email: string } | null {
  try {
    return jwt.verify(token, JWT_SECRET) as { userId: string; email: string };
  } catch {
    return null;
  }
}
```

**Login API Route:**

```typescript
// app/api/auth/login/route.ts
import { NextResponse } from 'next/server';
import { signToken } from '@/lib/jwt';
import prisma from '@/lib/prisma';
import bcrypt from 'bcryptjs';

export async function POST(request: Request) {
  const { email, password } = await request.json();
  
  const user = await prisma.user.findUnique({
    where: { email },
  });
  
  if (!user) {
    return NextResponse.json(
      { error: 'Invalid credentials' },
      { status: 401 }
    );
  }
  
  const isValid = await bcrypt.compare(password, user.password);
  if (!isValid) {
    return NextResponse.json(
      { error: 'Invalid credentials' },
      { status: 401 }
    );
  }
  
  const token = signToken({ userId: user.id, email: user.email });
  
  const response = NextResponse.json({ user: { id: user.id, email: user.email } });
  response.cookies.set('token', token, {
    httpOnly: true,
    secure: process.env.NODE_ENV === 'production',
    sameSite: 'lax',
    maxAge: 60 * 60 * 24 * 7, // 7 days
  });
  
  return response;
}
```

**Middleware for Protected Routes:**

```typescript
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';
import { verifyToken } from '@/lib/jwt';

export function middleware(request: NextRequest) {
  const token = request.cookies.get('token')?.value;
  
  if (!token) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  
  const payload = verifyToken(token);
  if (!payload) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  
  return NextResponse.next();
}

export const config = {
  matcher: ['/dashboard/:path*', '/profile/:path*'],
};
```

---

## Authorization

### Q18. How do you implement role-based access control (RBAC) in Next.js?

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Backend, Authorization, Security

**Answer:**

**User Model with Roles:**

```typescript
// prisma/schema.prisma
enum Role {
  USER
  ADMIN
  MODERATOR
}

model User {
  id        String   @id @default(cuid())
  email     String   @unique
  role      Role     @default(USER)
  // ...
}
```

**Authorization Middleware:**

```typescript
// lib/auth.ts
import { getServerSession } from 'next-auth';
import { authOptions } from '@/app/api/auth/[...nextauth]/route';
import { redirect } from 'next/navigation';
import prisma from '@/lib/prisma';

export async function requireAuth() {
  const session = await getServerSession(authOptions);
  if (!session) {
    redirect('/login');
  }
  return session;
}

export async function requireRole(allowedRoles: string[]) {
  const session = await requireAuth();
  const user = await prisma.user.findUnique({
    where: { id: session.user.id },
  });
  
  if (!user || !allowedRoles.includes(user.role)) {
    redirect('/unauthorized');
  }
  
  return { session, user };
}
```

**Using in Pages:**

```typescript
// app/admin/page.tsx
import { requireRole } from '@/lib/auth';

export default async function AdminPage() {
  const { user } = await requireRole(['ADMIN']);
  
  return (
    <div>
      <h1>Admin Dashboard</h1>
      <p>Welcome, {user.email}</p>
    </div>
  );
}
```

**API Route Protection:**

```typescript
// app/api/admin/users/route.ts
import { NextResponse } from 'next/server';
import { requireRole } from '@/lib/auth';

export async function GET() {
  const { user } = await requireRole(['ADMIN']);
  
  const users = await prisma.user.findMany();
  return NextResponse.json(users);
}
```

---

## Security Practices

### Q19. What are the security best practices for Next.js applications?

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Backend, Security, Best Practices

**Answer:**

**1. Environment Variables:**

```typescript
// .env.local (never commit)
DATABASE_URL=postgresql://...
JWT_SECRET=your-secret-key
NEXT_PUBLIC_API_URL=https://api.example.com

// Use NEXT_PUBLIC_ prefix only for client-side variables
```

**2. Input Validation:**

```typescript
// lib/validation.ts
import { z } from 'zod';

export const userSchema = z.object({
  email: z.string().email(),
  name: z.string().min(1).max(100),
  age: z.number().int().min(0).max(120),
});

// In API route
export async function POST(request: Request) {
  const body = await request.json();
  const validated = userSchema.parse(body); // Throws if invalid
  // Use validated data
}
```

**3. SQL Injection Prevention (with Prisma):**

```typescript
// ✅ Safe - Prisma handles escaping
const user = await prisma.user.findUnique({
  where: { email: userInput },
});

// ❌ Never do this with raw queries
// const query = `SELECT * FROM users WHERE email = '${userInput}'`;
```

**4. XSS Prevention:**

```typescript
// Use React's built-in escaping (default)
<div>{userContent}</div>

// For HTML content, sanitize
import DOMPurify from 'isomorphic-dompurify';

<div dangerouslySetInnerHTML={{
  __html: DOMPurify.sanitize(userContent)
}} />
```

**5. CSRF Protection:**

```typescript
// Use SameSite cookies
response.cookies.set('token', token, {
  httpOnly: true,
  secure: true,
  sameSite: 'strict',
});
```

**6. Rate Limiting:**

```typescript
// lib/rate-limit.ts
import { LRUCache } from 'lru-cache';

const rateLimit = new LRUCache({
  max: 500,
  ttl: 60000, // 1 minute
});

export function checkRateLimit(identifier: string): boolean {
  const count = rateLimit.get(identifier) as number || 0;
  if (count >= 10) {
    return false;
  }
  rateLimit.set(identifier, count + 1);
  return true;
}
```

**7. Content Security Policy:**

```typescript
// next.config.js
module.exports = {
  async headers() {
    return [
      {
        source: '/:path*',
        headers: [
          {
            key: 'Content-Security-Policy',
            value: "default-src 'self'; script-src 'self' 'unsafe-eval' 'unsafe-inline';",
          },
        ],
      },
    ];
  },
};
```

---

## Caching with Redis

### Q20. How do you integrate Redis caching in Next.js?

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Backend, Caching, Redis, I/O Operations

**Answer:**

**Setup Redis Client:**

```typescript
// lib/redis.ts
import { createClient } from 'redis';

const redisClient = createClient({
  url: process.env.REDIS_URL || 'redis://localhost:6379',
});

redisClient.on('error', (err) => console.error('Redis Client Error', err));

if (!redisClient.isOpen) {
  await redisClient.connect();
}

export default redisClient;
```

**Caching Utility:**

```typescript
// lib/cache.ts
import redisClient from './redis';

export async function getCache<T>(key: string): Promise<T | null> {
  try {
    const data = await redisClient.get(key);
    return data ? JSON.parse(data) : null;
  } catch (error) {
    console.error('Cache get error:', error);
    return null;
  }
}

export async function setCache(
  key: string,
  value: any,
  ttl: number = 3600
): Promise<void> {
  try {
    await redisClient.setEx(key, ttl, JSON.stringify(value));
  } catch (error) {
    console.error('Cache set error:', error);
  }
}

export async function deleteCache(key: string): Promise<void> {
  try {
    await redisClient.del(key);
  } catch (error) {
    console.error('Cache delete error:', error);
  }
}
```

**Using in API Routes:**

```typescript
// app/api/posts/route.ts
import { NextResponse } from 'next/server';
import { getCache, setCache } from '@/lib/cache';
import prisma from '@/lib/prisma';

export async function GET() {
  const cacheKey = 'posts:all';
  
  // Try cache first
  const cached = await getCache(cacheKey);
  if (cached) {
    return NextResponse.json(cached);
  }
  
  // Fetch from database
  const posts = await prisma.post.findMany({
    orderBy: { createdAt: 'desc' },
  });
  
  // Cache for 5 minutes
  await setCache(cacheKey, posts, 300);
  
  return NextResponse.json(posts);
}
```

**Cache Invalidation:**

```typescript
// app/api/posts/route.ts
export async function POST(request: Request) {
  const body = await request.json();
  const post = await prisma.post.create({ data: body });
  
  // Invalidate cache
  await deleteCache('posts:all');
  
  return NextResponse.json(post, { status: 201 });
}
```

**Next.js Built-in Caching:**

```typescript
// App Router - fetch caching
export default async function Page() {
  // This is cached by default
  const res = await fetch('https://api.example.com/data', {
    next: { revalidate: 3600 }, // Revalidate every hour
  });
  
  const data = await res.json();
  return <div>{data}</div>;
}
```

---

## Message Brokers

### Q21. How do you integrate RabbitMQ with Next.js?

**Difficulty:** Advanced  
**Role:** Architect  
**Tags:** Programming, Backend, Message Broker, RabbitMQ, I/O Operations

**Answer:**

**Setup RabbitMQ Client:**

```typescript
// lib/rabbitmq.ts
import amqp from 'amqplib';

let connection: amqp.Connection | null = null;
let channel: amqp.Channel | null = null;

export async function connectRabbitMQ() {
  if (connection) return { connection, channel: channel! };
  
  connection = await amqp.connect(process.env.RABBITMQ_URL || 'amqp://localhost');
  channel = await connection.createChannel();
  
  return { connection, channel };
}

export async function publishMessage(
  queue: string,
  message: any
): Promise<void> {
  const { channel } = await connectRabbitMQ();
  await channel.assertQueue(queue, { durable: true });
  channel.sendToQueue(queue, Buffer.from(JSON.stringify(message)), {
    persistent: true,
  });
}

export async function consumeMessages(
  queue: string,
  callback: (message: any) => Promise<void>
): Promise<void> {
  const { channel } = await connectRabbitMQ();
  await channel.assertQueue(queue, { durable: true });
  channel.prefetch(1);
  
  channel.consume(queue, async (msg) => {
    if (msg) {
      const content = JSON.parse(msg.content.toString());
      await callback(content);
      channel.ack(msg);
    }
  });
}
```

**Using in API Route:**

```typescript
// app/api/notifications/send/route.ts
import { NextResponse } from 'next/server';
import { publishMessage } from '@/lib/rabbitmq';

export async function POST(request: Request) {
  const { userId, message } = await request.json();
  
  // Publish to queue
  await publishMessage('notifications', {
    userId,
    message,
    timestamp: new Date().toISOString(),
  });
  
  return NextResponse.json({ success: true });
}
```

**Worker Process:**

```typescript
// workers/notification-worker.ts
import { consumeMessages } from '@/lib/rabbitmq';

async function processNotification(message: any) {
  console.log('Processing notification:', message);
  // Send email, push notification, etc.
}

consumeMessages('notifications', processNotification);
```

---

### Q22. How do you integrate Apache Kafka with Next.js?

**Difficulty:** Advanced  
**Role:** Architect  
**Tags:** Programming, Backend, Message Broker, Kafka, I/O Operations

**Answer:**

**Setup Kafka Client:**

```typescript
// lib/kafka.ts
import { Kafka } from 'kafkajs';

const kafka = new Kafka({
  clientId: 'nextjs-app',
  brokers: [process.env.KAFKA_BROKER || 'localhost:9092'],
});

export const producer = kafka.producer();
export const consumer = kafka.consumer({ groupId: 'nextjs-group' });

export async function connectKafka() {
  await producer.connect();
  await consumer.connect();
}

export async function publishEvent(
  topic: string,
  event: any
): Promise<void> {
  await producer.send({
    topic,
    messages: [
      {
        key: event.id,
        value: JSON.stringify(event),
      },
    ],
  });
}
```

**Using in API Route:**

```typescript
// app/api/events/publish/route.ts
import { NextResponse } from 'next/server';
import { publishEvent } from '@/lib/kafka';

export async function POST(request: Request) {
  const event = await request.json();
  
  await publishEvent('user-events', {
    ...event,
    timestamp: new Date().toISOString(),
  });
  
  return NextResponse.json({ success: true });
}
```

---

## Middleware

### Q23. How do you use Next.js middleware?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Backend, Middleware, Web

**Answer:**

**Basic Middleware:**

```typescript
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  // Add custom header
  const response = NextResponse.next();
  response.headers.set('x-custom-header', 'custom-value');
  return response;
}

export const config = {
  matcher: '/:path*',
};
```

**Authentication Middleware:**

```typescript
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';
import { verifyToken } from '@/lib/jwt';

export function middleware(request: NextRequest) {
  const token = request.cookies.get('token')?.value;
  
  // Public routes
  if (request.nextUrl.pathname.startsWith('/login')) {
    if (token) {
      return NextResponse.redirect(new URL('/dashboard', request.url));
    }
    return NextResponse.next();
  }
  
  // Protected routes
  if (!token) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  
  const payload = verifyToken(token);
  if (!payload) {
    const response = NextResponse.redirect(new URL('/login', request.url));
    response.cookies.delete('token');
    return response;
  }
  
  return NextResponse.next();
}

export const config = {
  matcher: ['/dashboard/:path*', '/api/protected/:path*'],
};
```

**Localization Middleware:**

```typescript
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

const locales = ['en', 'fr', 'es'];

export function middleware(request: NextRequest) {
  const pathname = request.nextUrl.pathname;
  const pathnameHasLocale = locales.some(
    (locale) => pathname.startsWith(`/${locale}/`) || pathname === `/${locale}`
  );
  
  if (pathnameHasLocale) return NextResponse.next();
  
  const locale = request.headers.get('accept-language')?.split(',')[0] || 'en';
  const newUrl = new URL(`/${locale}${pathname}`, request.url);
  return NextResponse.redirect(newUrl);
}

export const config = {
  matcher: ['/((?!api|_next|_vercel|.*\\..*).*)'],
};
```

---

## Server-Side Rendering (SSR)

### Q24. How does Server-Side Rendering work in Next.js?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, Server-Side Rendering

**Answer:**

**App Router SSR (Default):**

```typescript
// app/products/page.tsx
async function getProducts() {
  const res = await fetch('https://api.example.com/products', {
    cache: 'no-store', // Force SSR
  });
  return res.json();
}

export default async function ProductsPage() {
  const products = await getProducts(); // Runs on server
  
  return (
    <div>
      <h1>Products</h1>
      {products.map((product) => (
        <div key={product.id}>{product.name}</div>
      ))}
    </div>
  );
}
```

**Pages Router SSR:**

```typescript
// pages/products.tsx
import { GetServerSideProps } from 'next';

interface ProductsPageProps {
  products: Product[];
}

export default function ProductsPage({ products }: ProductsPageProps) {
  return (
    <div>
      <h1>Products</h1>
      {products.map((product) => (
        <div key={product.id}>{product.name}</div>
      ))}
    </div>
  );
}

export const getServerSideProps: GetServerSideProps = async (context) => {
  const res = await fetch('https://api.example.com/products');
  const products = await res.json();
  
  return {
    props: { products },
  };
};
```

**Benefits of SSR:**

1. **SEO:** Search engines can crawl fully rendered HTML
2. **Performance:** Faster initial page load
3. **Security:** Sensitive data stays on server
4. **Social Sharing:** Proper meta tags for social media

---

## Static Site Generation (SSG)

### Q25. How does Static Site Generation work in Next.js?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, Static Site Generation

**Answer:**

**App Router SSG:**

```typescript
// app/posts/page.tsx
async function getPosts() {
  const res = await fetch('https://api.example.com/posts', {
    next: { revalidate: 3600 }, // ISR: revalidate every hour
  });
  return res.json();
}

export default async function PostsPage() {
  const posts = await getPosts();
  
  return (
    <div>
      {posts.map((post) => (
        <div key={post.id}>{post.title}</div>
      ))}
    </div>
  );
}
```

**Pages Router SSG:**

```typescript
// pages/posts.tsx
import { GetStaticProps } from 'next';

export default function PostsPage({ posts }: { posts: Post[] }) {
  return (
    <div>
      {posts.map((post) => (
        <div key={post.id}>{post.title}</div>
      ))}
    </div>
  );
}

export const getStaticProps: GetStaticProps = async () => {
  const posts = await fetchPosts();
  
  return {
    props: { posts },
    revalidate: 3600, // ISR: revalidate every hour
  };
};
```

**Benefits of SSG:**

1. **Performance:** Fastest possible page loads
2. **CDN Friendly:** Can be served from CDN
3. **Cost Effective:** No server computation needed
4. **Reliability:** No server failures

---

## Incremental Static Regeneration (ISR)

### Q26. What is Incremental Static Regeneration and how does it work?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Web, Static Site Generation, ISR

**Answer:**

ISR allows you to update static pages after build without rebuilding the entire site.

**App Router ISR:**

```typescript
// app/products/[id]/page.tsx
async function getProduct(id: string) {
  const res = await fetch(`https://api.example.com/products/${id}`, {
    next: { revalidate: 60 }, // Revalidate every 60 seconds
  });
  return res.json();
}

export default async function ProductPage({
  params,
}: {
  params: { id: string };
}) {
  const product = await getProduct(params.id);
  return <div>{product.name}</div>;
}

export async function generateStaticParams() {
  const products = await fetch('https://api.example.com/products').then(
    (res) => res.json()
  );
  
  return products.map((product: Product) => ({
    id: product.id.toString(),
  }));
}
```

**Pages Router ISR:**

```typescript
// pages/products/[id].tsx
export const getStaticProps: GetStaticProps = async ({ params }) => {
  const product = await fetchProduct(params!.id as string);
  
  return {
    props: { product },
    revalidate: 60, // Revalidate every 60 seconds
  };
};

export const getStaticPaths: GetStaticPaths = async () => {
  return {
    paths: [],
    fallback: 'blocking', // Generate on-demand
  };
};
```

**On-Demand Revalidation:**

```typescript
// app/api/revalidate/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { revalidatePath } from 'next/cache';

export async function POST(request: NextRequest) {
  const { path, secret } = await request.json();
  
  if (secret !== process.env.REVALIDATION_SECRET) {
    return NextResponse.json({ error: 'Invalid secret' }, { status: 401 });
  }
  
  revalidatePath(path);
  return NextResponse.json({ revalidated: true });
}
```

---

## Image Optimization

### Q27. How does Next.js optimize images?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, Image Optimization

**Answer:**

**Using next/image:**

```typescript
// app/components/OptimizedImage.tsx
import Image from 'next/image';

export default function OptimizedImage() {
  return (
    <Image
      src="/hero.jpg"
      alt="Hero image"
      width={800}
      height={600}
      priority // Load immediately
      placeholder="blur" // Show blur while loading
      blurDataURL="data:image/jpeg;base64,..."
    />
  );
}
```

**Remote Images:**

```typescript
// next.config.js
module.exports = {
  images: {
    remotePatterns: [
      {
        protocol: 'https',
        hostname: 'example.com',
        pathname: '/images/**',
      },
    ],
  },
};
```

**Benefits:**

1. **Automatic Format Selection:** Serves WebP/AVIF when supported
2. **Responsive Images:** Serves appropriate sizes
3. **Lazy Loading:** Loads images as they enter viewport
4. **Blur Placeholder:** Shows placeholder while loading

---

## Styling and CSS

### Q28. What styling options are available in Next.js?

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Web, Styling, CSS

**Answer:**

**1. CSS Modules:**

```typescript
// app/components/Button.module.css
.button {
  background: blue;
  color: white;
  padding: 10px 20px;
}

// app/components/Button.tsx
import styles from './Button.module.css';

export default function Button() {
  return <button className={styles.button}>Click me</button>;
}
```

**2. Tailwind CSS:**

```typescript
// app/page.tsx
export default function Home() {
  return (
    <div className="flex items-center justify-center min-h-screen">
      <h1 className="text-4xl font-bold">Hello World</h1>
    </div>
  );
}
```

**3. Styled Components:**

```typescript
// app/components/StyledButton.tsx
'use client';

import styled from 'styled-components';

const Button = styled.button`
  background: blue;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
`;

export default Button;
```

**4. Global CSS:**

```typescript
// app/globals.css
body {
  margin: 0;
  font-family: system-ui;
}

// app/layout.tsx
import './globals.css';
```

---

## TypeScript with Next.js

### Q29. How do you use TypeScript effectively in Next.js?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, TypeScript

**Answer:**

**TypeScript Configuration:**

```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "plugins": [
      {
        "name": "next"
      }
    ],
    "paths": {
      "@/*": ["./*"]
    }
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx", ".next/types/**/*.ts"],
  "exclude": ["node_modules"]
}
```

**Typed API Routes:**

```typescript
// app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';

interface User {
  id: string;
  name: string;
  email: string;
}

interface ErrorResponse {
  error: string;
}

export async function GET(): Promise<NextResponse<User[] | ErrorResponse>> {
  try {
    const users: User[] = await getUsers();
    return NextResponse.json(users);
  } catch (error) {
    return NextResponse.json(
      { error: 'Failed to fetch users' },
      { status: 500 }
    );
  }
}
```

**Typed Server Components:**

```typescript
// app/users/[id]/page.tsx
interface UserPageProps {
  params: {
    id: string;
  };
}

interface User {
  id: string;
  name: string;
  email: string;
}

export default async function UserPage({ params }: UserPageProps) {
  const user: User = await getUser(params.id);
  return <div>{user.name}</div>;
}
```

**Type Safety with Prisma:**

```typescript
// lib/prisma.ts
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

export type User = {
  id: string;
  email: string;
  name: string | null;
};

export default prisma;
```

---

## Performance Optimization

### Q30. How do you optimize Next.js applications for performance?

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Web, Performance, Optimization

**Answer:**

**1. Code Splitting:**

```typescript
// Dynamic imports
import dynamic from 'next/dynamic';

const HeavyComponent = dynamic(() => import('./HeavyComponent'), {
  loading: () => <p>Loading...</p>,
  ssr: false, // Disable SSR if needed
});
```

**2. Image Optimization:**

```typescript
import Image from 'next/image';

<Image
  src="/image.jpg"
  alt="Description"
  width={500}
  height={300}
  loading="lazy"
  quality={75}
/>
```

**3. Font Optimization:**

```typescript
// app/layout.tsx
import { Inter } from 'next/font/google';

const inter = Inter({ subsets: ['latin'] });

export default function RootLayout({ children }) {
  return (
    <html className={inter.className}>
      <body>{children}</body>
    </html>
  );
}
```

**4. Bundle Analysis:**

```bash
npm install @next/bundle-analyzer
```

```javascript
// next.config.js
const withBundleAnalyzer = require('@next/bundle-analyzer')({
  enabled: process.env.ANALYZE === 'true',
});

module.exports = withBundleAnalyzer({});
```

**5. Caching Strategies:**

```typescript
// Cache API responses
const res = await fetch(url, {
  next: { revalidate: 3600 }, // Cache for 1 hour
});
```

---

## Error Handling

### Q31. How do you handle errors in Next.js?

**Difficulty:** Intermediate  
**Role:** Intermediate Developer  
**Tags:** Programming, Web, Error Handling

**Answer:**

**Error Boundaries (App Router):**

```typescript
// app/error.tsx
'use client';

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

**Not Found Pages:**

```typescript
// app/not-found.tsx
export default function NotFound() {
  return (
    <div>
      <h2>Not Found</h2>
      <p>Could not find requested resource</p>
    </div>
  );
}
```

**API Route Error Handling:**

```typescript
// app/api/users/route.ts
import { NextResponse } from 'next/server';

export async function GET() {
  try {
    const users = await getUsers();
    return NextResponse.json(users);
  } catch (error) {
    console.error('Error fetching users:', error);
    return NextResponse.json(
      { error: 'Internal server error' },
      { status: 500 }
    );
  }
}
```

**Global Error Handler:**

```typescript
// app/global-error.tsx
'use client';

export default function GlobalError({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  return (
    <html>
      <body>
        <h2>Something went wrong!</h2>
        <button onClick={() => reset()}>Try again</button>
      </body>
    </html>
  );
}
```

---

## Testing

### Q32. How do you test Next.js applications?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Testing, Web

**Answer:**

**Unit Testing with Jest:**

```typescript
// __tests__/utils.test.ts
import { formatDate } from '@/lib/utils';

describe('formatDate', () => {
  it('formats date correctly', () => {
    const date = new Date('2024-01-01');
    expect(formatDate(date)).toBe('Jan 1, 2024');
  });
});
```

**Component Testing with React Testing Library:**

```typescript
// __tests__/components/Button.test.tsx
import { render, screen } from '@testing-library/react';
import Button from '@/components/Button';

describe('Button', () => {
  it('renders correctly', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByText('Click me')).toBeInTheDocument();
  });
});
```

**E2E Testing with Playwright:**

```typescript
// e2e/home.spec.ts
import { test, expect } from '@playwright/test';

test('homepage loads', async ({ page }) => {
  await page.goto('/');
  await expect(page.locator('h1')).toContainText('Welcome');
});
```

---

## Deployment and DevOps

### Q33. How do you deploy Next.js applications?

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Deployment, DevOps, Web

**Answer:**

**Vercel Deployment:**

```bash
npm install -g vercel
vercel
```

**Docker Deployment:**

```dockerfile
# Dockerfile
FROM node:18-alpine AS base

FROM base AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci

FROM base AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

FROM base AS runner
WORKDIR /app
ENV NODE_ENV production
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/.next/static ./.next/static

EXPOSE 3000
CMD ["node", "server.js"]
```

**Environment Variables:**

```bash
# .env.production
DATABASE_URL=postgresql://...
NEXT_PUBLIC_API_URL=https://api.example.com
```

---

## Advanced Topics

### Q34. How do you implement real-time features with WebSockets in Next.js?

**Difficulty:** Advanced  
**Role:** Architect  
**Tags:** Programming, Backend, WebSockets, Real-time

**Answer:**

**WebSocket Server:**

```typescript
// app/api/ws/route.ts
import { NextRequest } from 'next/server';
import { Server as SocketIOServer } from 'socket.io';

export async function GET(request: NextRequest) {
  // Setup Socket.IO server
  // Handle WebSocket connections
}
```

**Client Connection:**

```typescript
// app/components/Chat.tsx
'use client';

import { useEffect, useState } from 'react';
import { io } from 'socket.io-client';

export default function Chat() {
  const [socket, setSocket] = useState<any>(null);
  
  useEffect(() => {
    const newSocket = io('http://localhost:3000');
    setSocket(newSocket);
    
    return () => newSocket.close();
  }, []);
  
  return <div>Chat component</div>;
}
```

---

### Q35. How do you implement internationalization (i18n) in Next.js?

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Web, i18n, Internationalization

**Answer:**

**Using next-intl:**

```typescript
// i18n.ts
import { notFound } from 'next/navigation';
import { getRequestConfig } from 'next-intl/server';

export const locales = ['en', 'fr', 'es'];

export default getRequestConfig(async ({ locale }) => {
  if (!locales.includes(locale as any)) notFound();
  
  return {
    messages: (await import(`../messages/${locale}.json`)).default,
  };
});
```

**Using in Components:**

```typescript
// app/[locale]/page.tsx
import { useTranslations } from 'next-intl';

export default function HomePage() {
  const t = useTranslations('HomePage');
  return <h1>{t('title')}</h1>;
}
```

---

## Summary

This comprehensive guide covers Next.js interview questions from basic to advanced levels, covering:

- **Fundamentals:** Core concepts and differences from React
- **Routing:** App Router and Pages Router
- **Data Fetching:** SSR, SSG, ISR strategies
- **Backend:** API routes, database connections, ORMs
- **Authentication & Authorization:** NextAuth.js, JWT, RBAC
- **Security:** Best practices and common vulnerabilities
- **Caching:** Redis integration
- **Message Brokers:** RabbitMQ and Kafka
- **Performance:** Optimization techniques
- **Testing:** Unit, integration, and E2E testing
- **Deployment:** Various deployment strategies

Each question includes:
- **Difficulty Level:** Basic, Intermediate, Advanced
- **Role Relevance:** Junior Developer, Intermediate Developer, Senior Developer, Architect
- **Tags:** Programming, Backend, Web, Database, Security, etc.
- **TypeScript Examples:** Real-world code samples

This guide serves as a one-stop resource for Next.js interview preparation, covering both frontend and backend development aspects of the framework.

---

