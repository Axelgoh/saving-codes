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

  Home import * as React from 'react';
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
import {subforum} from './Home';
import CreateNewPost from '../components/scripting/CreateNewPost';
import {useState, useEffect} from 'react';
import { Box, InputLabel,MenuItem, FormControl, Select, Popover, Button, Slider} from'@mui/material';



const CreatePage = ({addNewPost}) => {
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
        <Route exact path="/">
          <Home posts={posts} />
        </Route>
        <Route path="/createpage">
           <CreatePage addNewPost={addNewPost} />
         </Route>
      </Routes>
    </Router>
  );
};

export default App;

    
# saving-codes


TypeError: addNewPost is not a function
handleSubmit
C:/Users/smis038/Desktop/Axel goh projects/aia-feedback-forum-react/src/pages/CreatePage.js:20
  17 | 
  18 |  const handleSubmit = event => {
  19 |    event.preventDefault();
> 20 |    addNewPost(innovationTitle, innovationDescription);
     | ^  21 | 
  22 | 
  23 |    // Clear the form inputs after submission
View compiled
HTMLUnknownElement.callCallback
C:/Users/smis038/Desktop/Axel goh projects/aia-feedback-forum-react/node_modules/react-dom/cjs/react-dom.development.js:3733
  3730 | function callCallback() {
  3731 |   didCall = true;
  3732 |   restoreAfterDispatch();
> 3733 |   func.apply(context, funcArgs);
       | ^  3734 |   didError = false;
  3735 | } // Create a global error event handler. We use this to capture the value
  3736 | // that was thrown. It's possible that this error handler will fire more
View compiled
invokeGuardedCallbackDev
C:/Users/smis038/Desktop/Axel goh projects/aia-feedback-forum-react/node_modules/react-dom/cjs/react-dom.development.js:3777
  3774 | // errors, it will trigger our global error handler.
  3775 | 
  3776 | evt.initEvent(evtType, false, false);
> 3777 | fakeNode.dispatchEvent(evt);
       | ^  3778 | if (windowEventDescriptor) {
  3779 |   Object.defineProperty(window, 'event', windowEventDescriptor);
  3780 | }
View compiled
invokeGuardedCallback
C:/Users/smis038/Desktop/Axel goh projects/aia-feedback-forum-react/node_modules/react-dom/cjs/react-dom.development.js:3834
  3831 | function invokeGuardedCallback(name, func, context, a, b, c, d, e, f) {
  3832 |   hasError = false;
  3833 |   caughtError = null;
> 3834 |   invokeGuardedCallbackImpl$1.apply(reporter, arguments);
       | ^  3835 | }
  3836 | /**
  3837 |  * Same as invokeGuardedCallback, but instead of returning an error, it stores
View compiled
invokeGuardedCallbackAndCatchFirstError
C:/Users/smis038/Desktop/Axel goh projects/aia-feedback-forum-react/node_modules/react-dom/cjs/react-dom.development.js:3848
  3845 |  */
  3846 | 
  3847 | function invokeGuardedCallbackAndCatchFirstError(name, func, context, a, b, c, d, e, f) {
> 3848 |   invokeGuardedCallback.apply(this, arguments);
       | ^  3849 |   if (hasError) {
  3850 |     var error = clearCaughtError();
  3851 |     if (!hasRethrowError) {
View compiled
executeDispatch
C:/Users/smis038/Desktop/Axel goh projects/aia-feedback-forum-react/node_modules/react-dom/cjs/react-dom.development.js:7992
  7989 | function executeDispatch(event, listener, currentTarget) {
  7990 |   var type = event.type || 'unknown-event';
  7991 |   event.currentTarget = currentTarget;
> 7992 |   invokeGuardedCallbackAndCatchFirstError(type, listener, undefined, event);
       | ^  7993 |   event.currentTarget = null;
  7994 | }
  7995 | function processDispatchQueueItemsInOrder(event, dispatchListeners, inCapturePhase) {
View compiled
processDispatchQueueItemsInOrder
C:/Users/smis038/Desktop/Axel goh projects/aia-feedback-forum-react/node_modules/react-dom/cjs/react-dom.development.js:8018
  8015 |     if (_instance !== previousInstance && event.isPropagationStopped()) {
  8016 |       return;
  8017 |     }
> 8018 |     executeDispatch(event, _listener, _currentTarget);
       | ^  8019 |     previousInstance = _instance;
  8020 |   }
  8021 | }
