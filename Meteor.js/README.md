# Meteor.js

## 使用Meteor的好處
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

    [官方教學 step 2](https://www.meteor.com/tutorials/react/components)
    ```
    meteor npm install --save react react-dom
    meteor npm install --save react-addons-pure-render-mixin
    ```
    [官方教學 step 3](https://www.meteor.com/tutorials/react/collections)
    ```
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

    // tasks.js
    ```js
    if (Meteor.isServer) {
      // This code only runs on the server
      Meteor.publish('tasks', function tasksPublication() {
        return Tasks.find();
      });
    }
    ```

* subscribe

    // App.jsx
    ```js
    export default createContainer(() => {
      Meteor.subscribe('tasks');
     
      return {
        tasks: Tasks.find({}, { sort: { createdAt: -1 } }).fetch(),
        incompleteCount: Tasks.find({ checked: { $ne: true } }).count(),
    ```
