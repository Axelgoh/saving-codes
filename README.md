Feedbacks Web Application
A simple web application for submitting and displaying user feedbacks.

Table of Contents
Introduction
Features
Getting Started
Prerequisites
Installation
Running the Application
Usage
Submitting Feedback
Displaying Feedback
Liking Feedback
Screenshots
Contributing
License
Introduction
This web application provides a user-friendly interface for submitting, viewing, and interacting with user feedback entries. It's built using React.js framework and communicates with a corresponding REST API for managing feedback entries.

Features
Submit new feedback entries.
Display a list of user feedbacks.
Like user feedbacks to show appreciation.
Easy navigation between submission and display pages.
Getting Started
Prerequisites
To run this application locally, you need to have the following installed:

Node.js
npm (Node Package Manager)
Installation
Clone the repository:

sh
Copy code
git clone https://github.com/your-username/feedbacks-web-app.git
cd feedbacks-web-app
Install dependencies:

sh
Copy code
npm install
Running the Application
Start the development server:

sh
Copy code
npm start
The application will be accessible at http://localhost:3000.

Usage
Submitting Feedback
Launch the application in your web browser.
Go to the "Home" page.
Fill in the feedback title and description.
Click the "Submit" button.
Displaying Feedback
Go to the "Display" page.
View the list of submitted feedbacks.
Liking Feedback
On the "Display" page, each feedback entry has a "Like" button.
Click the "Like" button to show appreciation for a feedback.
Screenshots
Include screenshots of your application in action, showcasing its features.

Contributing
Contributions are welcome! Please see the CONTRIBUTING.md file for guidelines.

License
This project is licensed under the MIT License.


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
  import * as React from 'react';
import { Component } from "react";
import Sidebar from '../components/Sidebar.js';
import Navbar from '../components/Navbar.js';
import BasicPopover from "../components/BasicPopover.js";
import CategorySelect from "../components/CategorySelect-Dropdown.js";
import CreateNewPost from '../components/scripting/CreateNewPost';
import { FaSearch } from 'react-icons/fa';
import { Link } from "react-router-dom";
import { Box, InputLabel,MenuItem, FormControl, Select, Popover, Button, Slider} from'@mui/material';
import DiamondTwoToneIcon from '@mui/icons-material/DiamondTwoTone';
import ControlPointRoundedIcon from '@mui/icons-material/ControlPointRounded';
import {useState,useEffect} from 'react';



const Home = () => {
  const [posts, setPosts] = useState([]);

  const addNewPost = (title, description) => {
    const newPost = { title, description };
    setPosts(prevPosts => [...prevPosts, newPost]);
  };
        return(
        <div>
        <Navbar/>
            <body>
              <div className="search-box">
                <CategorySelect/>
                <div>
                  <input type="text" name="fsearch" placeholder="search ..." />
                  <button>
                    <i className="fa fa-search" />
                    <FaSearch/>
                  </button>
                </div>
              </div>

              <div>
                <Sidebar />
              </div>

              <div className="container testing your-department"> //your department innovation
                <div className="subforum">
                  <div className="subforum-title">
                    <h1>Your Department Innovations</h1>
                  </div>

                  <div className="subforum-row">
                    <div className="subforum-icon subforum-column center">
                      <i className="fa fa-car center" />
                      <BasicPopover/>
                    </div>
                    <div className="subforum-description subforum-column">
                      <h4>
                        <a href="#">Description Title</a>
                      </h4>
                      <p>Description Content:This will be populated by AIA staff for their Innovations. </p>
                    </div>
                    <div className="subforum-stats subforum-column center">
                      <span id="likes">12 Likes</span>
                    </div>
                    <div className="subforum-info subforum-column">
                      <b>
                        <a href>Last post</a>
                      </b> by <a href>Axel Goh</a>
                      <br />on <small>12 Dec 2020</small>
                    </div>
                  </div>

                  <hr className="subforum-devider" />
                  <div className="subforum-row">
                    <div className="subforum-icon subforum-column center">
                      <i className="fa fa-car center" />
                      <BasicPopover/>
                    </div>
                    <div className="subforum-description subforum-column">
                      <h4>
                        <a href="#">Description Title</a>
                      </h4>
                      <p>Description Content:This will be populated by AIA staff for their Innovations. </p>
                    </div>
                    <div className="subforum-stats subforum-column center">
                      <span>12 Likes | 2 comments</span>
                    </div>
                    <div className="subforum-info subforum-column">
                      <b>
                        <a href>Last post</a>
                      </b> by <a href>Axel Goh</a>
                      <br />on <small>12 Dec 2020</small>
                    </div>
                  </div>
                </div>
              </div>

              <div className="container testing" id="testest"> // general innovations
                <div className="subforum">
                  <div className="subforum-title">
                    <h1>View Some Innovationss</h1>

                  </div>
                            {/* Iterate over the posts array and render CreateNewPost components */}
                            {posts.map((post, index) => (
                              <CreateNewPost
                                key={index}
                                innovationTitle={post.title}
                                innovationDescription={post.description}
                              />
                            ))}
                </div>
              </div>
              <Link to="/createpage">
                  <ControlPointRoundedIcon className="createicon" fontSize="large"/>
              </Link>
            </body>
         </div>
           )
           }
export default Home;












create page 
import * as React from 'react';
import '../css/styles.css';
import Sidebar from '../components/Sidebar';
import Navbar from '../components/Navbar';
import CategorySelect from "../components/CategorySelect-Dropdown.js";
import * as Home from './Home';
import {subforum} from './Home';
import CreateNewPost from '../components/scripting/CreateNewPost';
import {useState, useEffect} from 'react';
import { Box, InputLabel,MenuItem, FormControl, Select, Popover, Button, Slider} from'@mui/material';



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
import logo from './logo.svg';
import React from 'react';
import Navbar from "./components/Navbar";
import Home from './pages/Home';
import './css/bootstrap/dist/css/bootstrap-grid.min.css'
import Message from './components/Message';
import CreatePage from './pages/CreatePage';
import CreateNewPost from './components/scripting/CreateNewPost';
import { BrowserRouter as Router, Routes, Route } from 'react-router-dom';
import {useState,useEffect} from 'react';



const App = () => {
   const [posts, setPosts] = useState([]);

   const addNewPost = (title, description) => {
     const newPost = { title, description };
     setPosts(prevPosts => [...prevPosts, newPost]);
  };

  return (
    <Router>
      <Routes>
        <Route path="/createpage">
           <CreatePage addNewPost={addNewPost} />
         </Route>
        <Route exact path="/">
          <Home posts={posts} />
        </Route>
      </Routes>
    </Router>
  );
};

export default App;



index  
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from 'react-router-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';
import "./css/styles.css";

ReactDOM.render(
  <React.StrictMode>
    <BrowserRouter>
        <App />
    </BrowserRouter>
  </React.StrictMode>,
  document.getElementById('root')
);

reportWebVitals();

    
# saving-codes


import React, { useEffect, useState } from 'react';
import { BrowserRouter as Router, Route, Routes } from 'react-router-dom';
import Home from './Home';
import Display from './display';

function App() {
  const [feedbacks, setFeedbacks] = useState(() => {
    // Initialize state from localStorage or an empty array
    const storedFeedbacks = localStorage.getItem('feedbacks');
    return storedFeedbacks ? JSON.parse(storedFeedbacks) : [];
  });

  useEffect(() => {
    // Save feedbacks to localStorage whenever they change
    localStorage.setItem('feedbacks', JSON.stringify(feedbacks));
  }, [feedbacks]);

  const addFeedback = (feedback) => {
    setFeedbacks([...feedbacks, feedback]);
  };

