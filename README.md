# Fall 2021: Object-Oriented Software Engineeing
Group: mOose

<!-- TABLE OF CONTENTS -->
## Table of Contents
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

MOOSE Scheduling app is the ultimate time management application that allows students to manage all their tasks, as well as long-term and short-term goals. Students are able to assign priority to tasks that need to be completed. With the app's feedback system, they can reflect on whether they meet that their daily goals. Time-consuming tasks will automatically be divided in chunks on the students’ calendars, allowing them to more effectively tackle larger tasks. The goal of our app is simple; Impact students by promoting productivity, discourage procrastination, and supporting students to meet their goals.


<p align="right">(<a href="#top">back to top</a>)</p>



### Built With

* [Node.js](https://nodejs.org/)
* [React.js](https://reactjs.org/)
* [MongoDB](https://www.mongodb.com/)
* [Mongoose](https://mongoosejs.com/)
* [Express](https://expressjs.com/)
<p align="right">(<a href="#top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

This is an example of how you may give instructions on setting up your project locally.
To get a local copy up and running follow these simple example steps.

### Prerequisites
* homebrew
  https://brew.sh/

* npm
  ```sh
  npm install npm@latest -g
  ```

### Installation

NOTE: If you're using IntelliJ IDEA, please install the ".env files support" plugin

1. Clone the repo
   ```sh
   git clone https://github.com/jhu-oose/2021-fall-group-moose.git
   ```
2. Install NPM packages
   ```sh
   npm install
   npm install --save styled-components
   npm i --save react-big-calendar
   ```
3. Run the server in the currect directory (You should have already ran npm install)
   ```js
   npm start
   ```
   
   If you get the following error: 
   ```
   const utf8Encoder = new TextEncoder();
                    ^
   ReferenceError: TextEncoder is not defined
   ```
   
   Please refer to [this](https://stackoverflow.com/a/69287561) StackOverflow solution to resolve your issue.

4. Open a new terminal and run the client in the client directory
   ```js
   cd client
   npm install
   npm start
   ```
   
   (Yes, you need to do "npm install" both for the client server as well!)
   
### Going Beyond CRUD
In order to go beyond CRUD, we created an algorithm that automatically gives users recommendations for future planning based on past task accomplishment. Since we are still developping the app, the following explains the formula as well as how instructors can verify our work:
    
    prodScore = [Sum of (actual time spent today) / Sum of (expected time spent today)]. 
    
    Note: The end of "today" will eventually be defined by the user, but for now, it is set at midnight by default.
    
    Based on the productivity score, the terminal will print out various messages:
    
    (a) < .75 – gets the recommendation "Wow! You're hyper-productive. Feel free to do more things, or just enjoy your day!"
    
    (b) .75 to 1 – gets the recommendation "Yay! You're pretty spot on with your time estimates. Keep it up!"
    
    (c) > 1 and < 1.5 – gets the recommendation "Hmm, do you want to add some buffer time in your day, and plan spend more time on your tasks?"
    
    (d) 1.5+ – gets the recommendation "Oof. Do you need a day off on [day of the week]s? Are you taking a day off at least once a week? Also, do you want to add some buffer time in your day, and plan spend more time on your tasks?"
  

    
Scheduling Algorithm:
We implemented a rudimentary scheduling algorithm that:
 
    (a) Help the users start the task at least 2 days before the deadline.
    
    (b) Determine every task's weight by the task priority and the predicted time that will be spent on the task. 
    
    (c) Choose the first meeting time for each task that matches up with task duration, with tasks ordered by weight. 

The output of the algorithm using dummy data is displayed in the console.

For future iterations, we intend to reflect recommendations and productivity scores in our front end, but we did not for this iteration since we were instructed to mostly work on the back end. 

Upcoming projected steps to the next part of our algorithm, for future iterations:
    
    (d) Calculate hidden productivity score for buckets of time (12-3, 3-6, etc)
    
    (e) Initialize each time bucket with same score
    
    (f) Determine optimal times as empty buckets with the highest productivity scores
    
    (g) Every time a task is completed, update the old productivity score of bucket by multiplying with task score = (expected / actual time) * learning rate (any number < 1 to minimize variance, depends on how often we think app will be used / how much we think each task should weigh into overall score)
    
    (h) If the task overlaps with another bucket, weight the score contributions differently (e.g. task is completed from 2-5, 1/3 of task score is given to 12-3, 2/3 given to 3-6 — (# of hrs spent in bucket / total hrs spent) * task score * old bucket score = new bucket score)
    
This second projected part of our algorithm is basically a rudimentary gradient descent algorithm for optimization/ML problems. The cost function is the error between expected time & actual time spent on a task, and the goal is to maximize the user’s productive hours by minimizing this function. Ideally, the algorithm improves overtime as there is more data to work with, learning the user’s habits.

Another projected idea to extend our algorithm is something we call the "Low Priority Procrastination Bias" (LPPB) extension, in which a user may purposely rank a task as lower priority as a way to procrastinate it. In order to address LPPB, the algorithm may take the following steps: 
    
    (i) If a task is within x days and it has < 3 stars, (ask user to) move it to 3 stars.
    
    (j) Randomly choose 1+ task(s) with < 3 stars to be recommended as if it were a task with 3 stars.

Please note that 3 stars is the highest priority, and the value of "x" is still to be determined.

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- ONLINE DEPLOYMENT -->
## Usage

You may use our app online with the following link: https://schedule-productively.herokuapp.com/

NOTE: Some users have reported that logging in may take a long time to load. Please allow up to 30 seconds for app to load while trying to log in if it does not load immediately.

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

The following **required** functionality is completed:

- [x] User can click a create task button
- [x] The user can view a right fly out window, where they can add details fo their task such as due date, priority, and task name.
- [x] User can view a calendar in the application's homepage.

The following system requirements are completed:

- [x] Set up our database - MongoDb
- [x] Design layout of our app's homepage using styled components and flexbox
- [x] For iteration 3, most of the work was done for our backend, including sending data to the database, and querying the database (also see Going Beyond CRUD).


See the [open issues](https://github.com/jhu-oose/2021-fall-group-moose/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- LICENSE -->
## License

For JHU OOSE.

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- CONTACT -->
## Contact
Keidai Lee - elee175@jhu.edu
Shaina Gabala - sgabala2@jhu.edu
Ayo Ajayi - aajayi8@jhmi.edu
Weina Dai  - wdai11@jhu.edu
Nolan Lombardo - nlombar2@jhu.edu
Michiko Takahashi - mtakaha4@jhu.edu



<p align="right">(<a href="#top">back to top</a>)</p>
