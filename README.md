# Players_vue-app: A Dynamic Player Dashboard with Vue.js

This project offers an interactive player dashboard built with Vue.js, allowing users to explore and filter player data effortlessly.

![Screenshot (201)](https://github.com/user-attachments/assets/b38782a1-ba6d-49d8-80ca-7372925b07c6)

![Screenshot (202)](https://github.com/user-attachments/assets/91325ea9-c098-4d99-9fde-c99ef1d33e60)

![Screenshot (203)](https://github.com/user-attachments/assets/8a84b38c-03c0-4f50-b2cd-9d008a339150)


## Features

* **Comprehensive Player Information:** View details like name, team, matches played, runs scored, fifties/hundreds, highest score, and bowling figures (if available).
* **Team Filtering:** Utilize the dropdown menu to filter players by their respective teams.
* **Search Functionality:** Search for specific players using their name or team name with the provided search bar.
* **Role-Based Grouping:** Players are automatically categorized based on their roles (batsman, all-rounder, bowler) for better organization.

## Getting Started

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/om6363-crypto/Players_Vue-app.git
   ```

2. **Install Dependencies:**
   ```bash
   cd Players_vue-app
   npm install
   ```

3. **Run the Application:**
   ```bash
   npm run serve
   ```

   This will launch a development server and open the Player Dashboard in your browser at http://localhost:8080/

## Technologies Used

* **Vue.js:** The core framework for building the interactive player dashboard.
* **Bootstrap:** Provides pre-built UI components for a visually appealing and responsive design.
* **JSON Data:** Player information is currently loaded from a local JSON file (`players.json`). You can integrate your own data source if desired.

## Data Source

The application retrieves player data from a local JSON file (`players.json`). Feel free to modify this file with your own data source for customization.

## Project Structure

```
Players_vue-app/
│
├── src/
│   ├── components/
│   │   └── PlayerDashboard.vue
│   │
│   ├── players.json
│   └── main.js
│
├── public/
│   └── index.html
│
├── package.json
└── README.md
```

## Contributing

We welcome contributions to this project! If you have any improvements, bug fixes, or feature additions, please fork the repository and submit pull requests.

## Author
https://github.com/om6363-crypto
