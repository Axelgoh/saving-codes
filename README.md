script 
import React from 'react';

const CreateNewPost = ({ innovationTitle, innovationDescription }) => {
  // The CreateNewPost component can be a separate reusable component
  // that takes the innovationTitle and innovationDescription as props,
  // and renders the content accordingly.

  return (
    <div className="subforum-description subforum-column">
      <h4>
        <a href="#">{innovationTitle}</a>
      </h4>
      <p>{innovationDescription}</p>
    </div>
  );
};

export default CreateNewPost;

  Home 
  import React, { useState } from 'react';
import Sidebar from '../components/Sidebar';
import Navbar from '../components/Navbar';
import CreateNewPost from '../components/scripting/CreateNewPost';

const Home = () => {
  const [posts, setPosts] = useState([]);

  const addNewPost = (title, description) => {
    const newPost = { title, description };
    setPosts(prevPosts => [...prevPosts, newPost]);
  };

  return (
    <div>
      <Navbar />
      <body>
        {/* Rest of the code */}
        <div className="container testing" id="testest">
          {/* Iterate over the posts array and render CreateNewPost components */}
          {posts.map((post, index) => (
            <CreateNewPost
              key={index}
              innovationTitle={post.title}
              innovationDescription={post.description}
            />
          ))}
        </div>
        {/* Rest of the code */}
      </body>
    </div>
  );
};

export default Home;


create page 
import React, { useState } from 'react';
import '../css/styles.css';
import Sidebar from '../components/Sidebar';
import Navbar from '../components/Navbar';
import CategorySelect from "../components/CategorySelect-Dropdown.js";
import { Box, InputLabel, MenuItem, FormControl, Select, Popover, Button, Slider } from '@mui/material';

const CreatePage = ({ addNewPost }) => {
  const [innovationTitle, setInnovationTitle] = useState('');
  const [innovationDescription, setInnovationDescription] = useState('');

  const handleSubmit = event => {
    event.preventDefault();
    addNewPost(innovationTitle, innovationDescription);

    // Clear the form inputs after submission
    setInnovationTitle('');
    setInnovationDescription('');
  };
  return (
    <div>
      <Navbar />
      <body className="back">
        <div>
          <Sidebar />
        </div>
         <div className="container" id="forum">
          <form onSubmit={handleSubmit}>
            <h1>Submit Innovation</h1>
            <p>Do you have a great idea or innovation that could make your workplace more productive, efficient, or enjoyable? We invite you to share your brilliance and ingenuity with us! Submit your idea today and be part of the positive change in your workplace.</p>
            <hr />
            <div>
              <p>What department are you from?:</p>
              <div className="categoryselect">
                <CategorySelect name="CategorySelect" />
              </div>
            </div>
            <div>
              <p>Innovation Title:</p>
              <textarea
                name="postInnovationTitle"
                id="innovation-title"
                placeholder="Eg: Team Bonding Tuesday"
                rows={2} cols={100}
                value={innovationTitle}
                onChange={(e) => setInnovationTitle(e.target.value)}
              />
            </div>
            <div>
              <p>Innovation Description:</p>
              <textarea
                name="postInnovationDescription"
                id="innovation-description"
                placeholder="Eg: Incorporate team building by having..."
                rows={10} cols={100}
                value={innovationDescription}
                onChange={(e) => setInnovationDescription(e.target.value)}
              />
            </div>
            <div id="testing" className="btn-block">
              <button className="submitBtn" type="submit">Submit</button>
            </div>
          </form>
        </div>
      </body>
    </div>
  );
};

export default CreatePage;

App 
import React from 'react';
import { BrowserRouter as Router, Switch, Route } from 'react-router-dom';
import Home from './Home';
import CreatePage from './CreatePage';

const App = () => {
   const [posts, setPosts] = useState([]);

  const addNewPost = (title, description) => {
    const newPost = { title, description };
    setPosts(prevPosts => [...prevPosts, newPost]);
  };

  return (
    <Router>
      <Switch>
        <Route exact path="/" component={Home} />
        <Route path="/createpage">
          <CreatePage addNewPost={addNewPost} />
        </Route>
      </Switch>
    </Router>
  );
};

export default App;

    
# saving-codes
