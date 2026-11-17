# DMV Wait-Time Dashboard

**Live:** https://dmv-dashboard-omega.vercel.app

A planning tool for DMV office managers. It shows how changes to the office
would affect customer wait times, before you try them on real customers.

## How to use it
1. Open the link above in any browser. Nothing to install.
2. At the top are three switches. Each one is a change you could make:
   - **Serve appointments first:** appointment customers go ahead of walk-ins
   - **Cross-train the Vehicle clerk:** they also help licensing customers when free
   - **Add a second Records clerk:** one more person on the Records counter
3. Turn switches on and off. The results update instantly.
4. Click **Back to current setup** to start over.

## What the results mean
- **Average wait:** how long a typical customer waited
- **People waiting over 15 min:** customers who missed the office goal
- **Longest wait:** the single worst wait of the day
- **Green arrow:** better than today. **Red arrow:** worse than today.
- **Yellow bar:** someone in that service waited longer than 15 minutes

## Good to know
- Results come from a made-up busy day with 35 customers, not real data.
- The numbers are calculated by a C++ simulation that replays the day minute by minute.