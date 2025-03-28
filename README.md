<img width="250px" src="https://neon.tech/brand/neon-logo-dark-color.svg" />

# Neon RLS + Stack Auth Example (SQL from the Backend)

A quick start Next.js template demonstrating secure user authentication and authorization using Neon RLS with Stack Auth integration. This guide primarily uses SQL from the backend to enforce row-level security policies.

## Features

- Next.js application with TypeScript
- User authentication powered by Stack Auth
- Row-level security using Neon RLS
- Database migrations with Drizzle ORM
- Ready-to-deploy configuration for Vercel, Netlify, and Render

## Prerequisites

- [Neon](https://neon.tech) account with a new project
- [Stack Auth](https://stack-auth.com/) account with a new project
- Node.js 18+ installed locally

## One-Click Deploy

Deploy directly to your preferred hosting platform:

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/neondatabase-labs/stack-nextjs-neon-rls&env=NEXT_PUBLIC_STACK_PROJECT_ID,NEXT_PUBLIC_STACK_PUBLISHABLE_CLIENT_KEY,STACK_SECRET_SERVER_KEY,DATABASE_URL,DATABASE_AUTHENTICATED_URL&project-name=neon-rls-stack&repository-name=neon-rls-stack)
[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/neondatabase-labs/stack-nextjs-neon-rls)
[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/neondatabase-labs/stack-nextjs-neon-rls)

> Make sure to add your website URL as a Trusted Domain on your Stack Auth project settings.

![Stack Auth Trusted Domain](/images/stack-auth-trusted-domain.png)

## Local Development Setup

### Configure Stack Auth

1. Sign up for a [Stack Auth](https://stack-auth.com/) account and create a new project.
2. Navigate to the project settings and create an API key.
3. Upon creating the API key, you will receive `NEXT_PUBLIC_STACK_PROJECT_ID`, `NEXT_PUBLIC_STACK_PUBLISHABLE_CLIENT_KEY` and `STACK_SECRET_SERVER_KEY`. Keep these handy for the next steps.

   ![Stack Auth API Key](/images/stack-auth-api-key.png)

### Set Up Neon RLS

1. Open your Neon Console and click "RLS" in your project's settings
2. Add a new authentication provider
3. Set the JWKS URL to: `https://api.stack-auth.com/api/v1/projects/<project-id>/.well-known/jwks.json`

   > Replace `<project-id>` with your Stack Auth project ID

   ![Neon RLS Add Auth Provider](/images/neon-rls-add-auth-provider.png)

4. Follow the steps in the UI to setup the roles for Neon RLS. You should ignore the schema related steps if you're following this guide.
5. Note down the connection strings for both the **`neondb_owner` role** and the **`authenticated, passwordless` role**. You'll need both. The `neondb_owner` role has full privileges and is used for migrations, while the `authenticated` role will be used by the application and will have its access restricted by RLS.
   
   ![Neon RLS Connection Strings](/images/neon-rls-env-values.png)

### Local Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/neondatabase-labs/stack-nextjs-neon-rls
   cd stack-nextjs-neon-rls
   ```

2. Install dependencies:

   ```bash
   npm install
   ```

3. Create `.env` file with the following variables:

   ```env
   NEXT_PUBLIC_STACK_PROJECT_ID=
   NEXT_PUBLIC_STACK_PUBLISHABLE_CLIENT_KEY=
   STACK_SECRET_SERVER_KEY=

   # Database connections
   DATABASE_URL=              # neondb_owner role connection
   DATABASE_AUTHENTICATED_URL= # authenticated role connection
   ```

   > Get your Stack Auth keys from your Stack Auth project dashboard.

4. Set up the database:

   ```bash
   npm run drizzle:generate  # Generate migrations
   npm run drizzle:migrate  # Apply migrations
   ```

5. Start the development server:

   ```bash
   npm run dev
   ```

6. Visit `http://localhost:3000` to see the application running.

   ![Neon RLS + Stack Auth Example](/images/neon-rls-stack-auth-example.png)

## Important: Production Setup

1. Upgrade your Stack Auth project to production mode by navigating to the project settings.
   ![Stack Auth Production Mode](/images/stack-auth-production-mode.png)
2. Verify that the JWKS URL in your Neon RLS configuration is correctly pointing to your Stack Auth project.

## Learn More

- [Neon RLS Tutorial](https://neon.tech/docs/guides/neon-rls-tutorial)
- [Simplify RLS with Drizzle](https://neon.tech/docs/guides/neon-rls-drizzle)
- [Stack Auth Documentation](https://docs.stack-auth.com/)
- [Neon RLS + Stack Auth Integration](https://neon.tech/docs/guides/neon-rls-stack-auth)

## Authors

- [David Gomes](https://github.com/davidgomes)

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
