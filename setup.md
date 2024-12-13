### Step-by-Step Guide to Set Up a MERN + Tailwind CSS Project

#### 1. **Prerequisites**
Ensure you have the following installed:
- **Node.js** (v16 or higher)
- **MongoDB**
- **npm** or **yarn**
- A code editor (e.g., VS Code)

---

### Project Setup

#### Step 1: **Initialize the Project**
1. Create a folder for the project:
   ```bash
   mkdir mern-tailwind
   cd mern-tailwind
   ```
2. Initialize a new Node.js project:
   ```bash
   npm init -y
   ```

---

#### Step 2: **Set Up the Server (Backend)**

1. Create a folder for the server:
   ```bash
   mkdir server
   cd server
   ```
2. Initialize a `package.json` for the server:
   ```bash
   npm init -y
   ```
3. Install backend dependencies:
   ```bash
   npm install express mongoose dotenv cors body-parser
   npm install --save-dev nodemon
   ```
4. Create the folder structure inside the `server` folder:
   ```
   server/
   ├── models/
   ├── routes/
   ├── controllers/
   ├── config/
   ├── .env
   ├── server.js
   └── package.json
   ```

5. Set up the **server.js** file:
   ```javascript
   const express = require('express');
   const mongoose = require('mongoose');
   const cors = require('cors');
   const dotenv = require('dotenv');

   dotenv.config();

   const app = express();

   app.use(cors());
   app.use(express.json());

   mongoose.connect(process.env.MONGO_URI, {
       useNewUrlParser: true,
       useUnifiedTopology: true,
   }).then(() => console.log('MongoDB Connected'))
     .catch(err => console.error(err));

   app.get('/', (req, res) => {
       res.send('Server is running...');
   });

   const PORT = process.env.PORT || 5000;
   app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
   ```

6. Add a start script in `server/package.json`:
   ```json
   "scripts": {
       "start": "node server.js",
       "dev": "nodemon server.js"
   }
   ```

7. Run the server:
   ```bash
   npm run dev
   ```

---

#### Step 3: **Set Up the Client (Frontend)**

1. Go back to the root directory and create a client folder:
   ```bash
   cd ..
   mkdir client
   cd client
   ```
2. Initialize React:
   ```bash
   npm install web-vitals
   npx create-react-app .
   ```
3. Install Tailwind CSS:
   ```bash
   npm install -D tailwindcss postcss autoprefixer
   npx tailwindcss init
   ```

4. Configure Tailwind in **`tailwind.config.js`**:
   ```javascript
   module.exports = {
       content: [
           "./src/**/*.{js,jsx,ts,tsx}",
       ],
       theme: {
           extend: {},
       },
       plugins: [],
   }
   ```

5. Add Tailwind directives to **`src/index.css`**:
   ```css
   @tailwind base;
   @tailwind components;
   @tailwind utilities;
   ```

6. Modify folder structure for React:
   ```
   client/
   ├── src/
   │   ├── components/
   │   ├── pages/
   │   ├── App.css
   │   ├── App.js
   │   ├── index.css
   │   ├── index.js
   └── package.json
   ```

---

#### Step 4: **Connect Backend and Frontend**

1. Install Axios in the client:
   ```bash
   npm install axios
   ```
2. Set up a proxy in the client’s `package.json`:
   ```json
   "proxy": "http://localhost:5000"
   ```
3. Example API call in a React component (e.g., `App.js`):
   ```javascript
   import React, { useEffect } from 'react';
   import axios from 'axios';

   const App = () => {
       useEffect(() => {
           axios.get('/')
               .then(response => console.log(response.data))
               .catch(err => console.error(err));
       }, []);

       return (
           <div className="text-center">
               <h1 className="text-3xl font-bold text-blue-500">
                   MERN + Tailwind Setup Complete!
               </h1>
           </div>
       );
   };

   export default App;
   ```

---

#### Step 5: **Run the Project**

1. Run the backend server:
   ```bash
   cd server
   npm run dev
   ```
2. Run the frontend client:
   ```bash
   cd ../client
   npm start
   ```

---

### Final Folder Structure
```
mern-tailwind/
├── client/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── App.js
│   │   ├── index.js
│   │   └── index.css
│   ├── tailwind.config.js
│   └── package.json
├── server/
│   ├── config/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── server.js
│   ├── .env
│   └── package.json
└── package.json
```

This setup creates a fully functional MERN + Tailwind project!
