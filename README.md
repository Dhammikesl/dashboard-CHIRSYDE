# Vue Timeline Project

A responsive Vue.js dashboard featuring an interactive timeline component with collapsible functionality and editable notes.

## Features

- **Interactive Timeline**: Collapsible timeline with toggle functionality
- **Responsive Design**: Auto-collapse on mobile devices (≤375px)
- **Editable Notes**: Click to edit notes with real-time updates
- **Modern UI**: Clean, professional interface

## Prerequisites

Before running this project, make sure you have the following installed:

- **Node.js** (version 16.0 or higher)
- **npm** (comes with Node.js) or **yarn**

## Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd vue-timeline-project
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

## Development

### Run the development server

```bash
npm run dev
# or
yarn dev
```

The application will be available at `http://localhost:5173` (or the port shown in your terminal).

### Build for production

```bash
npm run build
# or
yarn build
```

### Preview production build

```bash
npm run preview
# or
yarn preview
```

## Project Structure

```
src/
├── assets/                 # Static assets (images, fonts, etc.)
├── components/             # Reusable Vue components
│   ├── Header.vue         # Header component
│   ├── Notes.vue          # Notes component
│   ├── Sidebar.vue        # Sidebar component
│   ├── SvgIcons.vue       # SVG icons component
│   └── Timeline.vue       # Timeline component
├── styles/                 # Global stylesheets
│   ├── global.scss        # Global styles
│   ├── grid.scss          # Grid system styles
│   └── variables.scss     # SCSS variables and mixins
├── App.vue                # Root Vue component
├── main.js                # Application entry point
├── .gitignore             # Git ignore rules
└── index.html             # Main HTML template             

# Application entry point
```
Structure Overview

📁 Components

Header.vue - Application header with navigation
Notes.vue - Notes display and management
Sidebar.vue - Side navigation panel
SvgIcons.vue - Reusable SVG icon components
Timeline.vue - Timeline visualization component

🎨 Styles

global.scss - Global application styles
grid.scss - CSS Grid and layout utilities
variables.scss - SCSS variables, colors, and mixins

⚙️ Core Files

App.vue - Main application component
main.js - Vue app initialization and configuration
index.html - HTML entry point


## Usage

### Timeline Component

The timeline component features:

- **Toggle functionality**: Click the chevron icon to collapse/expand
- **Auto-collapse**: Automatically collapses on mobile devices
- **Responsive design**: Prevents horizontal overflow on small screens

### Notes Component

The notes component includes:

- **Edit mode**: Click "Edit session" to make notes editable
- **Real-time updates**: Changes are saved automatically
- **Mixed content types**: Text fields and multiple choice options

## SCSS Variables

The project uses SCSS variables for consistent theming. Key variables include:

```scss
$spacing-xs: 4px;
$spacing-sm: 8px;
$spacing-md: 16px;
$spacing-lg: 24px;


$color-primary: #012A25;
$color-primary-light: #2E7D76;
$color-secondary: #F7F5F5;
$color-green-text: #3A5754;
$color-green-light-bg: #E5FBF8;
```

## Browser Support

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Create a Pull Request


### Common Issues

**Port already in use**

```bash
# Kill the process using the port
npx kill-port 3000
# or run on a different port
npm run dev -- --port 3001
```

**Module not found**

```bash
# Clear node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

**Styles not loading**

- Ensure SCSS is properly configured in your build tool
- Check that all SCSS variables are defined

## Support

For questions or issues, please open an issue in the repository or contact me 
- Dhammike Rathnayaka 
- dhammike_rathnayaka@outlook.com
