# Unspoken: Reaction & Thread System Redesign
**Date:** February 15, 2026  
**Status:** Design spec for ChatGPT Pro review

---

## Problem Statement

Current reactions (❤️ heart, 💬 comment bubble, 🤝 handshake) are unclear:
- **Heart** = obvious like/love, but generic
- **Handshake** = "me too"? Agreement? Users don't instinctively know
- **Comment bubble** = looks like it should open replies, but currently just shows a count

The reactions need to be **emotionally specific to anonymous confessions** — not generic social media likes. People reading secrets have specific gut reactions: shock, boredom, solidarity, empathy. The UI should let them express those quickly.

The thread/reply system also needs proper UX — click to reply should open a full thread view, not just increment a counter.

---

## Research: What Works in Anonymous Platforms

### Whisper App
- Heart reactions (simple love/support)
- Reply system opens inline chat thread
- "Me too" feature was their most viral mechanic — solidarity in anonymity

### Reddit Confessions
- Upvote/downvote (engagement ranking)
- Comment threads with nesting
- Award system (gold, silver) for standout posts
- Sorting: Best, Top, New, Controversial

### PostSecret
- Mostly one-way (post → read), minimal interaction
- Community formed around shared vulnerability

### Key Insight
The magic of anonymous platforms is **low-friction emotional expression**. Users want to react instantly without composing a message. But when they DO want to reply, the thread should feel like a safe conversation space.

---

## Proposed Reaction System

### The 4 Reactions

Replace ❤️ 💬 🤝 with reactions that match how people actually respond to secrets:

| Reaction | Icon | Meaning | Why It Works |
|---|---|---|---|
| **"Me too"** | 🫂 (hug) | "I relate to this" / solidarity | The #1 reason people engage with confessions — feeling less alone. The hug emoji is warmer than a handshake. |
| **"OMG"** | 😱 | Shock / disbelief / jaw-drop | For the wild confessions. "You did WHAT?!" This is the reaction you can't suppress. |
| **"Meh"** | 🥱 | Boring / unimpressive / eye-roll | Mike's request. Honest feedback. Not everything is interesting. Gives users a way to signal "try harder" without being cruel. Also helps with ranking — low meh = quality indicator. |
| **"Reply"** | 💬 | Open thread to respond | Not a reaction counter — it's a **thread entry point**. Shows reply count as badge. |

### Why These 4?

They cover the **emotional spectrum of reading secrets**:
- **Positive connection** → 🫂 Me Too
- **Shock/excitement** → 😱 OMG  
- **Dismissal** → 🥱 Meh
- **Engagement** → 💬 Reply (N)

No thumbs up needed — "Me too" is MORE powerful for this context. A thumbs up says "good post." A hug says "I've been there." That's the difference.

### Visual Design

```
┌─────────────────────────────────────┐
│  Secret card text...                │
│                                     │
│  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────────┐
│  │ 🫂 42 │ │ 😱 18 │ │ 🥱 3  │ │ 💬 7 replies│
│  └──────┘ └──────┘ └──────┘ └──────────┘
│                                #relationships
└─────────────────────────────────────┘
```

- Reactions are pill-shaped buttons with icon + count
- Tapping a reaction toggles it (can only have one active per secret — exclusive, like Facebook reactions)
- OR: allow multiple (you can be both 🫂 AND 😱 about the same secret) — **recommend allowing multiple** since emotions aren't exclusive
- Active reaction gets a subtle glow/highlight in its color
- Reply button is visually distinct — slightly larger, shows "N replies" text instead of just a number
- On hover: tooltip with reaction name ("Me too", "OMG", "Meh")

### Reaction Colors (subtle, on active state)
- 🫂 Me Too → warm amber/orange glow
- 😱 OMG → electric purple glow  
- 🥱 Meh → muted grey glow
- 💬 Reply → blue glow (action color)

### Animation on React
- Icon does a quick bounce (scale 1 → 1.3 → 1, 200ms spring)
- Count increments with a subtle slide-up animation (old number slides up and out, new number slides up from below)
- If first reaction on this secret: pills do a subtle "noticed" shimmer

---

## Thread / Reply System Redesign

### Current Problem
Clicking 💬 on a card just increments a counter. There's no way to actually read or write replies from the feed view.

### New Flow

#### On the Feed Card
- Reply button shows: `💬 7 replies` (not just a number)
- Tapping the reply button OR tapping the card opens the **Detail View**
- The card itself is clickable (as it already is) — opens detail view

#### Detail View (Full Page Overlay)

When you open a secret, it takes over the screen (like current modal, but improved):

```
┌─────────────────────────────────────────┐
│  ← Back                     ···  Share  │
│─────────────────────────────────────────│
│                                         │
│  [Avatar gradient]                      │
│  Anonymous_Raven42 · 3 hours ago        │
│                                         │
│  "I've been pretending to be happy at   │
│   work for 2 years. Nobody knows I cry  │
│   in my car before going inside."       │
│                                         │
│  #work  #mental-health                  │
│                                         │
│  ┌──────┐ ┌──────┐ ┌──────┐           │
│  │ 🫂 847 │ │ 😱 234 │ │ 🥱 12  │           │
│  └──────┘ └──────┘ └──────┘           │
│                                         │
│─────────────────────────────────────────│
│  💬 23 Anonymous Responses              │
│─────────────────────────────────────────│
│                                         │
│  [gradient avatar]                      │
│  Hidden_Fox · 2h ago                    │
│  "Same here. 4 years. It gets easier    │
│   to fake it but harder to feel real."  │
│                                    🫂 12 │
│                                         │
│  [gradient avatar]                      │
│  Silent_River · 1h ago                  │
│  "Have you tried talking to someone?    │
│   I started therapy and it changed      │
│   everything."                          │
│                                    🫂 28 │
│                                         │
│  [gradient avatar]                      │
│  Midnight_Echo · 45m ago               │
│  "The car thing... I do the exact same  │
│   thing. Parking garage, level 3,       │
│   every morning."                       │
│                                 🫂 8 😱 3│
│                                         │
│  ... more replies ...                   │
│                                         │
│─────────────────────────────────────────│
│  [Reply anonymously...]          [Send] │
└─────────────────────────────────────────┘
```

#### Key Design Decisions

**1. Reply reactions are simpler**
- Replies only get 🫂 (me too) and 😱 (OMG) — no meh on replies (don't want to discourage conversation)
- Small, inline, right-aligned

**2. Reply entry is always visible**
- Sticky at the bottom of the detail view
- Textarea with placeholder "Reply anonymously..."
- Send button
- Character limit: 500 chars (keeps replies focused)
- Counter shows remaining chars when >400

**3. Reply sorting**
- Default: "Most relatable" (sorted by 🫂 count)
- Option to switch to "Newest first"
- Pinned reply: if the original poster replies, it's pinned at top with "OP" badge (still anonymous name)

**4. Reply count on feed cards**
- Shows actual reply count: "💬 7 replies" 
- If 0 replies: "💬 Reply" (invitation to be first)
- If replies exist but user hasn't seen them: subtle dot indicator (like unread)

**5. Thread depth**
- **No nested replies** — flat thread only. Nesting creates complexity and moderation headaches in anonymous contexts.
- Users can @mention other anonymous names in replies: "@Hidden_Fox exactly this"
- Mentioned user gets highlighted in the reply

**6. Navigating to detail view**
- From feed: card click OR reply button click → smooth slide-up animation
- URL updates to `#/s/{id}` (shareable, bookmarkable)
- Back button → smooth slide-down back to feed (remembers scroll position)
- Swipe right to go back (mobile)

---

## Data Model Changes

### Current Secret Object
```javascript
{
  id: 1,
  username: "Anonymous_Raven42",
  text: "...",
  topic: "work",
  timestamp: "3 hours ago",
  hearts: 847,      // ← REMOVE
  comments: 234,    // ← RENAME to replyCount
  metoo: 156,       // ← KEEP (rename from metoo to hugs)
  commentsList: []  // ← RENAME to replies
}
```

### New Secret Object
```javascript
{
  id: 1,
  username: "Anonymous_Raven42",
  text: "...",
  topic: "work",
  timestamp: "3 hours ago",
  
  // Reactions (new system)
  reactions: {
    hug: 847,        // 🫂 "Me too" / solidarity
    omg: 234,        // 😱 Shock
    meh: 12          // 🥱 Boring
  },
  
  // Thread
  replyCount: 23,
  replies: [
    {
      id: 101,
      user: "Hidden_Fox",
      text: "Same here. 4 years...",
      timestamp: "2h ago",
      reactions: { hug: 12, omg: 3 },
      isOP: false      // true if same poster as parent secret
    }
  ]
}
```

### Engagement Score Update
Current formula uses hearts + comments + metoo.
New formula:
```javascript
function calculateEngagementScore(secret) {
  const { hug, omg, meh } = secret.reactions;
  const replyCount = secret.replyCount;
  
  // Weighted scoring:
  // Hugs are strongest signal (emotional connection)
  // OMG is high engagement (viral potential)
  // Replies indicate active conversation
  // Meh is negative signal (reduces score)
  const score = (hug * 3) + (omg * 2) + (replyCount * 4) - (meh * 1);
  
  // Time decay (newer secrets get boost)
  const ageHours = getAgeInHours(secret.timestamp);
  const timeFactor = Math.max(0.5, 1 - (ageHours / 168)); // Decays over 1 week
  
  return Math.max(0, score * timeFactor);
}
```

Key: **Meh actively reduces ranking** — gives users real power to shape what surfaces. Replies are weighted highest because active conversation = most valuable content.

---

## Top 10 List Impact

The Top 10 ranking should update to use new engagement formula. Display on each Top 10 card:
- Show dominant reaction as badge (if 80%+ of reactions are 🫂, show "🫂 Most Relatable")
- Badges: "🫂 Most Relatable" / "😱 Most Shocking" / "💬 Most Discussed"
- This gives the Top 10 personality — not just "most popular" but categorized by WHY they're popular

---

## Feed Card Updates

### Before
```
❤️ 847  💬 234  🤝 156
```

### After  
```
🫂 847  😱 234  🥱 12  │  💬 23 replies
```

The reply button is visually separated from reactions (thin divider line) to make it clear it's a different action — reactions are one-tap expressions, reply opens a conversation.

---

## Submit Secret Form Updates

Current form has "Allow comments" toggle. Update to:
- **"Allow replies"** toggle (default ON)
- **"Allow reactions"** toggle (default ON) — some users may want to share without feedback
- Add topic multi-select (can tag up to 3 topics)

---

## Mobile Considerations

- Reactions should be large enough for thumb taps (min 44px touch target)
- On mobile, detail view is full-screen (not modal overlay)
- Reply textarea should auto-grow but cap at 4 lines before scrolling
- Swipe gestures: left-swipe on feed card → quick react (🫂), right-swipe → open detail
- Pull-to-refresh on feed

---

## Implementation Priority

1. **Replace reaction icons + data model** (quick, visual change)
2. **Fix reply button to open detail view** (UX flow)
3. **Improve detail view** (full-page layout, better reply display)
4. **Add reply entry at bottom of detail** (functional)
5. **Update engagement scoring** (ranking algorithm)
6. **Add reply reactions** (🫂 and 😱 on individual replies)
7. **Top 10 badges** (polish)
8. **Mobile swipe gestures** (polish)

---

## Questions for ChatGPT Pro

1. Should reactions be exclusive (pick one) or allow multiple per secret?
2. Is 🫂 (hug) universally understood, or should we use something more explicit?
3. Should 🥱 (meh) be visible to the poster, or only used for ranking? (Seeing "50 people think your secret is boring" could be hurtful)
4. Should there be a "report" mechanism hidden in the ··· menu?
5. For the detail view — full-page takeover or side-panel on desktop?
6. Should replies have a minimum character count to prevent low-effort "lol" responses?
7. Is there value in a "🔥 Trending" reaction for secrets gaining velocity?
8. How should we handle reply moderation in an anonymous context?

---

**Document prepared by:** Otto  
**Next:** Send to ChatGPT Pro for deep thinking, then implement
