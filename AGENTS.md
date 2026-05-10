# Kathryn's Travel Fund Site - Context & Documentation

## Overview
This repository contains the code for a static webpage (`personal-project.html`) designed to serve as a travel fund site for Kathryn's Nordic Adventures. Visitors can view planned trips, see the estimated costs, click out to external links detailing the trips, and send funds via Venmo.

## Technical Architecture
- **Tech Stack:** Vanilla HTML, CSS, and JavaScript. No build step or external libraries are required.
- **Styling:** The site uses a responsive CSS Grid "Card" layout and a Scandinavian/Baltic aesthetic (icy blue backgrounds, forest green accents, and modern typography via Google Fonts' 'Outfit').
- **Data Storage:** Because this is a simple static site often opened directly from the filesystem (which causes CORS issues for fetching local CSVs), the data is **embedded directly in the HTML file** within a JavaScript array called `destinations`.

## Features
- **Sorting:** Users can sort the cards by Cost (ascending/descending).
- **Dynamic Venmo Links:** The site automatically constructs a Venmo payment URL for each destination using the base handle `@Kathryn-Lambright-1`.
- **Trip Links:** If an external URL is provided for a trip, a "View Trip Details ↗" link appears.
- **"Funded" State:** If a trip has been paid for, providing a "Thank You Note" will automatically trigger the Funded state (shows a badge, displays the note, and disables the Venmo button).

## How to Modify in the Future

### 1. Adding or Editing Trips
Open `personal-project.html` and scroll down to the `<script>` tag (around line 200). You will see the `destinations` array. To add a new trip, just add a new object to the list:

```javascript
{
  location: "New Location Name",
  type: "Activity", // Optional categorizing
  cost: 150,
  link: "https://link-to-trip.com", // Optional: leave as "" if none
  notes: "Description of the trip here.",
  thankYouNote: "", // Keep empty if not funded yet
  image: "https://picsum.photos/seed/anyword/800/600" // Image URL
}
```

### 2. Marking a Trip as "Funded"
When someone pays for a trip, you do **not** need to change the HTML/CSS structure. Simply add their thank you note text to the `thankYouNote` property in the array. 

**Before:**
`thankYouNote: "",`

**After:**
`thankYouNote: "Thank you John for the coffee! ☕",`

The JavaScript will automatically read this and render the green "🎉 Funded!" badge, display the note, and disable the Venmo button.

### 3. Updating the Venmo Handle
If the Venmo handle changes, locate the following line just below the `destinations` array:
`const venmoHandle = "Kathryn-Lambright-1";`
Update that string, and all buttons will automatically use the new handle.
