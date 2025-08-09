
# Guitar Theory Mastery (Cloud Sync)

A dark, high-contrast, gamified guitar theory trainer with drills, mastery gates, and Supabase cloud sync.

## Quick Deploy to Vercel

1. **Download this zip** and push it to a new GitHub repo (or import straight into Vercel as a new project).
2. In Vercel → Project → **Settings → Environment Variables**, add:
   - `VITE_SUPABASE_URL` = https://YOUR_PROJECT_ID.supabase.co
   - `VITE_SUPABASE_ANON_KEY` = YOUR_ANON_KEY
3. Deploy.

## Setup Supabase (one-time)

In Supabase → **SQL Editor**, run:

```sql
create table if not exists public.progress (
  user_id uuid primary key references auth.users(id) on delete cascade,
  state jsonb not null,
  updated_at timestamp with time zone not null default now()
);

alter table public.progress enable row level security;
create policy "Users can read own progress" on public.progress for select using (auth.uid() = user_id);
create policy "Users can upsert own progress" on public.progress for insert with check (auth.uid() = user_id);
create policy "Users can update own progress" on public.progress for update using (auth.uid() = user_id) with check (auth.uid() = user_id);
```

## Local Dev (optional)
```bash
npm i
npm run dev
```
