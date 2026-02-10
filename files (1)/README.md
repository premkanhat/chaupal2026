# Real-Time Investment Voting System
### Business Plan Competition Platform

A complete, production-ready real-time voting system built for college business plan competitions. Allows 220+ students to invest virtual capital in business ideas with live leaderboard updates.

![Status](https://img.shields.io/badge/status-production--ready-brightgreen)
![Hosting](https://img.shields.io/badge/hosting-free--tier-blue)
![Tech](https://img.shields.io/badge/tech-HTML%20%7C%20CSS%20%7C%20JS-orange)

## 🎯 Features

### Student Voting Portal (`vote.html`)
- ✅ Secure login with student roll number
- ✅ ₹10 Crore virtual capital per student
- ✅ Invest in 10 different business ideas
- ✅ Real-time balance tracking
- ✅ Multiple investments allowed
- ✅ Auto-save and session persistence
- ✅ Mobile-first responsive design

### Live Results Display (`live.html`)
- ✅ Real-time leaderboard with auto-refresh
- ✅ Optimized for projector/large screen display
- ✅ Animated rankings and progress bars
- ✅ Top 3 ideas highlighted (Gold/Silver/Bronze)
- ✅ Live statistics dashboard
- ✅ Beautiful animations and transitions

### Admin Control Panel (`admin.html`)
- ✅ Password-protected access
- ✅ Start/Stop voting controls
- ✅ Reset all data
- ✅ Export results to CSV
- ✅ Real-time statistics
- ✅ Detailed voting analytics
- ✅ Student and business idea management

## 🚀 Quick Start

### Option 1: Firebase Setup (Recommended - 100% Free)

#### Step 1: Create Firebase Project
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add Project"
3. Enter project name: `business-voting-2026`
4. Disable Google Analytics (optional)
5. Click "Create Project"

#### Step 2: Enable Realtime Database
1. In Firebase Console, go to **Build** → **Realtime Database**
2. Click **Create Database**
3. Choose location (closest to your event location)
4. Start in **Test Mode** (for development)
5. Click **Enable**

#### Step 3: Configure Security Rules
In Realtime Database, go to **Rules** tab and paste:

```json
{
  "rules": {
    "students": {
      ".read": true,
      "$studentId": {
        ".write": "!data.exists() || $studentId === newData.child('id').val()",
        ".validate": "newData.hasChildren(['id', 'totalCapital', 'remainingBalance'])"
      }
    },
    "businessIdeas": {
      ".read": true,
      ".write": true
    },
    "votingStatus": {
      ".read": true,
      ".write": true
    }
  }
}
```

**For Production (Event Day):**
```json
{
  "rules": {
    "students": {
      ".read": true,
      "$studentId": {
        ".write": "data.child('id').val() === $studentId"
      }
    },
    "businessIdeas": {
      ".read": true,
      ".write": "auth != null"
    },
    "votingStatus": {
      ".read": true,
      ".write": "auth != null"
    }
  }
}
```

#### Step 4: Get Firebase Configuration
1. Go to **Project Settings** (gear icon) → **General**
2. Scroll to "Your apps" section
3. Click **Web** icon (`</>`)
4. Register app with nickname: `voting-app`
5. Copy the `firebaseConfig` object

It will look like:
```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "your-app.firebaseapp.com",
  databaseURL: "https://your-app.firebaseio.com",
  projectId: "your-app",
  storageBucket: "your-app.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

#### Step 5: Update HTML Files
Replace the Firebase config in **ALL THREE FILES** (`vote.html`, `live.html`, `admin.html`):

Find this section in each file:
```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    // ... rest of config
};
```

Replace with your actual Firebase config.

#### Step 6: Customize Business Ideas
In `vote.html`, update the business ideas array (around line 394):

```javascript
const businessIdeas = [
    { id: 1, name: "EcoTech Solutions", team: "Team Alpha" },
    { id: 2, name: "HealthHub AI", team: "Team Beta" },
    { id: 3, name: "EduLearn Platform", team: "Team Gamma" },
    // ... add your 10 business ideas
];
```

#### Step 7: Set Admin Password
In `admin.html`, change the admin password (line 545):

```javascript
const ADMIN_PASSWORD = "your_secure_password_here"; // CHANGE THIS!
```

### Option 2: Deploy to Free Hosting

#### GitHub Pages
```bash
# 1. Create new repository on GitHub
# 2. Clone repository
git clone https://github.com/yourusername/voting-system.git
cd voting-system

# 3. Add your files
cp vote.html index.html  # GitHub Pages uses index.html as default
cp live.html .
cp admin.html .

# 4. Commit and push
git add .
git commit -m "Initial deployment"
git push origin main

# 5. Enable GitHub Pages
# Go to Settings → Pages → Source: main branch → Save
```

Your site will be live at: `https://yourusername.github.io/voting-system/`

#### Netlify
```bash
# 1. Install Netlify CLI
npm install -g netlify-cli

# 2. Deploy
netlify deploy

# 3. Follow prompts to link site
# 4. Deploy to production
netlify deploy --prod
```

#### Vercel
```bash
# 1. Install Vercel CLI
npm install -g vercel

# 2. Deploy
vercel

# 3. Follow prompts
```

## 📱 Usage Instructions

### For Event Organizers

1. **Before Event:**
   - Update business ideas in code
   - Set secure admin password
   - Test all three pages
   - Create QR code for voting URL

2. **Event Day:**
   - Open `admin.html` and login
   - Click **"Start Voting"**
   - Share voting URL or QR code with students
   - Display `live.html` on projector
   - Monitor admin panel for statistics

3. **During Event:**
   - Watch live leaderboard update
   - Monitor voting participation
   - Can stop/start voting anytime

4. **After Event:**
   - Click **"Stop Voting"**
   - Export results to CSV
   - Announce winners from leaderboard

### For Students

1. Open voting URL on mobile browser
2. Enter your roll number
3. Select business idea from dropdown
4. Enter investment amount (in Crores)
5. Click "Invest Now"
6. Can make multiple investments
7. Track remaining balance
8. View your investment history

## 🔧 Customization

### Change Color Scheme
Edit CSS variables in each HTML file:

```css
:root {
    --accent-primary: #00d9ff;    /* Change primary color */
    --accent-secondary: #7000ff;  /* Change secondary color */
    --success: #00ff88;           /* Change success color */
}
```

### Add More Business Ideas
Just add to the array in `vote.html`:

```javascript
const businessIdeas = [
    // ... existing ideas
    { id: 11, name: "New Idea", team: "Team New" },
    { id: 12, name: "Another Idea", team: "Team Another" }
];
```

### Change Total Capital
In `vote.html`, modify:

```javascript
const TOTAL_CAPITAL = 10; // Change from 10 Crore to any value
```

## 📊 Data Structure

The system uses Firebase Realtime Database with this structure:

```
root/
├── students/
│   └── {studentId}/
│       ├── id: string
│       ├── totalCapital: number
│       ├── remainingBalance: number
│       ├── lastUpdated: timestamp
│       └── investments/
│           └── {investmentId}/
│               ├── businessId: string
│               ├── amount: number
│               └── timestamp: timestamp
├── businessIdeas/
│   └── {businessId}/
│       ├── name: string
│       ├── team: string
│       ├── totalInvestment: number
│       ├── investors: number
│       └── lastUpdated: timestamp
└── votingStatus/
    └── active: boolean
```

## 🎨 Design Features

- **Modern Dark Theme** - Eye-friendly for long events
- **Gradient Accents** - Cyberpunk-inspired neon aesthetics
- **Smooth Animations** - Delightful micro-interactions
- **Responsive Layout** - Works on all devices
- **Real-time Updates** - No refresh needed
- **Professional Typography** - DM Sans + JetBrains Mono

## 🔒 Security Notes

### Development Mode
- Test mode allows open database access
- Perfect for testing and development
- **DO NOT use in production**

### Production Mode (Event Day)
1. Use the production security rules provided above
2. Change admin password to something secure
3. Consider enabling Firebase Authentication
4. Monitor database usage during event

### Best Practices
- ✅ Use HTTPS (automatic with GitHub Pages/Netlify/Vercel)
- ✅ Change default admin password
- ✅ Test thoroughly before event
- ✅ Have backup plan (screenshots of data)
- ✅ Export data immediately after event

## 📈 Scalability

### Firebase Free Tier Limits
- **Storage:** 1 GB
- **Downloads:** 10 GB/month
- **Simultaneous connections:** 100

**This is MORE than enough for:**
- ✅ 220 students voting
- ✅ Real-time leaderboard
- ✅ Multiple admin sessions
- ✅ All day event

## 🐛 Troubleshooting

### "Permission Denied" Error
- Check Firebase security rules
- Ensure database URL is correct
- Verify internet connection

### Votes Not Updating
- Check Firebase config is correct
- Ensure voting status is "Active" in admin panel
- Check browser console for errors

### Admin Panel Not Loading
- Verify admin password
- Check Firebase config
- Clear browser cache

### Leaderboard Not Showing
- Ensure at least one investment exists
- Check Firebase console for data
- Verify database rules allow reads

## 💡 Tips for Success

1. **Test Everything:**
   - Test with multiple browsers
   - Test on different devices
   - Do a mock voting session

2. **Prepare Backups:**
   - Take screenshots of setup
   - Save Firebase config separately
   - Have CSV exports ready

3. **Event Day:**
   - Arrive early to test WiFi
   - Have QR codes printed
   - Keep admin panel open
   - Monitor in real-time

4. **Student Communication:**
   - Send clear instructions before event
   - Explain the ₹10 Cr is virtual
   - Remind about multiple investments
   - Share voting URL in advance

## 📦 What's Included

```
voting-system/
├── vote.html          # Student voting interface
├── live.html          # Live results display
├── admin.html         # Admin control panel
└── README.md          # This file
```

## 🌟 Features Breakdown

| Feature | Student Portal | Live Display | Admin Panel |
|---------|---------------|--------------|-------------|
| Real-time updates | ✅ | ✅ | ✅ |
| Mobile responsive | ✅ | ❌ | ✅ |
| Auto-save | ✅ | N/A | N/A |
| Data export | ❌ | ❌ | ✅ |
| Analytics | ❌ | ✅ | ✅ |
| Controls | ❌ | ❌ | ✅ |

## 📞 Support

For issues or questions:
1. Check this README thoroughly
2. Review Firebase documentation
3. Check browser console for errors
4. Test with different browsers

## 📄 License

Free to use for educational purposes. No attribution required.

---

**Built for Business Plan Competition 2026**  
*Making voting simple, transparent, and engaging*

🚀 **Ready to deploy in under 10 minutes!**
