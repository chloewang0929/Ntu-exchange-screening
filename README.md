# Ntu-Exchange-Screening System
# __Abstract and Motivation__:
The exchange student system webpage of National Taiwan University is not intuitive and organizes information by school, requiring students to visit each school's webpage to find application details such as required language tests and minimum GPA limits.<br>
To address this issue, we aim to create a webpage where students can input their language certificates or test scores, GPA, and desired state or region. The system will then automatically filter and display schools and departments that match the student's qualifications, significantly reducing the time and effort spent researching and verifying application criteria.
# Topic: Screening exchange schools that meet application requirements
__Web crawler__: Crawls the information we need from the webpage of the National Taiwan University International Office List of Exchange Schools at National Taiwan University and organizes it.<br> <br>
__Webpage__: Create a window that allows users to input their language test scores, departments, GPA and other information, and then select the country they want to view. Finally, a organized form will pop up, showing the schools they can apply for and the school's detailed information.

# Web Crawler Algorithm:
Our goal is to have the program click on the "Application Information" page of each school sequentially from the list of applied schools, and then crawl out the information of individual schools.<br>
![My Image](pic1.JPEG)<br>
(pic1: List of exchange student programs at National Taiwan University)
![My Image](pic2.jpeg)<br>
(pic2: Application information pages for each university)<br>
 <br>
Therefore, first crawl out all the web links to the "Application Information" page that you want to enter sequentially from the list, and store them in the list of filtered_links.<br>
```python
# Get the source code of the web page
url = "https://oia.ntu.edu.tw/outgoing/school.list"  # 將URL替換為你的目標網頁
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")

# Find links to all application data requirements
links = soup.find_all('a', href=True, text='申請資料')

# Filter out links to specific websites
filtered_links = [link for link in links if '聖保羅大學' not in link.get('href')]
```
Next, we use __loops__ to crawl data on the pages of different schools. We save all the required data into the list first, so that it can be added to the csv at once.<br>
 <br>
__1. Chinese and English name of the university__<br>
During our testing, we found that there were English commas in the English names, which would affect the formatting of the csv file during output, so we replaced          them with "," and stored the Chinese and English names separately.<br>
__2. Second application__<br>
Similar to the above, the attribute used is 'class': 'uninfo-awall', and it is judged whether there is the keyword "This school is open to students who want to go abroad for exchange for the second time."<br>
__3. Other precautions__<br>
Since other items including "Application Qualifications", "Quota", "School Calendar", "Registration and Payment", "Notes", and "Accommodation Information" are all stored in the same "class":'uninfo-content' title, among which Most do not have a uniform format. Therefore, we first climb down and save it into the double list of uninfo_contents, and then do segmentation and sorting later. Use "、" to replace "," at the same time to avoid csv file jumping.
(The contents of each list in uninfo_contents are in the order described above. For example, the application qualification is item 0)<br>
 <br>
We use another loop to sort out "a bunch of notes" according to different universities, and save the sorted information into a list for final output to a csv file:<br>
```python
for i in range(len(uninfo_contents_list)):
```
__1. Open exchange quota__<br>
Use the fixed text format "X names in one semester" in "Quota" to find the positions of semesters and names respectively. Note that if the exchange is not open, such a format cannot be found, so append "0" directly to avoid the final format jumping.<br>

__2. GPA__<br>
Search for the keyword "GPA" in "Application Qualifications" to find out one or more GPA score requirements to two decimal places.<br>
```python
# GPA
    ct = 0
    score = ""
    while True:
        index = uninfo_contents_list[i][0].find("GPA", ct)
        if index == -1 and ct == 0:
            score = "None"
            break
        if index == -1:
            break
        else:
            score += uninfo_contents_list[i][0][index + 5:index + 9]
            ct = index + 1
    gpa_list.append(score)
```








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

{
  "name": "ntu-exchange-screening",
  "private": true,
  "version": "0.1.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "predeploy": "npm run build",
    "deploy": "gh-pages -d dist"
  },
  "dependencies": {
    "@radix-ui/react-checkbox": "^1.0.0",
    "@radix-ui/react-icons": "^1.3.0",
    "@radix-ui/react-label": "^2.0.0",
    "@radix-ui/react-select": "^1.2.0",
    "class-variance-authority": "^0.7.0",
    "clsx": "^2.0.0",
    "lucide-react": "^0.263.1",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "tailwindcss-animate": "^1.0.7"
  },
  "devDependencies": {
    "@types/react": "^18.2.15",
    "@types/react-dom": "^18.2.7",
    "@vitejs/plugin-react": "^4.0.3",
    "autoprefixer": "^10.4.14",
    "gh-pages": "^6.0.0",
    "postcss": "^8.4.27",
    "tailwindcss": "^3.3.3",
    "vite": "^4.4.5"
  }
}
