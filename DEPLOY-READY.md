# 153 Cuts - DEPLOY READY ✅

**Status:** Ready for deployment  
**Last Updated:** May 3, 2026  
**QC Cost:** $0 (Kimi review)

---

## WHAT WAS FIXED

### 1. Added Demo Mode Notice (Client Side)
- Added blue info box on booking page explaining localStorage mode
- Helps users understand bookings won't sync until Supabase is connected

### 2. Added Payment Information
- Added "Cash preferred" notice in booking section
- Green styling to match payment theme

### 3. Added Student Barber Disclaimer
- Added "Student Barber - Quality cuts at student prices" to hero section
- Uses graduation cap icon
- Gold color to match theme

### 4. Added Configuration Comments
- Marked all editable sections in both HTML files
- Clear instructions for: prices, services, hours, password, Supabase credentials
- Easy to find and modify

---

## QUICK START

### Test Locally
```bash
cd "C:\Users\skyfl\Desktop\153 cuts"
python -m http.server 8080
# Open http://localhost:8080
```

### Deploy to Netlify (Easiest)
1. Go to [netlify.com](https://netlify.com)
2. Drag & drop the "153 cuts" folder
3. Done! Site is live.

### Deploy to Vercel
```bash
npm i -g vercel
vercel
```

---

## EDITING GUIDE

### Change Prices
**File:** `index.html`  
**Location:** Around line 760, in the `<select id="service">` dropdown
```html
<option value="Haircut">Haircut - $15</option>
<option value="Beard Trim">Beard Trim - $10</option>
<option value="Haircut + Beard">Haircut + Beard - $22</option>
```

### Change Business Hours
**File:** `admin.html`  
**Location:** Around line 880, in `defaultSchedule` object
```javascript
const defaultSchedule = {
    tuesday: { open: true, start: '09:00', end: '18:00' },
    // ... etc
};
```

### Change Admin Password
**File:** `admin.html`  
**Location:** Top of `<script>` section
```javascript
const ADMIN_PASSWORD = 'change-me-123';  // <-- CHANGE THIS
```

### Change TikTok Handle
**File:** `index.html`  
**Location:** Contact section and TikTok section
Search for: `@Flying_oppusit`

### Change Phone Number
**File:** `index.html`  
**Location:** Contact section
Search for: `(904) 480-9422`

### Connect Supabase (Production)
**Files:** `index.html` and `admin.html`

1. In `index.html`:
```javascript
const CONFIG = {
    useSupabase: true,  // <-- SET TO TRUE
    supabaseUrl: 'https://your-project.supabase.co',  // <-- YOUR URL
    supabaseKey: 'your-anon-key'  // <-- YOUR KEY
};
```

2. In `admin.html`:
```javascript
const USE_SUPABASE = true;                          // <-- SET TO TRUE
const SUPABASE_URL = 'https://your-project.supabase.co';  // <-- YOUR URL
const SUPABASE_KEY = 'your-anon-key';               // <-- YOUR KEY
```

---

## FEATURES WORKING ✅

- ✅ Booking form with validation
- ✅ No double booking (checks pending/confirmed)
- ✅ Time slots update based on schedule
- ✅ Admin dashboard with password
- ✅ Status management (Pending → Confirmed → Completed/Canceled)
- ✅ Schedule editor (open/closed days, hours)
- ✅ Blocked times
- ✅ Mobile responsive
- ✅ Student prices displayed
- ✅ Cash payment notice
- ✅ TikTok link
- ✅ Demo mode banner

---

## FILE STRUCTURE

```
153 cuts/
├── index.html              # Main booking page
├── admin.html              # Admin dashboard
├── README.md               # Full setup instructions
├── QC-REPORT.md            # Quality control report
├── DEPLOY-READY.md         # This file
└── images/
    ├── barber-cutting.png  # Hero image
    ├── barber-tiktok.jpg   # Your photo
    ├── barber-tools.png    # Services section
    └── barber-client.png   # Backup
```

---

## NEXT STEPS

1. **Test locally** - Make sure everything works
2. **Change admin password** - Before deploying
3. **Deploy** - Use Netlify for easiest setup
4. **Optional: Connect Supabase** - For production data sync

---

## SUPPORT

Questions? Check:
- `README.md` for full setup instructions
- `QC-REPORT.md` for detailed review
- Comments in HTML files for editable sections

**Ready to go live!** 🚀
