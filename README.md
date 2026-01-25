# Backend Study Group Website

A minimal, modern, and high-performance Hugo website built for a technical study group. This project features a custom design, auto-alternating carousel, project showcase, and dynamic theme switching.

## ✨ Features

- **Hugo Powered**: Built with Hugo for speed and ease of content management.
- **Custom Design System**: A "Warmer" Light Mode and a deep charcoal Dark Mode.
- **Modern Landing Page**:
  - **Full-Page Hero**: Dynamic animations with isometric backend-themed illustrations.
  - **Auto-Alternating Carousel**: Interactive "Mission" and "What We Study" sections with grid-based individual slide heights.
  - **Project Showcase**: Premium card layout with GitHub and Web demo icons.
- **Global Aesthetics**: A subtle "checkbox" grid background pattern across the entire site.
- **SEO Optimized**: Built-in Open Graph tags, Twitter Cards, and canonical linking.
- **Responsive**: Fully optimized for mobile and desktop viewing.

## 🚀 Getting Started

### Prerequisites

- [Hugo](https://gohugo.io/installation/) (Extended version recommended)

### Local Development

1.  Clone the repository.
2.  Run the Hugo development server:
    ```bash
    hugo server
    ```
3.  Open `http://localhost:1313` in your browser.

## 📂 Project Structure

- `assets/css/style.css`: The core design system and theme variables.
- `content/`: Markdown files for all pages (Home, Projects, Events).
- `layouts/`: Custom HTML templates and partials.
- `static/images/`: Optimized illustrations for the hero section.

## 📝 Adding Content

### Adding a New Project
Create a new file in `content/projects/your-project.md`:
```markdown
---
title: "Project Name"
date: 2026-01-25
description: "Brief summary of the project."
github: "https://github.com/your-username/repo"
demo: "https://your-demo.com"
---
Your deep dive content here...
```

### Adding a New Event
Create a new file in `content/events/your-event.md`:
```markdown
---
title: "Event Title"
date: 2026-02-15T18:00:00Z
description: "What the session is about."
---
Event details...
```

## 🛠 Built With

- **Hugo** - Static Site Generator
- **Vanilla CSS** - Custom Stylesheet
- **Vanilla JS** - Carousel Logic & Theme Toggle
