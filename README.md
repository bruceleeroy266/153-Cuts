# 153 Cuts - Booking System

A clean, professional booking webpage for 153 Cuts barbershop with admin management.

---

## Quick Start (Demo Mode)

1. Open `index.html` in your browser
2. Book appointments (saves to browser localStorage)
3. Access admin at `admin.html`
4. Login with password: `BarberPro925!`

**Note:** Demo mode stores data locally. Bookings won't sync across devices.

---

## Supabase Setup (Production)

### 1. Create Supabase Project

1. Go to [supabase.com](https://supabase.com)
2. Sign up / Log in
3. Click "New Project"
4. Choose organization, name it "153-cuts"
5. Select region closest to you
6. Wait for project to initialize

### 2. Create Database Tables

Go to SQL Editor and run:

```sql
-- Bookings table
CREATE TABLE bookings (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    name TEXT NOT NULL,
    phone TEXT NOT NULL,
    email TEXT,
    service TEXT NOT NULL,
    date DATE NOT NULL,
    time TEXT NOT NULL,
    notes TEXT,
    status TEXT DEFAULT 'pending',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Enable Row Level Security
ALTER TABLE bookings ENABLE ROW LEVEL SECURITY;

-- Allow public inserts (for booking form)
CREATE POLICY "Allow public bookings" ON bookings
    FOR INSERT TO anon WITH CHECK (true);

-- Allow public reads (for checking availability)
CREATE POLICY "Allow public reads" ON bookings
    FOR SELECT TO anon USING (true);

-- Schedule settings table
CREATE TABLE schedule (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    day TEXT UNIQUE NOT NULL,
    open BOOLEAN DEFAULT true,
    start_time TEXT DEFAULT '09:00',
    end_time TEXT DEFAULT '18:00'
);

-- Blocked times table
CREATE TABLE blocked_times (
    id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
    date DATE NOT NULL,
    start_time TEXT NOT NULL,
    end_time TEXT NOT NULL,
    reason TEXT
);

-- Insert default schedule
INSERT INTO schedule (day, open, start_time, end_time) VALUES
    ('monday', false, '09:00', '18:00'),
    ('tuesday', true, '09:00', '18:00'),
    ('wednesday', true, '09:00', '18:00'),
    ('thursday', true, '09:00', '18:00'),
    ('friday', true, '09:00', '18:00'),
    ('saturday', true, '09:00', '18:00'),
    ('sunday', false, '09:00', '18:00');
```

### 3. Get API Credentials

1. Go to Project Settings → API
2. Copy "Project URL"
3. Copy "anon public" API key

### 4. Update Website

Edit `index.html`:

```javascript
const CONFIG = {
    useSupabase: true,  // Change to true
    supabaseUrl: 'https://your-project.supabase.co',  // Your URL
    supabaseKey: 'your-anon-key'  // Your key
};
```

Same for `admin.html`.

### 5. Deploy

Upload to any static host:
- Netlify
- Vercel
- GitHub Pages
- Traditional web host

---

## Features

### Client Side
- Clean one-page design
- Service selection with prices
- Date/time picker with availability check
- No double booking (checks pending/confirmed)
- No-show policy display
- Mobile responsive

### Admin Side
- Password protected
- View all bookings
- Filter by status (Pending, Confirmed, Completed, Canceled)
- Update booking status
- Weekly schedule editor
- Block time slots
- Stats dashboard

### Booking Flow
1. Client selects service, date, time
2. System checks availability (no conflicts)
3. Booking saved as "Pending"
4. Client sees confirmation message
5. Admin reviews and confirms
6. Only Pending/Confirmed block time slots

---

## Security Notes

⚠️ **Current admin password is temporary:** `change-me-123`

Before heavy public use:
1. Change admin password in `admin.html`
2. Set up proper authentication (Supabase Auth)
3. Enable HTTPS on your domain
4. Consider adding rate limiting

---

## File Structure

```
153 cuts/
├── index.html      # Main booking page
├── admin.html      # Admin dashboard
└── README.md       # This file
```

---

## Customization

### Change Services
Edit the services grid in `index.html`:

```html
<div class="service-card">
    <div class="service-icon">
        <i class="fas fa-cut"></i>
    </div>
    <h3>Your Service</h3>
    <p>Description</p>
    <div class="service-price">$XX</div>
</div>
```

### Change Hours
Update the schedule in admin panel, or edit default in `admin.html`:

```javascript
const defaultSchedule = {
    tuesday: { open: true, start: '09:00', end: '18:00' },
    // ... etc
};
```

### Change Colors
Edit CSS variables in both files:

```css
:root {
    --gold: #D4AF37;        /* Primary accent */
    --dark: #0a0a0a;        /* Background */
    --dark-gray: #1a1a1a;   /* Card backgrounds */
    /* ... etc */
}
```

---

## Support

Built for 153 Cuts barbershop. Questions? Check the code comments or reach out.

**Remember:** Switch to Supabase before going live!
