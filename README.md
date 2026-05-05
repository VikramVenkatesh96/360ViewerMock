# Virtual Tour — GitHub Pages

A mobile-first 360° virtual tour with progressive image loading and an embedded AI chatbot.

## Folder Structure

```
/
├── index.html
├── images/
│   ├── exterior/
│   │   ├── 1/   low.png  med.png  high.jpg
│   │   ├── 2/   low.png  med.png  high.jpg
│   │   └── 3/   low.png  med.png  high.jpg
│   └── interior/
│       ├── 1/   low.jpg  med.jpg  high.jpg
│       ├── 2/   ...
│       └── 8/   low.jpg  med.jpg  high.jpg
└── README.md
```

## Deploy to GitHub Pages

1. Create a new GitHub repository (e.g. `virtual-tour`)
2. Upload all files maintaining the folder structure above
3. Go to **Settings → Pages → Source → Deploy from branch → main / (root)**
4. Your site will be live at `https://yourusername.github.io/virtual-tour/`

## Customising Scene Names & Hotspots

Open `index.html` and find the `SCENES` array near the top of the `<script>` tag.

Each scene looks like:
```js
{
  id: "ext1",           // unique ID
  group: "Exterior",    // tab group label
  name: "Exterior 1",   // display name
  low:  "images/exterior/1/low.png",
  med:  "images/exterior/1/med.png",
  high: "images/exterior/1/high.jpg",
  hotspots: [
    { pitch: -5, yaw: 60, text: "Next Scene", target: "ext2" }
  ]
}
```

- **pitch** — vertical angle of the hotspot arrow (-90 = floor, 90 = ceiling, 0 = horizon)
- **yaw** — horizontal angle (0 = front, 90 = right, -90 = left, 180 = behind)
- **target** — `id` of the scene to navigate to

## Customising the Chatbot Q&A

Find the `QA` array in `index.html`. Each entry:
```js
{
  keys: ["keyword1", "keyword2"],   // words that trigger this answer
  ans: "Your answer text here."
}
```

Add, remove, or edit entries freely. Anything not matched falls back to Claude AI,
which is also constrained to only discuss your property.

## Progressive Loading

Each scene loads in 3 stages:
1. **25% quality** — shown immediately (fast)
2. **50% quality** — swapped in silently once downloaded
3. **100% quality** — final HD swap, badge fades out

The viewer preserves your current pan/tilt angle between quality upgrades.
