## Creating a full blog app using React JS and Tailwind CSS involves several steps. Here's a comprehensive guide to build this app. We'll cover:

1. Setting up the React app
2. Adding Tailwind CSS
3. Creating the components
4. Loading data from a JSON file
5. Implementing routing to show blog details on click

## 1. Setting up the React app

First, create a new React app using Create React App:

```bash
npx create-react-app blog-app
cd blog-app
```

## 2. Adding Tailwind CSS

Install Tailwind CSS:

```bash
npm install -D tailwindcss
npx tailwindcss init
```

Configure Tailwind by adding the following content to your `tailwind.config.js` file:

```javascript
/** @type {import('tailwindcss').Config} */
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

Add the following lines to your `src/index.css` file:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## 3. Creating the Components

Let's create the main components: `BlogList` and `BlogDetails`.

### BlogList Component

Create a file `src/components/BlogList.js`:

```javascript
import React from 'react';
import { Link } from 'react-router-dom';
import blogsData from '../data/blogs.json';

const BlogList = () => {
  return (
    <div className="container mx-auto p-4">
      <h1 className="text-3xl font-bold mb-4">Blog List</h1>
      <div className="grid gap-4 grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
        {blogsData.map((blog) => (
          <div key={blog.id} className="bg-white p-6 rounded-lg shadow-lg">
            <h2 className="text-2xl font-bold mb-2">{blog.title}</h2>
            <p className="text-gray-700">{blog.excerpt}</p>
            <Link to={`/blog/${blog.id}`} className="text-blue-500 hover:underline mt-2 block">
              Read More
            </Link>
          </div>
        ))}
      </div>
    </div>
  );
};

export default BlogList;
```

### BlogDetails Component

Create a file `src/components/BlogDetails.js`:

```javascript
import React from 'react';
import { useParams } from 'react-router-dom';
import blogsData from '../data/blogs.json';

const BlogDetails = () => {
  const { id } = useParams();
  const blog = blogsData.find(blog => blog.id === parseInt(id));

  if (!blog) {
    return <div>Blog not found</div>;
  }

  return (
    <div className="container mx-auto p-4">
      <h1 className="text-3xl font-bold mb-4">{blog.title}</h1>
      <p className="text-gray-700">{blog.content}</p>
    </div>
  );
};

export default BlogDetails;
```

## 4. Loading Data from a JSON File

Create a `data` folder in `src` and add a `blogs.json` file:

```json
[
  {
    "id": 1,
    "title": "First Blog Post",
    "excerpt": "This is the first blog post excerpt.",
    "content": "This is the detailed content of the first blog post."
  },
  {
    "id": 2,
    "title": "Second Blog Post",
    "excerpt": "This is the second blog post excerpt.",
    "content": "This is the detailed content of the second blog post."
  },
  {
    "id": 3,
    "title": "Third Blog Post",
    "excerpt": "This is the third blog post excerpt.",
    "content": "This is the detailed content of the third blog post."
  }
]
```

## 5. Implementing Routing

Set up React Router to handle navigation between the list and details view. First, install React Router:

```bash
npm install react-router-dom
```

Then, update your `src/App.js`:

```javascript
import React from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import BlogList from './components/BlogList';
import BlogDetails from './components/BlogDetails';

const App = () => {
  return (
    <Router>
      <div className="min-h-screen bg-gray-100">
        <Routes>
          <Route path="/" element={<BlogList />} />
          <Route path="/blog/:id" element={<BlogDetails />} />
        </Routes>
      </div>
    </Router>
  );
};

export default App;
```

## Final Project Structure

Your final project structure should look like this:

```
blog-app/
├── node_modules/
├── public/
├── src/
│   ├── components/
│   │   ├── BlogDetails.js
│   │   └── BlogList.js
│   ├── data/
│   │   └── blogs.json
│   ├── App.js
│   ├── index.css
│   └── index.js
├── .gitignore
├── package.json
├── tailwind.config.js
└── README.md
```

Now you can start your app:

```bash
npm start
```

Your app should be running at `http://localhost:3000` with a list of blogs, and clicking on a blog link will show the details.
