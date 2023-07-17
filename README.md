script 
import * as React from 'react';
import CreatePage from '../../pages/CreatePage';
import Home from '../../pages/Home';
import BasicPopover from "../BasicPopover";
import { subforum } from '../../pages/Home';
import {useState, useEffect} from 'react';
import * as ReactDom from 'react-dom';


export default function CreateNewPost() {

  // create a new div element with className
    const newDiv = document.createElement("div");
    newDiv.classList.add("subforum-description", "subforum-column")

    // create a new h4 element
    const newH4 = document.createElement("h4");
    // put this H4 element into the new Div
    newDiv.appendChild(newH4);

    // create a new p to be added into the div as well
    const newP = document.createElement("p");
    newDiv.appendChild(newP)

    // create a new a element
    const newA = document.createElement("a");
    newH4.appendChild(newA); // put this a element into the h4

    // and give it some content
    const title = document.createTextNode(document.getElementById("innovation-title").value);
    // add the text node to the newly created a element which is inside the h4 element
    newA.appendChild(title);

    // give some content for the p
    const description = document.createTextNode(document.getElementById("innovation-description").value);
    newP.appendChild(description);

    // add the newly created element and its content into the DOM
    const element = document.getElementById("testest");
    element.appendChild(newDiv); // add the whole new div with it sub contents into element which is the document specified by the id
  };

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
import * as ReactDom from 'react-dom';






export default function Home() {
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

                  <div className="subforum-row">
                    <div className="subforum-icon subforum-column center">
                      <i className="fa fa-car center" />
                      <BasicPopover/>
                    </div>
                    <div  className="subforum-description subforum-column">
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


                </div>
              </div>
              <Link to="/createpage">
                  <ControlPointRoundedIcon className="createicon" fontSize="large"/>
              </Link>
            </body>
         </div>
           )

           }


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


export default function CreatePage() {
    function handleSubmit(e) {

    // Prevent the browser from reloading the page
    e.preventDefault();

    // Read the form data
    const form = e.target;
    const formData = new FormData(form);

    // You can pass formData as a fetch body directly:
    alert('Successfully Submitted !\n Title: ' + form.postInnovationTitle.value + "\n From: "+ document.getElementById("category-select").value);

    }

    return(
      <div>
        <div id="testtest">
          <Navbar />
        </div>
        <body className="back">
          <div>
            <Sidebar />
          </div>
          <div className="container" id="forum">
            <form method="post" onSubmit={handleSubmit}>
              <h1>Submit Innovation</h1>
              <p>Do you have a great idea or innovation that could make your workplace more productive, efficient, or enjoyable ? We invite you to share your brilliance and ingenuity with us! Submit your idea today and be part of the positive change in your workplace. </p>
              <hr />
              <div>
                <p> What department are you from ?: </p>
                <div className="categoryselect">
                  <CategorySelect name="CategorySelect"/>
                </div>
              </div>
              <div>
                <p> Innovation Title: </p>
                <textarea name="postInnovationTitle" id="innovation-title" placeholder="Eg: Team Bonding Tuesday" rows={2} cols={100} />
              </div>
              <div>
                <p> Innovation Description: </p>
                <textarea name="postInnovationDescription" id="innovation-description" placeholder="Eg: Incorporate team building by having..." rows={10} cols={100} />
              </div>
              <div id="testing" className="btn-block">
                <button  className="submitBtn" type="submit" href="/" onClick={CreateNewPost}>Submit</button>
              </div>
            </form>
          </div>
        </body>
      </div> ); }





    
# saving-codes
