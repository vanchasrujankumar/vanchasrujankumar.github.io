# Portfolio Site

Personal portfolio site — Lead Data Engineer.
Live at: **https://vanchasrujankumar.github.io**

---

## File Structure

```
├── index.html       # Single-file site — all HTML, CSS, and JS inline
├── srujan.jpeg      # Headshot photo (professional headshot)
├── renovate.json    # Dependency auto-update config
└── .github/
    └── workflows/
        └── deploy.yml   # GitHub Actions — auto-deploys on push to main
```

---

## How to Make Changes

### 1. Update Profile Photo
Replace `srujan.jpeg` in this directory with a new image (keep the same filename).
The CSS crops to the top 15% of the image automatically (`object-position: 50% 15%`).

### 2. Update Career / Experience
In `index.html`, find the `<!-- CAREER -->` section.
Each role is a `.tl-item` block:

```html
<div class="tl-item reveal">
  <div class="tl-dot"></div>
  <div class="tl-card">
    <div class="tl-header">
      <div><span class="tl-role">Job Title <span class="tl-company co-target">Company</span></span></div>
      <div class="tl-date">Month Year – Month Year · City, ST</div>
    </div>
    <ul class="tl-points">
      <li>Achievement or responsibility here.</li>
    </ul>
    <div class="tl-tags">
      <span class="tl-tag">Tech</span><span class="tl-tag">Stack</span>
    </div>
  </div>
</div>
```

Company badge color classes:
- `co-target` → red (Target)
- `co-morgan` → blue (Morgan Stanley)
- `co-mindagile` → green (Mindagile)
- Add new ones in the CSS `:root` area for new employers.

### 3. Update Skills / Percentages
Find the `<!-- SKILLS -->` section. Each skill bar looks like:

```html
<div class="skill-row">
  <span class="skill-name">Skill Name</span>
  <div class="skill-track"><div class="skill-fill" data-w="90"></div></div>
  <span class="skill-pct">90%</span>
</div>
```

Change `data-w="90"` and the `90%` label to update a skill bar.

To add a tech tag (bottom cloud), append inside `.tech-cloud`:
```html
<span class="tech-tag">New Tool</span>
```

### 4. Update Certifications
Find the `<!-- CERTIFICATIONS -->` section. Each cert card:

```html
<div class="cert-card reveal">
  <div class="cert-badge badge-gcp">GCP</div>
  <div class="cert-text">
    <strong>Certification Name</strong>
    <span>Issuer</span>
  </div>
</div>
```

Available badge classes (colored by brand):
| Class         | Color  | Use for          |
|---------------|--------|------------------|
| `badge-gcp`   | Green  | Google Cloud     |
| `badge-google`| Blue   | Google           |
| `badge-msft`  | Blue   | Microsoft        |
| `badge-ibm`   | Blue   | IBM              |
| `badge-ttd`   | Purple | The Trade Desk   |
| `badge-dlai`  | Orange | DeepLearning.AI  |
| `badge-mapr`  | Red    | MapR / Cloudera  |

### 5. Update Projects
Find the `<!-- PROJECTS -->` section. Each project card is a `.project-card` div.
Update the `href` links, `.project-name`, `.project-desc`, and `.project-tag` spans.

### 6. Update Stats Bar
Find the `<!-- STATS -->` section. Each stat counter:

```html
<div class="stat-num"><span class="count" data-target="10">0</span>+</div>
<div class="stat-label">Label</div>
```

Change `data-target="10"` to update the number. The `+` or `%` suffix is plain text after the `<span>`.

### 7. Update Contact / Links
Search for `mailto:` and `linkedin.com/in/` to update email and LinkedIn URL.

---

## Color Palette

| Variable       | Value     | Used for                  |
|----------------|-----------|---------------------------|
| `--bg`         | `#f8fafc` | Page background           |
| `--bg-hero`    | `#f0f4ff` | Hero section background   |
| `--card`       | `#ffffff` | Card backgrounds          |
| `--accent`     | `#2563eb` | Primary blue              |
| `--accent2`    | `#7c3aed` | Secondary purple          |
| `--gradient`   | blue→purple | Buttons, bars, rings    |
| `--text`       | `#0f172a` | Primary text              |
| `--text-sec`   | `#475569` | Secondary text            |
| `--text-muted` | `#94a3b8` | Muted / labels            |
| `--border`     | `#e2e8f0` | Card borders              |

---

## Deploy Flow

Changes are deployed automatically via GitHub Actions on every push to `main`.

```bash
# Make your edits to index.html, then:
git add index.html srujan.jpeg   # add only the files you changed
git commit -m "your message"
GIT_COMMITTER_EMAIL="<your-noreply-email>" \
GIT_COMMITTER_NAME="<your-name>" \
git commit --amend --author="<your-name> <<your-noreply-email>>" --no-edit
git push origin main
```

> **Why the special push?** GitHub's email-privacy setting blocks pushes that expose your personal email.
> The no-reply address format is: `{GitHub_user_id}+{username}@users.noreply.github.com`
> Find your ID at: https://api.github.com/users/{your-username}

Check deploy status: https://github.com/vanchasrujankumar/vanchasrujankumar.github.io/actions

---

## Animations Reference

| Effect           | How it works                                      |
|------------------|---------------------------------------------------|
| Hero blobs       | CSS `@keyframes blobFloat` on three blur'd divs   |
| Typewriter       | JS cycles phrases with character-level interval   |
| Scroll reveal    | `IntersectionObserver` adds `.visible` class      |
| Skill bars       | `IntersectionObserver` sets `width` from `data-w` |
| Stat counters    | `IntersectionObserver` increments number to target |
| Avatar ring      | CSS `@keyframes rotate` on gradient pseudo-element |
