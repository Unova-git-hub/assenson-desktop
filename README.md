# Assenson — Supabase + Vercel

A React + Vite personal finance web app with Supabase authentication and per-user cloud data. Designed for deployment on Vercel.

## Included
- Email/password sign-up, sign-in, and sign-out through Supabase Auth
- Cloud-saved income/expense transactions (create, search/filter, delete, CSV export)
- Monthly category budgets with current-month progress
- Savings goals with progress updates
- Compound savings, loan payment, 50/30/20 budget, and emergency-fund calculators
- Financial tips and guides
- Responsive yellow/gold UI
- SQL schema with Row Level Security (RLS) policies so users can access only their own rows

## 1. Create and configure Supabase
1. Create a project at https://supabase.com/dashboard.
2. Open **SQL Editor → New query**.
3. Paste and run the complete contents of `supabase/schema.sql`.
4. Go to **Project Settings → API** (or the API keys page). Copy the Project URL and the **publishable key** (or legacy `anon` key).
5. Copy `.env.example` to `.env.local` and fill in:
   ```
   VITE_SUPABASE_URL=https://YOUR_PROJECT_ID.supabase.co
   VITE_SUPABASE_ANON_KEY=YOUR_SUPABASE_PUBLISHABLE_OR_ANON_KEY
   ```
   Never put a Supabase `service_role` or secret key in this frontend app.
6. In **Authentication → URL Configuration**, add your local URL `http://localhost:5173` to allowed redirect URLs. Later add your exact Vercel production URL too.

## 2. Run locally
Install Node.js (LTS) from https://nodejs.org if needed. Open a terminal in this folder and run:
```bash
npm install
npm run dev
```
Open the localhost URL shown by Vite (usually `http://localhost:5173`).

## 3. Publish to Vercel
Recommended path:
1. Create a GitHub repository and upload the project files (do not upload `.env.local`).
2. Open https://vercel.com/new and import that repository.
3. Framework preset should detect **Vite**. Build command: `npm run build`; output directory: `dist`.
4. In Vercel project **Settings → Environment Variables**, add:
   - `VITE_SUPABASE_URL` = your Supabase project URL
   - `VITE_SUPABASE_ANON_KEY` = your Supabase publishable/anon key
   Add for Production, Preview, and Development as appropriate.
5. Deploy. Once deployed, copy the Vercel URL.
6. Return to Supabase **Authentication → URL Configuration**:
   - Set **Site URL** to your production Vercel URL.
   - Add the production URL and preview URL patterns you use to **Redirect URLs**.
7. Redeploy after changing Vercel environment variables. Test signup, email confirmation (if enabled), login, add transaction, refresh, delete, and sign-out.

### GitHub upload quick path
- Create a new repository in GitHub.
- Upload `package.json`, `index.html`, `vite.config.js`, `vercel.json`, `.gitignore`, `.env.example`, `README.md`, and the `src` and `supabase` folders.
- Do not upload `node_modules`, `dist`, or `.env.local`.

## Important production notes
- This is a personal finance tracker, not a bank, payment processor, or regulated financial service.
- Only the Supabase publishable/anon key belongs in the browser; RLS policies protect user data. Never expose the `service_role` key.
- Use Supabase email confirmation and configure email delivery before inviting public users. Default email sending limits may be restrictive.
- Add a privacy policy, terms, support contact, and an appropriate security review before a public commercial launch.
- Data is per-user in Supabase. Do not collect bank credentials, card numbers, PINs, or other unnecessary sensitive data.
- Calculators are estimates for education and planning, not financial advice or guaranteed outcomes.
