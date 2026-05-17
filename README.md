# Google Help Portal V2

A multi-page HTML application for managing Google Help Portal operations, featuring Firebase auth, Supabase user management, and Resend email delivery — deployed on Vercel.

---

## ⚠️ Critical Rules — Read Before Touching Anything

### 1. This Is NOT a React App
The project uses a **multi-page HTML architecture**. The real app lives in:
pages/login.html
pages/user.html
pages/email-admin.html
pages/hq-control-7x9k.html
pages/compose/index.html
The `src/` folder only exists as a Vite entry point. **Do not add React logic to `src/App.tsx`**.

---

### 2. Never Edit vite.config.ts with sed
Always rewrite the whole file using `cat > vite.config.ts << 'EOF'` or use `nano`.

---

### 3. Environment Variables Required

| Variable | Required |
|---|---|
| `RESEND_API_KEY` | ✅ Yes |
| `SUPABASE_URL` | ✅ Yes |
| `SUPABASE_SERVICE_KEY` | ✅ Yes |
| `APP_URL` | ✅ Yes |
| `GEMINI_API_KEY` | ❌ Removed |

```bash
vercel env pull .env
4. Never Expose API Keys in Chat or Logs
Rotate immediately if leaked:
Resend: resend.com/api-keys
Supabase: Project Settings → API
Vercel: Settings → Tokens
5. Always Build Before Pushing
npm run build && git add . && git commit -m "fix: description" && git push origin main && vercel --prod
6. index.html Must Always Redirect to Login
<meta http-equiv="refresh" content="0; url=/pages/login" />
Never replace it with a React mount point or the app goes blank.
7. Termux Tips
Use ~/ not /tmp
Split sessions by swiping left edge
Always cd into correct project before Vercel commands
8. Lessons Learned
Problem
Cause
Fix
Blank page
index.html pointed to empty React stub
Redirect to /pages/login
Missing env vars
Vercel v2 never had them
vercel env pull + vercel env add
Corrupt vite.config.ts
sed deleted closing brackets
Rewrote entire file
Local Dev
npm install && vercel env pull .env && npm run dev
