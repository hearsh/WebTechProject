# hackadayApi

## Introduction
This project provides a view for [hackaday.io](https://hackaday.io) projects and their users. The projects makes use of server side rendering without using ReactJs. Implemented caching inorder to navigate through pages faster.

Provides 10 projects per page, has a read more on each projects if anyone wants to know more about the project. 

All data is fetched from the [hackaday API](https://dev.hackaday.io/doc/api). The project itself only maintains local cache and no database as of now.

It also provides the user with recommendations about projects and users, Recommendations are unique to each browsing session. Recommendations are based tags for users and projects, shows projects similar to projects where users clicks on read more.

Used a singleton architecture for the project.

Created my own component system to facilitate server side rendering. All operations happen on the server, only dynamic content is generated on the front end.

## Objective

The primary objective as a unit was to create an intuitive web app where the users could have a look at the project information by either hovering to the selected project or by opening a new project page. We also built a recommender system which would offer unique recommendations to the users and guide them in the process of their selection. We have challenged ourselves as a team and we strived to make something substantial and hence we went ahead with our objective of creating an intuitive API. The objectives can be broken down into:

- Project List page: 
    - Rendering a page that shows a list of projects 
    - The page is rendered on the server side and displays each projects metadata and owner 
    - Show a tooltip presenting the owners metadata when hovering over a project owners name 
    - The tooltip should be loaded dynamically and only once per browsing session 

- Implement Pagination: 
    - Pages should not load when going to the next/previous pages 
    - The browser will display an unique URL when going to next/previous pages 
    - The URL should load the same page of projects as if the visitor navigated using the next/previous links 
    - Asynchronous caching for redirecting to next or previous page  

- Project detail page: 
    - Server-side renders a page that would show projects metadata on clicking the project 
    - Show recommended projects and recommended users by comparing the selected project tags with other tags and users 
  

## Requirements
* [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/en/)
* [NodeJs](https://nodejs.org/en/)

## How to Run the Application?
* Clone or download the project
* Enter the project directory
* Open your cmd
* Type `yarn` or `npm install`
* Go to the `index_help.js` file under `components/Credentials`
* Enter your unique api key from [hackaday.io](https://hackaday.io)
* Change the file from `index_help.js` to `index.js`
* Type `yarn start` or `npm start`
* Go to `localhost:3000`
* Enjoy browsing and hack away.

## Team members contribution:

Teamwork is more of  “WE” and less of  “ME”.  We believe that we worked well as a team and thought of adding our contributions at the very end as everyone tried helping and fixing the bugs that were encountered during the development phase. 

**Backend:**

Hearsh: Data Access (Min-Heap, Recommender), Layouts

Ishan: Data Access (User Data, Project Data), Layouts

**Front end:**

Sohini: App.js and SASS

Karan: App.js along with layout and positioning of elements

## Detailed Description On The Project

### Components

#### Credentials
Stores the api key for hackaday.io

#### DataAccess
Has helper functions to maintain the data of the project. Each of these functions have their own state of data which they maintain

##### MinHeap
It is used to maintain a min heap to store the top three project tags and user tags. The tags have a score attached to them which is calculted using probability.

##### ProjectData
It has helper functions to get project data. Used to get a page of projects and also single projects.

##### Recommender
It containts helper funtions to maintain recommendation data. It scores each tag based on the number of times the user has visited similar projects or users having that tag.

##### UserData
Similar to project data but has helper functions for users and not projects.

#### Layouts
It has several helper functions to generate the layout. Takes care of the entire layout. has modular functions to create the html template, head section, body section etc. Each function is a pure function here. Is serves as the base for server side rendering. It also has attributes which are simple functions to return the various html tags like the anchor tag `<a>`, pararaph tag `<p>`, header tag `<h1>` etc.

#### Sass
Contains all the styling for the project.

### Public
Contains the javascript files for dynamic content loading. Loads the user data dn tooltips dynamically after the page loads. It also changes the pages dynamically using hash routes. Generates recommendations dynamically to.

### Routes

#### Index
Manages all the data for `/`, `/projects/:id`, `/getRecommendation`, `/getPage`. Deals with mostly project data. It creates the html for the page on the server and sends a `text/html` response back to the client. Puts all the componenets together.

#### Users
Manages the user data for `/users`. Fetches the user data and sends it back as a `json` response back to the client.

## Challenges

**1. Server Side Rendering** - Complexity of SSR grows with complexity of application. 

**2. Quick Data access** 

**3. Improve page performance** 

**4. API Restrictions**- We scanned through a lot of API’s where we could have the tags to find the users however due to the restrictions we were not in a position to implement that 
  
## Future work:

**GitLogin** - We deemed the O authorization as surplus as it imposed limitations on the recommender system. Building a recommender system was much easier when we had the user data. We wanted to create a recommender system that went beyond the data and analyzed user behavior each time in enters the system. This could be easily understood with Google which provides recommendation based on the users browsing history and Duckduckgo which provides recommendations without the history. We could definitely work on getting Gitlogin and adding additional layer of security after we have a concrete recommender system

MongoDB: We would be also working on transferring the API data from Hackaday to a Mongodb data instance. 


## Conclusion

Technologies learnt:

- **Node JS** - To easily build fast and scalable network applications. 
- **MongoDB** - Database that works fast and integrates well with Node JS 
- **Vanilla JS** - Most lightweight framework available anywhere 
- **SASS** - Powerful professional grade CSS extension language 
- **Express with EJS** (Embedded javascript)
- **Git**
