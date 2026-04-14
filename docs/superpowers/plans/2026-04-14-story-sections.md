# Story Sections & Light Mode Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add two horizontal-sliding storytelling sections (Before/After IoT) between Hero and "What is Industrial IoT?", and switch default theme to light mode with persistence.

**Architecture:** Single-file changes to `index.html`. Add CSS for the slideshow component in the existing `<style>` block, add two new `<section>` elements after Hero, add slideshow JS logic in the existing `<script>` block. No external dependencies — pure HTML/CSS/JS with Tailwind.

**Tech Stack:** HTML, Tailwind CSS (via CDN), vanilla JavaScript

**Spec:** `docs/superpowers/specs/2026-04-14-story-sections-design.md`

---

### Task 1: Switch Default Theme to Light Mode with localStorage Persistence

**Files:**
- Modify: `index.html:2` (html tag)
- Modify: `index.html:1522-1526` (theme toggle script)

- [ ] **Step 1: Remove `dark` class from html tag**

Change line 2 from:
```html
<html lang="en" class="dark scroll-smooth">
```
to:
```html
<html lang="en" class="scroll-smooth">
```

- [ ] **Step 2: Add localStorage persistence to theme toggle and initial load**

Replace the existing theme toggle script (lines 1523-1526):
```javascript
// Theme Toggle
document.getElementById('themeToggle').addEventListener('click', () => {
    document.documentElement.classList.toggle('dark');
});
```
with:
```javascript
// Theme Toggle with localStorage persistence
(function() {
    const saved = localStorage.getItem('theme');
    if (saved === 'dark') {
        document.documentElement.classList.add('dark');
    }
})();
document.getElementById('themeToggle').addEventListener('click', () => {
    document.documentElement.classList.toggle('dark');
    const isDark = document.documentElement.classList.contains('dark');
    localStorage.setItem('theme', isDark ? 'dark' : 'light');
});
```

- [ ] **Step 3: Verify in browser**

Open `index.html` in browser. Confirm:
- Page loads in light mode (white background)
- Clicking the moon icon switches to dark mode
- Refreshing the page keeps dark mode
- Clicking back to light and refreshing keeps light mode

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: switch default theme to light mode with localStorage persistence"
```

---

### Task 2: Add Slideshow CSS Styles

**Files:**
- Modify: `index.html:56-110` (inside existing `<style>` block, after the existing styles before `</style>`)

- [ ] **Step 1: Add slideshow CSS before the closing `</style>` tag (line 110)**

Insert the following CSS just before `</style>` on line 110:

```css
/* Slideshow */
.slideshow-container {
    position: relative;
    overflow: hidden;
    width: 100%;
}
.slideshow-track {
    display: flex;
    transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}
.slideshow-slide {
    min-width: 100%;
    padding: 0 2rem;
    box-sizing: border-box;
}
.slideshow-slide .slide-content {
    display: flex;
    align-items: center;
    gap: 3rem;
    max-width: 72rem;
    margin: 0 auto;
}
.slideshow-slide .slide-content.reverse {
    flex-direction: row-reverse;
}
.slideshow-slide .slide-image {
    flex: 1;
    min-width: 0;
}
.slideshow-slide .slide-image img {
    width: 100%;
    height: auto;
    border-radius: 1rem;
}
.slideshow-slide .slide-image .image-placeholder {
    width: 100%;
    aspect-ratio: 3/2;
    border-radius: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.875rem;
}
.slideshow-slide .slide-text {
    flex: 1;
    min-width: 0;
}
.slideshow-arrow {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    z-index: 10;
    width: 3rem;
    height: 3rem;
    border-radius: 9999px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: all 0.2s ease;
    border: none;
}
.slideshow-arrow:hover {
    transform: translateY(-50%) scale(1.1);
}
.slideshow-arrow.prev { left: 1rem; }
.slideshow-arrow.next { right: 1rem; }
.slideshow-arrow:disabled {
    opacity: 0.3;
    cursor: default;
}
.slideshow-arrow:disabled:hover {
    transform: translateY(-50%) scale(1);
}
.slideshow-dots {
    display: flex;
    justify-content: center;
    gap: 0.5rem;
    margin-top: 1.5rem;
}
.slideshow-dots button {
    width: 0.625rem;
    height: 0.625rem;
    border-radius: 9999px;
    border: none;
    cursor: pointer;
    transition: all 0.3s ease;
    opacity: 0.4;
}
.slideshow-dots button.active {
    opacity: 1;
    transform: scale(1.4);
}

@media (max-width: 768px) {
    .slideshow-slide .slide-content,
    .slideshow-slide .slide-content.reverse {
        flex-direction: column;
        gap: 1.5rem;
    }
    .slideshow-slide {
        padding: 0 1rem;
    }
    .slideshow-arrow {
        width: 2.25rem;
        height: 2.25rem;
    }
    .slideshow-arrow.prev { left: 0.5rem; }
    .slideshow-arrow.next { right: 0.5rem; }
}
```

- [ ] **Step 2: Verify CSS loads without errors**

Open browser, confirm no visual breakage on existing sections. The new CSS doesn't affect anything yet.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add slideshow CSS styles for story sections"
```

---

### Task 3: Add "Before" Story Section HTML

**Files:**
- Modify: `index.html` — insert new section after `</section>` of Hero (after line 180), before `<!-- SECTION 2: WHAT IS IoT -->`

- [ ] **Step 1: Insert the "Before" story section HTML**

Insert the following after the closing `</section>` of the Hero section (line 180) and before the `<!-- SECTION 2: WHAT IS IoT -->` comment:

```html
    <!-- ==================== STORY: BEFORE (Without IoT) ==================== -->
    <section id="story-before" class="snap-section grid-bg flex flex-col items-center justify-center px-6 py-20">
        <div class="max-w-6xl mx-auto w-full">
            <div class="text-center mb-12 fade-up">
                <p class="text-red-500 font-semibold text-sm tracking-wider uppercase mb-3">The Daily Reality</p>
                <h2 class="text-4xl md:text-5xl font-bold mb-4">Without Smart Monitoring</h2>
                <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">A story every factory manager knows too well</p>
            </div>

            <div class="slideshow-container fade-up" data-slideshow="before">
                <!-- Prev Arrow -->
                <button class="slideshow-arrow prev bg-white dark:bg-gray-800 shadow-lg text-gray-700 dark:text-gray-200" onclick="slideshowPrev('before')" disabled>
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/></svg>
                </button>
                <!-- Next Arrow -->
                <button class="slideshow-arrow next bg-white dark:bg-gray-800 shadow-lg text-gray-700 dark:text-gray-200" onclick="slideshowNext('before')">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/></svg>
                </button>

                <div class="slideshow-track">
                    <!-- Slide 1: The Factory Floor (image left) -->
                    <div class="slideshow-slide">
                        <div class="slide-content">
                            <div class="slide-image">
                                <div class="image-placeholder bg-red-50 dark:bg-red-950/20 border-2 border-dashed border-red-200 dark:border-red-800 text-red-400">
                                    <span>Image: Factory Floor</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 text-xs font-semibold mb-4">Step 1 of 7</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">The Factory Floor</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">A busy factory with 20+ CNC machines. Operators at their stations. The hum of production. Everything looks like it's running fine — but is it?</p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 2: The Owner's Call (image right / reverse) -->
                    <div class="slideshow-slide">
                        <div class="slide-content reverse">
                            <div class="slide-image">
                                <div class="image-placeholder bg-red-50 dark:bg-red-950/20 border-2 border-dashed border-red-200 dark:border-red-800 text-red-400">
                                    <span>Image: Owner's Call</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 text-xs font-semibold mb-4">Step 2 of 7</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">The Owner's Call</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">Owner picks up the phone and calls the manager: <strong class="text-gray-900 dark:text-white">"How many machines are running right now? How many are switched off?"</strong></p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 3: More Questions (image left) -->
                    <div class="slideshow-slide">
                        <div class="slide-content">
                            <div class="slide-image">
                                <div class="image-placeholder bg-red-50 dark:bg-red-950/20 border-2 border-dashed border-red-200 dark:border-red-800 text-red-400">
                                    <span>Image: Questions Pile Up</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 text-xs font-semibold mb-4">Step 3 of 7</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">More Questions Pile Up</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed"><strong class="text-gray-900 dark:text-white">"Which batch is each machine working on? How many pieces are done? What about voltage and temperature?"</strong> The questions keep coming.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 4: The Manual Count (image right / reverse) -->
                    <div class="slideshow-slide">
                        <div class="slide-content reverse">
                            <div class="slide-image">
                                <div class="image-placeholder bg-red-50 dark:bg-red-950/20 border-2 border-dashed border-red-200 dark:border-red-800 text-red-400">
                                    <span>Image: Manual Count</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 text-xs font-semibold mb-4">Step 4 of 7</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">The Manual Count</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">Manager puts down the phone, grabs a clipboard, and starts walking machine to machine. Checking each one. Asking operators. Writing on paper.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 5: Hours Pass (image left) -->
                    <div class="slideshow-slide">
                        <div class="slide-content">
                            <div class="slide-image">
                                <div class="image-placeholder bg-red-50 dark:bg-red-950/20 border-2 border-dashed border-red-200 dark:border-red-800 text-red-400">
                                    <span>Image: Hours Pass</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 text-xs font-semibold mb-4">Step 5 of 7</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">Hours Pass...</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">The owner is still waiting. It's been <strong class="text-gray-900 dark:text-white">2 hours</strong>. Meanwhile, machines have changed status — some stopped, some started. The data is already stale.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 6: Report Has Errors (image right / reverse) -->
                    <div class="slideshow-slide">
                        <div class="slide-content reverse">
                            <div class="slide-image">
                                <div class="image-placeholder bg-red-50 dark:bg-red-950/20 border-2 border-dashed border-red-200 dark:border-red-800 text-red-400">
                                    <span>Image: Report Errors</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 text-xs font-semibold mb-4">Step 6 of 7</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">The Report Has Errors</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">Manager finally calls back with numbers. But 3 machines changed state while he was counting. The numbers don't add up. <strong class="text-red-500">Owner is frustrated.</strong></p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 7: Every Single Day (image left) -->
                    <div class="slideshow-slide">
                        <div class="slide-content">
                            <div class="slide-image">
                                <div class="image-placeholder bg-red-50 dark:bg-red-950/20 border-2 border-dashed border-red-200 dark:border-red-800 text-red-400">
                                    <span>Image: Every Single Day</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400 text-xs font-semibold mb-4">Step 7 of 7</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">Every. Single. Day.</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">This isn't a one-time problem. This is the <strong class="text-gray-900 dark:text-white">daily reality</strong>. The manager dreads the owner's call. The owner can never trust the numbers. Decisions are based on guesswork.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Dots -->
                <div class="slideshow-dots" data-dots="before">
                    <button class="bg-red-500 active" onclick="slideshowGo('before',0)"></button>
                    <button class="bg-red-500" onclick="slideshowGo('before',1)"></button>
                    <button class="bg-red-500" onclick="slideshowGo('before',2)"></button>
                    <button class="bg-red-500" onclick="slideshowGo('before',3)"></button>
                    <button class="bg-red-500" onclick="slideshowGo('before',4)"></button>
                    <button class="bg-red-500" onclick="slideshowGo('before',5)"></button>
                    <button class="bg-red-500" onclick="slideshowGo('before',6)"></button>
                </div>
            </div>
        </div>
    </section>
```

- [ ] **Step 2: Verify the section appears in the browser**

Open in browser. The section should appear after Hero with placeholder image boxes. Arrows and dots won't work yet (JS not added). Confirm layout and text render correctly.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add Before story section HTML with 7 slides"
```

---

### Task 4: Add "After" Story Section HTML

**Files:**
- Modify: `index.html` — insert new section after the "Before" section's closing `</section>`, before `<!-- SECTION 2: WHAT IS IoT -->`

- [ ] **Step 1: Insert the "After" story section HTML**

Insert directly after the "Before" section's closing `</section>`:

```html
    <!-- ==================== STORY: AFTER (With IoT) ==================== -->
    <section id="story-after" class="snap-section grid-bg flex flex-col items-center justify-center px-6 py-20">
        <div class="max-w-6xl mx-auto w-full">
            <div class="text-center mb-12 fade-up">
                <p class="text-accent-500 font-semibold text-sm tracking-wider uppercase mb-3">The Smart Way</p>
                <h2 class="text-4xl md:text-5xl font-bold mb-4">Now Imagine This Instead...</h2>
                <p class="text-lg text-gray-600 dark:text-gray-400 max-w-2xl mx-auto">Same factory, same questions — completely different experience</p>
            </div>

            <div class="slideshow-container fade-up" data-slideshow="after">
                <!-- Prev Arrow -->
                <button class="slideshow-arrow prev bg-white dark:bg-gray-800 shadow-lg text-gray-700 dark:text-gray-200" onclick="slideshowPrev('after')" disabled>
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"/></svg>
                </button>
                <!-- Next Arrow -->
                <button class="slideshow-arrow next bg-white dark:bg-gray-800 shadow-lg text-gray-700 dark:text-gray-200" onclick="slideshowNext('after')">
                    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"/></svg>
                </button>

                <div class="slideshow-track">
                    <!-- Slide 1: Same Question (image left) -->
                    <div class="slideshow-slide">
                        <div class="slide-content">
                            <div class="slide-image">
                                <div class="image-placeholder bg-green-50 dark:bg-green-950/20 border-2 border-dashed border-green-200 dark:border-green-800 text-green-500">
                                    <span>Image: Same Question</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-green-100 dark:bg-green-900/30 text-green-600 dark:text-green-400 text-xs font-semibold mb-4">Step 1 of 6</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">Same Question</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">Owner asks: <strong class="text-gray-900 dark:text-white">"What's the factory status?"</strong> Same question as before. But this time, the answer is seconds away.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 2: Instant Answer (image right / reverse) -->
                    <div class="slideshow-slide">
                        <div class="slide-content reverse">
                            <div class="slide-image">
                                <div class="image-placeholder bg-green-50 dark:bg-green-950/20 border-2 border-dashed border-green-200 dark:border-green-800 text-green-500">
                                    <span>Image: Instant Answer</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-green-100 dark:bg-green-900/30 text-green-600 dark:text-green-400 text-xs font-semibold mb-4">Step 2 of 6</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">Instant Answer</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">Manager pulls out his phone, opens the app. Within <strong class="text-accent-500">5 seconds</strong>: "12 machines running, 3 idle, 2 in maintenance. Batch #47 is 78% complete."</p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 3: Every Detail (image left) -->
                    <div class="slideshow-slide">
                        <div class="slide-content">
                            <div class="slide-image">
                                <div class="image-placeholder bg-green-50 dark:bg-green-950/20 border-2 border-dashed border-green-200 dark:border-green-800 text-green-500">
                                    <span>Image: Every Detail</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-green-100 dark:bg-green-900/30 text-green-600 dark:text-green-400 text-xs font-semibold mb-4">Step 3 of 6</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">Every Detail, One Tap</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">Tap any machine on the dashboard — see temperature, voltage, RPM, output count, batch info. <strong class="text-gray-900 dark:text-white">All live data.</strong> No walking around needed.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 4: Owner Checks From Anywhere (image right / reverse) -->
                    <div class="slideshow-slide">
                        <div class="slide-content reverse">
                            <div class="slide-image">
                                <div class="image-placeholder bg-green-50 dark:bg-green-950/20 border-2 border-dashed border-green-200 dark:border-green-800 text-green-500">
                                    <span>Image: From Anywhere</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-green-100 dark:bg-green-900/30 text-green-600 dark:text-green-400 text-xs font-semibold mb-4">Step 4 of 6</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">Owner Checks From Anywhere</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">The owner doesn't even need to call. He opens the same app from home, from his car, from the office. He sees everything the manager sees. <strong class="text-gray-900 dark:text-white">Real-time, always accurate.</strong></p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 5: Alerts Come to You (image left) -->
                    <div class="slideshow-slide">
                        <div class="slide-content">
                            <div class="slide-image">
                                <div class="image-placeholder bg-green-50 dark:bg-green-950/20 border-2 border-dashed border-green-200 dark:border-green-800 text-green-500">
                                    <span>Image: Alerts</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-green-100 dark:bg-green-900/30 text-green-600 dark:text-green-400 text-xs font-semibold mb-4">Step 5 of 6</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">Alerts Come to You</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">Machine overheating? Unexpected shutdown? You get a <strong class="text-gray-900 dark:text-white">notification instantly</strong>. Problems find you — you don't have to discover them.</p>
                            </div>
                        </div>
                    </div>

                    <!-- Slide 6: Confidence & Control (image right / reverse) -->
                    <div class="slideshow-slide">
                        <div class="slide-content reverse">
                            <div class="slide-image">
                                <div class="image-placeholder bg-green-50 dark:bg-green-950/20 border-2 border-dashed border-green-200 dark:border-green-800 text-green-500">
                                    <span>Image: Confidence</span>
                                </div>
                            </div>
                            <div class="slide-text">
                                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-green-100 dark:bg-green-900/30 text-green-600 dark:text-green-400 text-xs font-semibold mb-4">Step 6 of 6</div>
                                <h3 class="text-2xl md:text-3xl font-bold mb-4">Confidence & Control</h3>
                                <p class="text-gray-600 dark:text-gray-400 text-lg leading-relaxed">Every number is accurate. Every decision is data-driven. The owner trusts the reports. The manager is free to <strong class="text-accent-500">focus on real work</strong>, not counting machines.</p>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Dots -->
                <div class="slideshow-dots" data-dots="after">
                    <button class="bg-accent-500 active" onclick="slideshowGo('after',0)"></button>
                    <button class="bg-accent-500" onclick="slideshowGo('after',1)"></button>
                    <button class="bg-accent-500" onclick="slideshowGo('after',2)"></button>
                    <button class="bg-accent-500" onclick="slideshowGo('after',3)"></button>
                    <button class="bg-accent-500" onclick="slideshowGo('after',4)"></button>
                    <button class="bg-accent-500" onclick="slideshowGo('after',5)"></button>
                </div>
            </div>
        </div>
    </section>
```

- [ ] **Step 2: Verify in browser**

Both story sections should now be visible after Hero. Confirm text, layout, and placeholder images render.

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add After story section HTML with 6 slides"
```

---

### Task 5: Add Slideshow JavaScript Logic

**Files:**
- Modify: `index.html` — add JS inside the existing `<script>` block, after the theme toggle code

- [ ] **Step 1: Add slideshow state and control functions**

Insert the following JavaScript after the theme toggle code (after the closing `});` of the theme toggle listener):

```javascript
// Slideshow logic
const slideshows = {};

function initSlideshow(name) {
    const container = document.querySelector('[data-slideshow="' + name + '"]');
    if (!container) return;
    const track = container.querySelector('.slideshow-track');
    const slides = track.querySelectorAll('.slideshow-slide');
    const dots = container.querySelector('.slideshow-dots').querySelectorAll('button');
    const prevBtn = container.querySelector('.slideshow-arrow.prev');
    const nextBtn = container.querySelector('.slideshow-arrow.next');

    slideshows[name] = { track, slides, dots, prevBtn, nextBtn, current: 0, total: slides.length };
    updateSlideshow(name);
}

function updateSlideshow(name) {
    const s = slideshows[name];
    if (!s) return;
    s.track.style.transform = 'translateX(-' + (s.current * 100) + '%)';
    s.prevBtn.disabled = s.current === 0;
    s.nextBtn.disabled = s.current === s.total - 1;
    s.dots.forEach(function(dot, i) {
        dot.classList.toggle('active', i === s.current);
    });
}

function slideshowNext(name) {
    const s = slideshows[name];
    if (!s || s.current >= s.total - 1) return;
    s.current++;
    updateSlideshow(name);
}

function slideshowPrev(name) {
    const s = slideshows[name];
    if (!s || s.current <= 0) return;
    s.current--;
    updateSlideshow(name);
}

function slideshowGo(name, index) {
    const s = slideshows[name];
    if (!s || index < 0 || index >= s.total) return;
    s.current = index;
    updateSlideshow(name);
}

// Keyboard navigation for slideshows
document.addEventListener('keydown', function(e) {
    if (e.key === 'ArrowLeft' || e.key === 'ArrowRight') {
        var visible = null;
        Object.keys(slideshows).forEach(function(name) {
            var container = document.querySelector('[data-slideshow="' + name + '"]');
            var rect = container.getBoundingClientRect();
            if (rect.top < window.innerHeight * 0.5 && rect.bottom > window.innerHeight * 0.5) {
                visible = name;
            }
        });
        if (visible) {
            if (e.key === 'ArrowLeft') slideshowPrev(visible);
            if (e.key === 'ArrowRight') slideshowNext(visible);
        }
    }
});

initSlideshow('before');
initSlideshow('after');
```

- [ ] **Step 2: Verify slideshow works in browser**

Test the following:
- Click right arrow → slides advance with smooth animation
- Click left arrow → slides go back
- Left arrow is disabled on first slide
- Right arrow is disabled on last slide
- Clicking dots jumps to that slide
- Keyboard left/right arrows work when section is in viewport
- Both "Before" and "After" slideshows work independently

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add slideshow JavaScript logic with arrow and dot navigation"
```

---

### Task 6: Update Side Navigation Dots

**Files:**
- Modify: `index.html` — the `<nav id="sideNav">` block (lines 121-134)

- [ ] **Step 1: Add dots for the two new sections and update data-section indices**

Replace the entire `<nav id="sideNav">` block with:

```html
    <nav id="sideNav" class="fixed right-5 top-1/2 -translate-y-1/2 z-50 flex flex-col gap-3">
        <a href="#hero" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="0" title="Home"></a>
        <a href="#story-before" class="nav-dot w-3 h-3 rounded-full bg-red-500 opacity-50 hover:opacity-100 transition-all" data-section="1" title="Before IoT"></a>
        <a href="#story-after" class="nav-dot w-3 h-3 rounded-full bg-accent-500 opacity-50 hover:opacity-100 transition-all" data-section="2" title="After IoT"></a>
        <a href="#what-is-iot" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="3" title="What is IoT"></a>
        <a href="#problem" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="4" title="The Problem"></a>
        <a href="#how-it-works" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="5" title="How It Works"></a>
        <a href="#hardware-components" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="6" title="Hardware Components"></a>
        <a href="#full-architecture" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="7" title="Full Architecture"></a>
        <a href="#machine-types" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="8" title="Machine Types"></a>
        <a href="#data-capture" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="9" title="Data Capture"></a>
        <a href="#batch-mgmt" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="10" title="Batch Management"></a>
        <a href="#comm-layers" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="11" title="Communication"></a>
        <a href="#impact" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="12" title="Impact"></a>
        <a href="#dashboard" class="nav-dot w-3 h-3 rounded-full bg-brand-500 opacity-50 hover:opacity-100 transition-all" data-section="13" title="Dashboard"></a>
    </nav>
```

- [ ] **Step 2: Verify in browser**

Scroll through the page. Confirm:
- Side nav now has 14 dots (was 12)
- The "Before" dot is red, "After" dot is green
- Clicking the new dots scrolls to the correct sections
- Active dot highlighting works correctly as you scroll

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: update side navigation dots for new story sections"
```

---

### Task 7: Final Verification and Polish

**Files:**
- Modify: `index.html` (minor fixes if needed)

- [ ] **Step 1: Full page walkthrough**

Open `index.html` in browser and scroll through the entire page top to bottom. Verify:
- Page loads in light mode
- Hero section renders correctly
- "Before" section: all 7 slides navigate, zigzag layout works, arrows/dots functional
- "After" section: all 6 slides navigate, zigzag layout works, arrows/dots functional
- "What is Industrial IoT?" section follows after the two story sections
- All remaining sections render unchanged
- Side nav dots highlight correctly for all 14 sections
- Theme toggle works and persists

- [ ] **Step 2: Test mobile responsiveness**

Open browser dev tools, switch to mobile viewport (375px wide). Verify:
- Slide content stacks vertically (image on top, text below)
- Arrows are smaller and properly positioned
- Text is readable, not overflowing
- Dots are tappable

- [ ] **Step 3: Test dark mode**

Toggle to dark mode. Verify:
- Story sections have proper dark backgrounds
- Placeholder image boxes have dark borders
- Text contrast is good
- Arrows have dark background

- [ ] **Step 4: Commit if any fixes were needed**

```bash
git add index.html
git commit -m "fix: polish story sections after final review"
```
