# Next.js w/ Tailwind for Telegram Web Apps

This is a template for quickly create Telegram Web Apps using [Next.js](https://nextjs.org/) and [Tailwind CSS](https://tailwindcss.com/).

### Why Next.js?

Next.js is easy and powerful, it also allows creating API routes without the need of another server and any troubles, example, it's ideal for validating the incoming web app's request hash.

## How to use

Execute [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app) with [pnpm](https://pnpm.io) to create a new project:

```bash
pnpm create next-app --example https://github.com/mauriciobraz/next.js-telegram-webapp your-app-name
```

Now, clone the [`.env.example`](.env.example) file and rename it to `.env.local` and fill the variables with your own data.

- `BOT_TOKEN`: Your Telegram Bot Token (used for validating the incoming requests, see [Request Validation](#request-validation) for more info)

```bash
pnpm dev
```

### Testing locally w/ [ngrok](https://ngrok.com/)

Since Telegram only accepts HTTPS links, you'll need to use a tunneling service like [ngrok](https://ngrok.com/) to test your bot locally.

```bash
# Copy the HTTPS URL given by ngrok and use it as main URL for your bot.
# If the port differs from 3000, change it accordingly.
ngrok http 3000
```

### Bundle Analyzer

This template is already configured to use [@next/bundle-analyzer](https://www.npmjs.com/package/@next/bundle-analyzer), that is a plugin for Next.js that analyzes the bundle size of your application (useful when you want to replace a library with another one that is smaller). The following command will generate a report in the `.next/analyze` folder and open it in your browser.

```bash
pnpm analyze
```

## Request Hash Validation

All the requests are validated using an API route that checks if the request is coming from Telegram. [Telegram's documentation](https://core.telegram.org/bots/webapps#validating-data-received-via-the-web-app) explains how it works.

### Disabling the validation

To disable this feature, delete the [`pages/api/validate-hash.ts`](src/pages/api/validate-hash.ts) file and remove the `useEffect` hook from [`pages/_app.tsx`](src/pages/_app.tsx) and it's dependencies.

```diff
