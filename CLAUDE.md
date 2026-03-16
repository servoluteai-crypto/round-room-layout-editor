# Round Room Layout Editor

## Repository Structure

This is a **git repository with a submodule**. All active development happens inside the submodule.

```
Round-room-layout-editor/          ← You are here (root repo)
├── roundroom-floorplanner/        ← Main Next.js app (git submodule)
│   ├── src/                       ← All source code lives here
│   ├── docs/                      ← Architecture, features, changelog, status
│   ├── CLAUDE.md                  ← Dev essentials (SSR, workflow, quick ref)
│   └── package.json
├── .mcp.json                      ← MCP server config (Supabase)
└── package.json                   ← Root deps (minimal, not the app)
```

**For all development work, cd into `roundroom-floorplanner/` and read its `CLAUDE.md`.**

---

## Quick Start

```bash
cd roundroom-floorplanner
npm install
npm run dev          # → http://localhost:3000
```

---

## What This App Does

AI-powered floor planning tool for the **Round Room at Mansion House, Dublin** — a 29.5m diameter circular venue. Helps event planners create table layouts in seconds instead of hours.

- **2D drag-and-drop canvas** (Konva)
- **3D visualization** (Three.js)
- **Preset library** (saved to Supabase)
- **Share links** for read-only layout sharing
- **PDF export**

---

## Tech Stack (Summary)

| Layer | Technology |
|-------|-----------|
| Framework | Next.js 15, React 19, TypeScript |
| 2D Canvas | Konva + react-konva |
| 3D Scene | Three.js + @react-three/fiber |
| State | Zustand |
| Backend | Supabase (PostgreSQL + Auth) |
| Styling | Tailwind CSS |

---

## MCP Configuration

`.mcp.json` configures the **Supabase MCP server** for direct database access:
- Project ref: `zspvgllcdapejoglgpdu`
- Use for: inspecting schema, running queries, checking RLS policies

---

## Submodule Workflow

```bash
# Update submodule to latest
git submodule update --remote roundroom-floorplanner

# After making changes inside submodule, commit the new ref from root
cd ..
git add roundroom-floorplanner
git commit -m "chore: update roundroom-floorplanner submodule ref"
```

---

## Environment Variables

Create `roundroom-floorplanner/.env.local`:

```
NEXT_PUBLIC_SUPABASE_URL=https://zspvgllcdapejoglgpdu.supabase.co
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY=<your key>
```

---

## Key Files to Know

| File | Purpose |
|------|---------|
| `roundroom-floorplanner/CLAUDE.md` | Dev essentials (SSR, workflow, quick ref) |
| `roundroom-floorplanner/docs/` | Architecture, features, changelog, project status |
| `roundroom-floorplanner/src/lib/store.ts` | Zustand state (1048 lines, single source of truth) |
| `roundroom-floorplanner/src/types/index.ts` | All TypeScript interfaces + constants |
| `roundroom-floorplanner/src/lib/scenarios.ts` | 9 built-in preset layouts |
| `roundroom-floorplanner/src/components/FloorPlan/Canvas.tsx` | 2D Konva canvas |
| `roundroom-floorplanner/src/components/FloorPlan3D/Canvas3D.tsx` | 3D Three.js scene |
