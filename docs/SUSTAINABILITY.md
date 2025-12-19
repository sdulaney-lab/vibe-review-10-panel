# Vibe Review: Sustainability Specialist (Judge 10)
*Created: 2025-12-19*

The Sustainability Specialist - nicknamed "Carbon" - evaluates applications through the lens of Green Software Engineering principles.

---

## Why Sustainability Matters

Software has a carbon footprint. Every API call, image download, and CPU cycle consumes energy, which often comes from carbon-emitting sources. The tech industry accounts for approximately **2-4% of global carbon emissions** - comparable to the aviation industry.

As developers, we have the power to reduce this impact through conscious design choices.

---

## Green Software Foundation Principles

The Sustainability Specialist applies the [Green Software Foundation](https://greensoftware.foundation/) principles:

### 1. Carbon Efficiency
**Emit the least amount of carbon possible.**

**What Carbon looks for:**
- Deployment region carbon intensity
- Unnecessary computation
- Inefficient algorithms
- Redundant processes

### 2. Energy Efficiency
**Use the least amount of energy possible.**

**What Carbon looks for:**
- Asset optimization (images, bundles)
- Idle resource consumption
- Dark mode support (OLED energy savings)
- CPU-intensive operations

### 3. Carbon Awareness
**Do more when the electricity is cleaner, do less when it's dirtier.**

**What Carbon looks for:**
- Flexible workload scheduling
- Background job timing
- Batch processing during low-carbon periods

### 4. Hardware Efficiency
**Use the least amount of embodied carbon possible.**

**What Carbon looks for:**
- Server utilization efficiency
- Zombie infrastructure
- Over-provisioned resources
- Hardware lifecycle considerations

### 5. Measurement
**What you can't measure, you can't improve.**

**What Carbon looks for:**
- Carbon tracking implementation
- SCI scoring documentation
- Environmental impact disclosure

---

## Software Carbon Intensity (SCI)

The SCI formula provides a standard way to measure software carbon:

```
SCI = ((E × I) + M) per R
```

| Variable | Description | Example |
|----------|-------------|---------|
| E | Energy consumed | 0.05 kWh per request |
| I | Carbon intensity of electricity | 400 gCO2/kWh |
| M | Embodied carbon (hardware) | 5 gCO2 per request |
| R | Functional unit | Per user, per transaction |

**Example Calculation:**
```
E = 0.05 kWh
I = 400 gCO2/kWh
M = 5 gCO2

SCI = ((0.05 × 400) + 5) = 25 gCO2 per request
```

---

## Carbon Region Awareness

Not all cloud regions are equal in carbon intensity:

### Low Carbon Regions (Prefer These)
| Provider | Region | Why |
|----------|--------|-----|
| **Google Cloud** | europe-north1 (Finland) | Hydroelectric power |
| **AWS** | eu-north-1 (Stockholm) | Nordic renewable grid |
| **Azure** | Sweden Central | Renewable energy |
| **Google Cloud** | us-west1 (Oregon) | Carbon-neutral |

### High Carbon Regions (Avoid When Possible)
| Provider | Region | Why |
|----------|--------|-----|
| Various | Coal-heavy grids | High carbon intensity |
| Various | Peak demand times | Grid stress |

### Tools for Region Selection
- [Electricity Maps](https://electricitymap.org/) - Real-time carbon intensity
- [Google Cloud Carbon Footprint](https://cloud.google.com/carbon-footprint)
- [AWS Customer Carbon Footprint Tool](https://aws.amazon.com/aws-cost-management/aws-customer-carbon-footprint-tool/)

---

## P0-P3 Sustainability Classifications

### P0 - Critical (Blocks Deployment)

**High-Carbon Region with Alternatives:**
```
Issue: Application deployed to us-east-1 (high carbon) when users are primarily in EU
Impact: 3x carbon emissions vs eu-north-1
Action: Migrate to low-carbon region or add CDN edge locations
```

**Zombie Infrastructure:**
```
Issue: 5 unused Cloud Functions still running and consuming resources
Impact: Wasted energy and cost
Action: Audit and terminate unused resources
```

**Massive Unoptimized Assets:**
```
Issue: 4.8MB PNG hero image
Impact: ~2g CO2 per page view (at scale: tons annually)
Action: Compress to <200KB WebP
```

### P1 - High Priority (Fix Before Production)

**Unoptimized Images >1MB:**
```
Issue: Product images averaging 1.5MB each
Impact: High bandwidth, slow load, excess energy
Action: Implement image optimization pipeline
```

**Missing Dark Mode:**
```
Issue: Light-only theme on OLED displays
Impact: 30-50% more screen energy consumption
Action: Add dark mode with system preference detection
```

**Excessive Polling:**
```
Issue: API polling every 1 second
Impact: 86,400 requests/day per client
Action: WebSocket or minimum 30-second polling
```

### P2 - Medium (Fix in Next Sprint)

**Inefficient Algorithms:**
```
Issue: O(n²) sorting where O(n log n) would work
Impact: Unnecessary CPU cycles at scale
Action: Optimize algorithm or use built-in sort
```

**Excessive Tracking Scripts:**
```
Issue: 12 third-party analytics scripts
Impact: Added latency, bandwidth, processing
Action: Consolidate to 1-2 essential trackers
```

### P3 - Low (Nice to Have)

**Missing Environmental Disclosures:**
```
Issue: No information about environmental impact
Impact: User awareness, transparency
Action: Add environmental impact page/badge
```

**SCI Documentation:**
```
Issue: Carbon footprint not measured
Impact: Can't improve what you don't measure
Action: Implement SCI calculation and tracking
```

---

## Implementation Patterns

### Image Optimization

```html
<!-- Before: 4.8MB PNG -->
<img src="hero.png" alt="Hero image">

<!-- After: <200KB WebP with responsive sizes -->
<picture>
  <source
    srcset="hero-400.webp 400w, hero-800.webp 800w, hero-1200.webp 1200w"
    type="image/webp">
  <img
    src="hero-800.jpg"
    alt="Hero image"
    loading="lazy"
    decoding="async">
</picture>
```

### Dark Mode Implementation

```css
/* System preference detection */
@media (prefers-color-scheme: dark) {
  :root {
    --bg-color: #1a1a1a;
    --text-color: #ffffff;
  }
}

/* Manual toggle support */
[data-theme="dark"] {
  --bg-color: #1a1a1a;
  --text-color: #ffffff;
}
```

```javascript
// Respect system preference + allow override
const getTheme = () => {
  const saved = localStorage.getItem('theme');
  if (saved) return saved;
  return window.matchMedia('(prefers-color-scheme: dark)').matches
    ? 'dark'
    : 'light';
};
```

### Efficient Data Fetching

```javascript
// Before: Polling every second
setInterval(() => fetch('/api/data'), 1000);

// After: WebSocket for real-time updates
const ws = new WebSocket('wss://api.example.com/stream');
ws.onmessage = (event) => updateData(JSON.parse(event.data));

// Or: Long polling with exponential backoff
async function pollWithBackoff(baseDelay = 5000) {
  try {
    const data = await fetch('/api/data');
    processData(data);
    setTimeout(() => pollWithBackoff(baseDelay), baseDelay);
  } catch {
    setTimeout(() => pollWithBackoff(baseDelay * 2), baseDelay * 2);
  }
}
```

### Lazy Loading

```javascript
// Intersection Observer for images
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src;
      observer.unobserve(img);
    }
  });
});

document.querySelectorAll('img[data-src]').forEach(img => {
  observer.observe(img);
});
```

---

## Measurement Tools

### Website Carbon Calculator
https://www.websitecarbon.com/

Enter a URL to estimate carbon per page view.

### Lighthouse
```bash
lighthouse https://example.com --output json
# Check "total-byte-weight" audit
```

### Custom SCI Implementation

```javascript
// Simple SCI tracker
class CarbonTracker {
  constructor(regionIntensity = 400) { // gCO2/kWh
    this.intensity = regionIntensity;
    this.requests = 0;
    this.bytesTransferred = 0;
  }

  trackRequest(bytes) {
    this.requests++;
    this.bytesTransferred += bytes;
  }

  calculateSCI() {
    // Simplified: ~0.0001 kWh per MB transferred
    const energy = (this.bytesTransferred / 1024 / 1024) * 0.0001;
    const embodied = this.requests * 0.001; // gCO2 per request
    return (energy * this.intensity) + embodied;
  }

  report() {
    return {
      requests: this.requests,
      bytesTransferred: this.bytesTransferred,
      estimatedCO2: this.calculateSCI().toFixed(2) + ' gCO2'
    };
  }
}
```

---

## Sustainability Checklist

### Quick Wins (Low Effort, High Impact)
- [ ] Compress images to WebP format
- [ ] Enable gzip/brotli compression
- [ ] Add `loading="lazy"` to images
- [ ] Implement dark mode
- [ ] Remove unused CSS/JS

### Medium Effort
- [ ] Replace polling with WebSocket
- [ ] Implement code splitting
- [ ] Add service worker caching
- [ ] Audit and remove unused dependencies
- [ ] Optimize database queries

### Strategic (High Effort, High Impact)
- [ ] Choose low-carbon hosting region
- [ ] Implement SCI measurement
- [ ] Carbon-aware job scheduling
- [ ] Regular infrastructure audits
- [ ] Environmental impact disclosure

---

## Resources

- [Green Software Foundation](https://greensoftware.foundation/)
- [Principles of Green Software](https://principles.green/)
- [Software Carbon Intensity Specification](https://sci.greensoftware.foundation/)
- [Sustainable Web Design](https://sustainablewebdesign.org/)
- [Website Carbon Calculator](https://www.websitecarbon.com/)
- [Electricity Maps](https://electricitymap.org/)
