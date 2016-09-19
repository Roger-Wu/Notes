# Meteor.js Notes

## 學習資源

* [Official Tutorials](https://www.meteor.com/tutorials)
* [Official Guide](https://guide.meteor.com/)
* [Official Documentation](http://docs.meteor.com/#/full/)

## Meteor的優點

* full-stack, isomorphic
* real-time app
* web, android, ios

## 創建app
* create

    ```
    meteor create app-name
    cd app-name
    meteor npm install
    ```

* run

    ```meteor``` or ```meteor run```
    
* 去除不安全的部分

    ```
    meteor remove insecure
    meteor remove autopublish
    ```

* 換成React

    請按照[官方教學 step 2: Defining views with React components](https://www.meteor.com/tutorials/react/components)
    
    及[官方教學 step 3: Storing tasks in a collection](https://www.meteor.com/tutorials/react/collections)做
    
    ```
    meteor npm install --save react react-dom
    meteor npm install --save react-addons-pure-render-mixin
    meteor add react-meteor-data
    ```

## methods (前後共通的function)

* 定義methods

    ```js
    Meteor.methods({
      'tasks.insert'(text) {
        check(text, String);
     
        // Make sure the user is logged in before inserting a task
        if (! this.userId) {
          throw new Meteor.Error('not-authorized');
        }
     
        Tasks.insert({
          text,
          createdAt: new Date(),
          owner: this.userId,
          username: Meteor.users.findOne(this.userId).username,
        });
      },
      'tasks.remove'(taskId) {
        check(taskId, String);
     
        Tasks.remove(taskId);
      },
      'tasks.setChecked'(taskId, setChecked) {
        check(taskId, String);
        check(setChecked, Boolean);
     
        Tasks.update(taskId, { $set: { checked: setChecked } });
      },
    });
    ```
* call

    ```js
    Meteor.call('tasks.insert', text);
    ```

## publish, subscribe (即時更新資料)

* publish

    ```js
    // tasks.js
    if (Meteor.isServer) {
      // This code only runs on the server
      Meteor.publish('tasks', function tasksPublication() {
        return Tasks.find();
      });
    }
    ```

* subscribe

    ```js
    // App.jsx
    export default createContainer(() => {
      Meteor.subscribe('tasks');
     
      return {
        tasks: Tasks.find({}, { sort: { createdAt: -1 } }).fetch(),
        incompleteCount: Tasks.find({ checked: { $ne: true } }).count(),
    ```

## Database

* [官方教學 3](https://www.meteor.com/tutorials/react/collections)

* Create collection

    ```js
    // imports/api/tasks.js
    import { Mongo } from 'meteor/mongo';
 
    export const Tasks = new Mongo.Collection('tasks');
    ```

* Load tasks collection on the server

    ```js
    // server/main.js
    import '../imports/api/tasks.js';
    ```

* Using data from a collection inside a React component

    To use data from a Meteor collection inside a React component, we can use an Atmosphere package react-meteor-data which allows us to create a "data container" to feed Meteor's reactive data into React's component hierarchy.
    We need to install that package alongside a NPM package it utilizes, react-addons-pure-render-mixin:
    
    ```
    meteor npm install --save react-addons-pure-render-mixin
    meteor add react-meteor-data
    ```
    
    To use react-meteor-data, we need to wrap our component in a container using the createContainer Higher Order Component:
    
    ```js
    import React, { Component, PropTypes } from 'react';
    import { createContainer } from 'meteor/react-meteor-data';
     
    import { Tasks } from '../api/tasks.js';
     
    import Task from './Task.jsx';
     
    // App component - represents the whole app
    class App extends Component {
      renderTasks() {
        return this.props.tasks.map((task) => (
          <Task key={task._id} task={task} />
        ));
      }
    ...some lines skipped...
        );
      }
    }
    
    // propTypes are defined as properties on the constructor instead of in the class body
    App.propTypes = {
      tasks: PropTypes.array.isRequired,
    };
     
    export default createContainer(() => {
      return {
        tasks: Tasks.find({}).fetch(),  // fetch data from MongoDB
      };
    }, App);  // data injected into App component as props
    ```
    
    注意[In ES6, propTypes and defaultProps are defined as properties on the constructor instead of in the class body.](https://facebook.github.io/react/docs/reusable-components.html#es6-classes)
    
    
