# TellAnything Rebuild Task

Transform this "Unspoken" anonymous secrets site into "TellAnything" with major upgrades.

## 1. REBRAND: Unspoken → TellAnything
- Change all references from "Unspoken" to "TellAnything" 
- New tagline ideas: "What would you say if no one knew it was you?" or "The truth has no name"
- Update page title, meta tags, any branding text

## 2. HERO SECTION - Make it PROVOCATIVE and IMPRESSIVE
- Center the hero content both horizontally and vertically
- Make the headline more provocative and daring
- Parallax scroll effect: hero scrolls FASTER than the page (translateY at ~1.5x scroll speed) so it disappears quickly as you scroll
- Hero only returns if you scroll ALL the way back to top
- Add a subtle animated background (dark gradient mesh or floating particles)
- Make it feel cinematic and edgy - this is about raw truth, not a corporate site

## 3. NEW REACTION SYSTEM (replace current ❤️ 💬 🤝)
Replace with 4 new reactions:
- 🫂 "Me Too" (solidarity/relate) - replaces heart AND handshake  
- 😱 "OMG" (shock/disbelief)
- 🥱 "Meh" (boring/unimpressive)  
- 💬 "N replies" (thread entry point, shows reply count)

Design:
- Pill-shaped buttons with icon + count
- Users can select multiple reactions (not exclusive)
- Active reaction gets a subtle color glow (🫂=amber, 😱=purple, 🥱=grey, 💬=blue)
- Bounce animation on tap (scale 1→1.3→1, 200ms)
- Reply button visually separated from reaction pills
- On feed cards: show "💬 7 replies" not just a number. If 0: "💬 Reply"

## 4. PROVOCATIVE MOCK DATA - 25+ secrets
Make secrets WAY more provocative, shocking, funny, and real. Think:
- Dark humor confessions
- Workplace scandals  
- Relationship bombshells
- Embarrassing moments that are relatable
- Family secrets
- Things people would NEVER say out loud
- Mix of serious and funny
- Some should be short and punchy, others longer narratives

Each secret needs 3-8 realistic, fun, shocking replies in commentsList.
- Replies should feel like real anonymous people responding
- Mix of supportive, shocked, funny, judgmental responses
- Some reply threads should have back-and-forth conversation feel
- Reply counts in the data MUST match actual commentsList.length

## 5. THREAD SYSTEM
- Clicking a card or reply button opens full-page detail view
- Detail view shows: secret text, all reactions with counts, "N Anonymous Responses" header
- Flat reply list (no nesting)
- Each reply has mini-reactions (🫂 and 😱 only)
- Reply input sticky at bottom: textarea + Send button
- Character limit: 500
- Sort options: "Most Relatable" (by 🫂) or "Newest"
- Back button with smooth transition

## 6. ENGAGEMENT SCORING
New formula: (hug × 3) + (omg × 2) + (replyCount × 4) - (meh × 1) with time decay
Update the Top 10 ranking to use this.
Add personality badges on Top 10: "🫂 Most Relatable" / "😱 Most Shocking" / "💬 Most Discussed"

## 7. DATA MODEL
```javascript
{
  id: 1,
  username: "Anonymous_name",
  text: "...",
  topic: "topic",
  timestamp: "3 hours ago",
  reactions: { hug: N, omg: N, meh: N },
  replyCount: N,  // MUST equal replies.length
  replies: [
    { id: 101, user: "Name", text: "...", timestamp: "2h ago", reactions: { hug: N, omg: N }, isOP: false }
  ]
}
```

## 8. VISUAL POLISH
- Dark theme (keep the midnight vault aesthetic)
- Smooth animations on everything
- Feed cards should have subtle hover lift effect
- Topic filter pills should be more prominent
- Make it feel like a premium, slightly dangerous app

## IMPORTANT
- This is a SINGLE index.html file - all CSS, JS, and HTML inline
- Keep it under 100KB
- Must work on mobile
- Generate at least 25 secrets with 3-8 replies EACH
- All reply counts must match actual data
- Make it impressive enough to score 9/10

When completely finished, run: openclaw system event --text "Done: TellAnything rebuilt — rebranded, new reactions, provocative data, parallax hero, thread system" --mode now
