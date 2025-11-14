# FISPAN SE Capacity & Pipeline Dashboard

A real-time collaborative dashboard for tracking Solution Engineer capacity across Bank and ERP opportunities.

## Features

- **Dual Tracking**: Manage Bank and ERP assignments separately
- **Real-time Sync**: Instant updates across all team members via Supabase
- **Inline Editing**: Update SE assignments and funnel stages directly in the table
- **Interactive Charts**: Multiple views (Banks, ERPs, Combined) with Chart.js visualizations
- **Sortable & Filterable**: Click headers to sort, filter by type or SE

## Quick Setup

### 1. Create Supabase Project

1. Sign up at [supabase.com](https://supabase.com)
2. Create a new project
3. Go to **SQL Editor** and run:

```sql
CREATE TABLE assignments (
  id BIGSERIAL PRIMARY KEY,
  opportunity_name TEXT NOT NULL,
  se TEXT NOT NULL,
  type TEXT NOT NULL,
  stage TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE assignments ENABLE ROW LEVEL SECURITY;

CREATE POLICY "Enable all access" ON assignments FOR ALL USING (true) WITH CHECK (true);

ALTER TABLE assignments ADD CONSTRAINT valid_type CHECK (type IN ('Bank', 'ERP'));
```

### 2. Get API Credentials

Go to **Project Settings > API** and copy:
- Project URL
- anon public key

### 3. Configure Dashboard

Edit `index.html` (lines 199-200):

```javascript
const SUPABASE_URL = 'https://xxxxx.supabase.co';
const SUPABASE_KEY = 'your-anon-key-here';
```

### 4. Deploy

**GitHub Pages:**
1. Create GitHub repo
2. Upload `index.html`
3. Enable Pages in Settings
4. Access at `https://username.github.io/repo-name`

## Usage

### Add Assignment
Fill in form (Type, Name, SE, Stage) → Click "Add Assignment"

### Update Assignment
- Change SE or Stage using dropdowns in table
- Delete with red button

### View Analytics
- **Banks**: Bank-specific capacity and funnel
- **ERPs**: ERP-specific capacity and funnel  
- **Combined**: Cross-view analytics

### Sort & Filter
- Click column headers to sort
- Use filters to show specific types or SEs

## Customization

**Add Solution Engineers:**
```javascript
const seNames = ["Rudra", "David", "Liam", "NewName"];
```

**Change Funnel Stages:**
```javascript
const funnelStages = ["Stage1", "Stage2", "Stage3"];
const stageColors = {
    "Stage1": '#4F46E5',
    "Stage2": '#10B981',
    "Stage3": '#F59E0B',
};
```

## Tech Stack

- HTML/CSS/JavaScript + Tailwind CSS
- Supabase (PostgreSQL + Realtime)
- Chart.js
- GitHub Pages

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Charts not loading | Verify Supabase credentials in code |
| Updates not syncing | Check internet connection, refresh page |
| Can't save data | Verify RLS policies enabled in Supabase |

## Security Note

The anon/public key is safe for frontend use. Row Level Security policies control access. Consider adding authentication for production environments.

---

**Questions?** Check [Supabase docs](https://docs.supabase.com) or [Chart.js docs](https://www.chartjs.org)
