# Charley King Stables — Setup Guide

Follow these steps in order. Each one takes about 5 minutes.
Total time: ~25 minutes to get fully live.

---

## Step 1 — Set Your Admin Password

Open `admin.html` in a text editor and find this line near the top of the script:

    const ADMIN_PASSWORD = 'charleyking1922';

Change `charleyking1922` to whatever password you want.
Keep it simple — you're the only one who'll ever use this page.

---

## Step 2 — Set Up Supabase (the guestbook database)

1. Go to **https://supabase.com** and click "Start your project"
2. Sign up with your email (free, no credit card)
3. Click "New Project" — name it `charleykingstables`
4. Choose a region (US East is fine) and set any database password — write it down
5. Wait about 60 seconds for the project to spin up

**Create the guestbook table:**

6. In the left sidebar, click **Table Editor**
7. Click **New Table**
8. Name it: `guestbook`
9. Make sure "Enable Row Level Security (RLS)" is **OFF** for now
10. Add these columns (click "Add Column" for each):

   | Name        | Type      | Default | Notes              |
   |-------------|-----------|---------|---------------------|
   | name        | text      | —       | required           |
   | location    | text      | —       | optional           |
   | message     | text      | —       | required           |
   | approved    | bool      | false   | set default: false |
   | created_at  | timestamp | now()   | set default: now() |

   (The `id` column is created automatically)

11. Click **Save**

**Get your keys:**

12. In the left sidebar, click the **gear icon → API**
13. Copy the **Project URL** — it looks like `https://abcdefgh.supabase.co`
14. Copy the **anon public** key — it's a long string starting with `eyJ...`

**Add the keys to your files:**

Open both `guestbook.html` and `admin.html` in a text editor.
In each file, find these two lines near the top of the `<script>` section and replace:

    const SUPABASE_URL      = 'YOUR_SUPABASE_URL';
    const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';

With your actual values:

    const SUPABASE_URL      = 'https://abcdefgh.supabase.co';
    const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';

---

## Step 3 — Set Up reCAPTCHA (blocks bots)

1. Go to **https://www.google.com/recaptcha/admin/create**
2. Sign in with your Google account
3. Fill in:
   - **Label:** Charley King Stables
   - **reCAPTCHA type:** reCAPTCHA v2 → "I'm not a robot" checkbox
   - **Domains:** add your domain (e.g. `charleykingstables.com`) AND `localhost`
4. Click Submit
5. You'll get a **Site Key** and a **Secret Key**
   - You only need the **Site Key** for the website files

Open `guestbook.html` and find:

    <div class="g-recaptcha" data-sitekey="YOUR_RECAPTCHA_SITE_KEY"></div>

Replace `YOUR_RECAPTCHA_SITE_KEY` with your actual Site Key.

---

## Step 4 — Deploy to Netlify (free hosting)

1. Go to **https://netlify.com** and sign up (free)
2. From your dashboard, click **Add new site → Deploy manually**
3. Drag your entire `charleykingstables` folder into the upload box
   - This folder should contain: `index.html`, `biography.html`, `horses.html`,
     `photos.html`, `recordings.html`, `eliking.html`, `brooke.html`,
     `crawfordville.html`, `guestbook.html`, `admin.html`, `contact.html`,
     and your `Assets` folder with all the photos.
4. Netlify will give you a random URL like `festive-jones-abc123.netlify.app`
   — the site is live!

---

## Step 5 — Connect Your Domain (charleykingstables.com)

If you already own the domain:

1. In Netlify, go to **Site Settings → Domain Management → Add custom domain**
2. Type in `charleykingstables.com` and follow the instructions
3. Netlify will tell you which nameservers or DNS records to set at your registrar
   (GoDaddy, Namecheap, etc.)
4. DNS changes take a few hours to propagate — then you're live at charleykingstables.com

If you need to buy the domain, check **https://namecheap.com** (~$12/year).

---

## How to Moderate the Guestbook

When someone submits a message:
- It goes into Supabase with `approved = false`
- It is **invisible to visitors**
- You review it at: `https://charleykingstables.com/admin.html`

To approve or delete:
1. Go to `yoursite.com/admin.html`
2. Enter your admin password (from Step 1)
3. You'll see all pending messages in the "Pending Review" tab
4. Click **Approve** to publish it, or **Delete** to remove it forever

**Keep the admin.html address private** — don't link to it from the site.
It's protected by a password, but there's no need to advertise it.

---

## That's it!

Your site is live, the guestbook works, spam bots are blocked by reCAPTCHA,
and you have full control over what gets posted.

Questions? The site was built by Claude for Wyatt King.
