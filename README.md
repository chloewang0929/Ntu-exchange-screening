# Ntu-exchange-screening
# Create project directory
mkdir ntu-exchange-screening
cd ntu-exchange-screening

# Initialize git
git init

# Create a new Vite project
npm create vite@latest . -- --template react

# Install dependencies
npm install

# Install additional required packages
npm install @radix-ui/react-icons lucide-react class-variance-authority clsx tailwindcss postcss autoprefixer tailwindcss-animate @radix-ui/react-label @radix-ui/react-checkbox @radix-ui/react-select
# NTU Exchange Student Screening Platform

## Project Structure
```
ntu-exchange-screening/
├── README.md
├── package.json
├── .gitignore
├── public/
│   ├── index.html
│   └── favicon.ico
└── src/
    ├── components/
    │   └── ExchangeScreening.jsx
    ├── data/
    │   └── universities.js
    ├── styles/
    │   └── globals.css
    ├── App.jsx
    └── index.js
```

## Setup Instructions

1. Create a new repository on GitHub:
   - Go to github.com
   - Click "New repository"
   - Name it "ntu-exchange-screening"
   - Add a description
   - Initialize with README
   - Create repository

2. Clone the repository locally:
```bash
git clone https://github.com/YOUR_USERNAME/ntu-exchange-screening.git
cd ntu-exchange-screening
```

3. Initialize a new React project with Vite:
```bash
npm create vite@latest . -- --template react
```

4. Install dependencies:
```bash
npm install
npm install @radix-ui/react-icons
npm install lucide-react
npm install class-variance-authority
npm install clsx
npm install tailwindcss postcss autoprefixer
npm install tailwindcss-animate
npm install @radix-ui/react-label
npm install @radix-ui/react-checkbox
npm install @radix-ui/react-select
```

5. Initialize Tailwind CSS:
```bash
npx tailwindcss init -p
```

6. Start the development server:
```bash
npm run dev
```

7. Build for production:
```bash
npm run build
```

8. Deploy to GitHub Pages:
- Add "homepage" to package.json:
```json
{
  "homepage": "https://YOUR_USERNAME.github.io/ntu-exchange-screening"
}
```
- Install gh-pages:
```bash
npm install --save-dev gh-pages
```
- Add deploy scripts to package.json:
```json
{
  "scripts": {
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  }
}
```
- Deploy:
```bash
npm run deploy
```

## Environment Setup
- Node.js v16 or higher
- npm v7 or higher
