# CyberHub Arena

A gamified, browser-based ethical-hacking and blue-team practice range for **CyberHub IT Academy**.
Students walk into a virtual company in first-person 3D, open a simulated Kali console, and practice
the real penetration-testing workflow — **recon → scan → enumerate → exploit → capture the flag →
privilege escalation** — plus blue-team triage and reporting labs.

> Training simulation only. All targets are safe, fictional practice hosts; the console teaches real
> command syntax and methodology but never touches real systems. For authorized training/education use.

**Live site:** https://cyberhubitacademy.github.io/CyberHubArena/

---

## What's inside

| File | Purpose |
|------|---------|
| `index.html` | The entire app — one self-contained page (HTML + CSS + JS). |
| `lockup.png` | CyberHub IT Academy logo lockup used on the portal. |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is. |

No build step, no dependencies to install. The 3D engine (three.js) loads from a public CDN at runtime.

---

## Host it free on GitHub Pages

1. Upload `index.html`, `lockup.png` and `.nojekyll` to the **root** of the repo.
2. **Settings → Pages → Build and deployment**: Source = *Deploy from a branch*, Branch = `main`, folder = `/ (root)`, **Save**.
3. Wait 1–2 minutes → open `https://cyberhubitacademy.github.io/CyberHubArena/`.

Keep the repo **public** (free Pages requires it). To use a custom domain (e.g. `arena.cyberhubitacademy.com`),
add it under **Settings → Pages → Custom domain** and point a CNAME at `cyberhubitacademy.github.io`.

---

## How students use it

- **Sign in:** `demo.student` / `cyberhub` (or any username).
- **Dashboard:** the flagship 3D range + skill labs + blue-team quizzes. Each card shows a progress %,
  and the top strip shows overall mastery (saved per device).
- **3D range controls:** `W A S D` move · mouse look (click to capture, or click-drag) · `Shift` run ·
  `E` interact · `Tab` console · `Esc` release cursor.
- **Console flow:** `nmap -sn <subnet>` → `nmap -sV <ip>` → `searchsploit <service>` → `exploit <ip>` →
  `ls` / `cat flag.txt` / `sudo -l` → paste the flag into the host's **Capture** box.
- Type `help`, `hint`, or `status` any time — `hint` always gives the next step.

---

## Add more labs

All labs are data — add one entry to the `LABS` array near the top of the `<script>` in `index.html`.
No engine changes needed.

**Terminal lab:**
```js
{ id:'ftp-lab', type:'terminal', title:'FTP Server Takeover', track:'Ethical Hacking', diff:'beg', icon:'folder',
  desc:'One-line card description.', learn:['Objective 1','Objective 2'],
  scenario: scen('10.10.60.0/24','10.10.60.50', [
    mach({ id:'f1', name:'FTP-BOX', ip:'10.10.60.15', os:'Linux',
      role:'What this host is and why it matters.',
      services:[['21','ftp','ProFTPd 1.3.5'],['22','ssh','OpenSSH 8.2']],
      weakIdx:0,
      weakness:{ title:'Short weakness name', teach:'Why it is weak.', defense:'How to fix it.' },
      exploit:['[*] step one...','[+] Session opened as <user>.'],
      idline:'uid=0(root) gid=0(root)', prompt:'root@ftp-box:~#',
      files:{ 'flag.txt':'CYBERHUB{your_flag_here}' },
      sudo:'(nothing useful here)', next:'What to say after capture.' })
  ]) }
```

**Blue-team quiz:**
```js
{ id:'phish', type:'quiz', title:'Phishing Triage', track:'SOC & VAPT', diff:'beg', icon:'activity',
  desc:'Spot the phishing signals.', learn:['Headers','Links','Urgency'],
  quiz:[ { q:'Question?', ctx:'optional evidence block', opts:['A','B','C','D'], a:1, fb:'Explanation.' } ] }
```

**Briefing (reading card):**
```js
{ id:'x', type:'briefing', title:'…', track:'…', diff:'beg', icon:'shield', desc:'…', learn:['…'] }
```

Notes:
- `icon` keys: `crosshair, radar, arrow-up, folder, globe, activity, clipboard, wifi, shield`.
- `diff`: `beg` / `int` / `adv`. Add `flag:true` to feature a lab in the flagship row.
- The flag is read from `files['flag.txt']` automatically — that's the single source of truth.
- Chain multiple hosts by adding several `mach({...})` entries to one scenario.

After editing, re-upload `index.html` — the live site refreshes within a minute or two.

---

© CyberHub IT Academy. For authorized cybersecurity training and education.
