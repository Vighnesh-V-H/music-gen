# 🎵 Music Gen - AI-Powered Music Generation Platform

A full-stack web application that harnesses AI to generate unique music from text descriptions and lyrics. Music Gen empowers creators, musicians, and enthusiasts to transform their ideas into audio tracks with intuitive generation modes and a vibrant community platform.

---

## ✨ Key Features

### 🎼 Intelligent Music Generation
- **Description-Based Generation**: Create music from detailed textual descriptions
- **Lyrics-Driven Creation**: Generate full compositions from your own lyrics
- **Hybrid Mode**: Combine descriptions with lyrics for enhanced creative control
- **Style & Inspiration Tags**: Pre-built tags for quick access to popular musical styles

### 👤 User Account Management
- **Secure Authentication**: Email/password sign-up and login powered by BetterAuth
- **Credit System**: Pay-as-you-go credit model for generation API calls
- **User Profiles**: Showcase your creations publicly or keep them private

### 💳 Monetization & Billing
- **Polar Payments Integration**: Seamless subscription and one-time purchase handling
- **Three-Tier Plans**: Small (10 credits), Medium (25 credits), and Large (50 credits) packages
- **Customer Portal**: Users manage subscriptions and billing directly
- **Webhook Support**: Automated credit allocation on successful payment

### 🎧 Music Discovery & Engagement
- **Public Music Hub**: Browse and discover tracks created by the community
- **Like System**: Save your favorite tracks for quick access
- **Social Features**: See who created each track
- **Search & Filter**: Find music by title and creator

### 🎛️ Playback & Management
- **Integrated Player**: Listen to generated tracks directly in the app
- **Download Support**: Export your music in standard audio formats
- **Track Management**: Rename, publish, or delete your creations
- **Presigned URLs**: Secure, temporary access to music files in S3

---

## 🏗️ Tech Stack

### Frontend
- **Framework**: [Next.js 14+](https://nextjs.org/) - React with server-side rendering and API routes
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) - Utility-first CSS framework
- **UI Components**: [shadcn/ui](https://ui.shadcn.com/) - High-quality, accessible component library
- **State Management**: [Zustand](https://github.com/pmndrs/zustand) - Lightweight state management
- **Authentication UI**: [BetterAuth UI](https://github.com/better-auth/better-auth) - Pre-built auth components
- **Icons**: [Lucide React](https://lucide.dev/) - Beautiful SVG icons
- **Notifications**: [Sonner](https://sonner.emilkowal.ski/) - Elegant toast notifications

### Backend & Database
- **ORM**: [Prisma](https://www.prisma.io/) - Type-safe database access
- **Database**: PostgreSQL - Reliable relational database
- **Authentication**: [BetterAuth](https://better-auth.js.org/) - Lightweight auth framework with plugins
- **Background Jobs**: [Inngest](https://www.inngest.com/) - Serverless job processing

### External Services
- **Music Generation AI**: Modal.com - API endpoints for AI music generation
- **File Storage**: Amazon S3 - Scalable cloud storage for generated tracks
- **Payments**: [Polar](https://polar.sh/) - Payment processing & subscription management
- **Authentication Provider**: BetterAuth with PostgreSQL adapter

---

## 📁 Project Structure

```
src/
├── app/                    # Next.js App Router pages & layouts
│   └── (auth)/            # Auth-grouped routes
│       └── auth/          # Authentication pages
├── components/             # React components
│   ├── create/            # Music generation UI
│   │   ├── song-panel.tsx         # Generation form & controls
│   │   ├── track-list.tsx         # User's track management
│   │   └── rename-dialog.tsx      # Track rename modal
│   ├── home/              # Discovery & browsing
│   │   └── song-card.tsx          # Music card component
│   ├── sidebar/           # Navigation & layout
│   │   └── app-sidebar.tsx        # Main sidebar component
│   ├── ui/                # Base UI components
│   └── providers.tsx      # App-wide providers & context
├── hooks/                  # Custom React hooks
│   └── use-mobile.ts      # Responsive design hook
├── inngest/               # Background job definitions
├── lib/                   # Utility functions & configuration
│   ├── auth.ts           # BetterAuth server config with Polar integration
│   ├── auth-client.ts    # Client-side auth client
│   └── utils.ts          # Common utilities
├── server/                # Server-only code
│   └── db.ts             # Prisma client singleton
├── stores/                # Zustand state stores
│   └── use-player-store.ts  # Music player state
├── styles/                # Global CSS
├── actions/               # Server actions (to be implemented)
├── env.js                # Environment variable validation
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ and npm/yarn
- PostgreSQL database
- Environment variables (see `.env.example`)

### Required Environment Variables

```env
# Authentication
BETTER_AUTH_SECRET=your_secret_key_here

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/musicgen

# Modal.com (AI Music Generation)
MODAL_KEY=your_modal_key
MODAL_SECRET=your_modal_secret
GENERATE_FROM_DESCRIPTION=function_id
GENERATE_FROM_DESCRIBED_LYRICS=function_id
GENERATE_WITH_LYRICS=function_id

# AWS S3 (File Storage)
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY_ID=your_secret_key
AWS_REGION=us-east-1
S3_BUCKET_NAME=your-bucket-name

# Polar (Payments)
POLAR_ACCESS_TOKEN=your_polar_token
POLAR_WEBHOOK_SECRET=your_webhook_secret
```

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd music-gen/frontend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env.local
   # Edit .env.local with your configuration
   ```

4. **Initialize the database**
   ```bash
   npx prisma migrate dev
   ```

5. **Start the development server**
   ```bash
   npm run dev
   ```

   Open [http://localhost:3000](http://localhost:3000) to view the application.

---

## 🔑 Core Functionality

### Music Generation Workflow
1. **User Input**: Create a prompt via description or lyrics
2. **Validation**: Check user credits and validate input
3. **API Call**: Submit to Modal AI services for generation
4. **Processing**: Background jobs track generation status
5. **Storage**: Generated audio saved to S3
6. **Retrieval**: User plays or downloads the track

### Payment Flow
1. **User Selection**: Choose a credit package
2. **Checkout**: Redirected to Polar checkout
3. **Payment**: Processed securely by Polar
4. **Webhook**: Polar notifies app of successful payment
5. **Credit Allocation**: Credits automatically added to user account
6. **Usage**: User can now generate music

### Authentication Flow
1. **Sign Up**: Email verification through BetterAuth
2. **Session**: Secure JWT-based session management
3. **Authorization**: Protected routes check user session
4. **Customer Creation**: Polar automatically creates customer profile

---

## 🛠️ Development

### Available Scripts
```bash
npm run dev       # Start development server with hot reload
npm run build     # Build for production
npm run start     # Start production server
npm lint          # Run ESLint
npm type-check    # Type check with TypeScript
```

### Database Migrations
```bash
npx prisma migrate dev --name <migration_name>  # Create new migration
npx prisma migrate deploy                        # Deploy migrations
npx prisma studio                                # Open Prisma UI
```

### Type Safety
The project uses TypeScript for end-to-end type safety. Environment variables are validated with Zod at runtime. Components use proper React TypeScript patterns.

---

## 🎨 UI/UX Design

### Component Architecture
- **UI Layer**: Reusable shadcn/ui components (Button, Dialog, Input, etc.)
- **Feature Components**: Domain-specific components (SongPanel, TrackList, SongCard)
- **Layouts**: App-wide layout structure with sidebar navigation
- **Responsive**: Mobile-first design with responsive utilities

### State Management
- **Global Player State**: Zustand store for current playing track
- **Local Component State**: React hooks for form data and UI state
- **Server State**: Prisma queries and server actions for data operations

---

## 🔐 Security & Best Practices

- **Environment Validation**: Zod-based schema validation for all env vars
- **Database**: Prisma adapter with SQL injection prevention
- **Authentication**: BetterAuth with encrypted sessions
- **File Access**: Presigned URLs expire after limited time
- **Payment**: PCI-compliant through Polar, no direct credit card handling
- **CORS**: Next.js API routes with built-in security
