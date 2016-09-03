# Anything about style

## Using scss/sass
* https://atmospherejs.com/fourseven/scss
* ```meteor add fourseven:scss```

## Using Bootstrap
* https://atmospherejs.com/twbs/bootstrap
* ```meteor add twbs:bootstrap```

## Using Material UI
* [Material UI](http://www.material-ui.com/#/)
* [How to Install Material UI in Meteor](https://forums.meteor.com/t/cannot-use-material-ui-with-meteor/26379/3)
* Install

  ```
  meteor npm install --save material-ui
  meteor npm install --save react-tap-event-plugin
  ```

* Usage
  * main.jsx
  
    ```js
    // main.jsx
    import injectTapEventPlugin from 'react-tap-event-plugin';
    ...
    Meteor.startup(() => {
      injectTapEventPlugin();
      ...
    });
    ```
    
  * App.jsx
    
    ```js
    import MuiThemeProvider from 'material-ui/styles/MuiThemeProvider';
    ...
    class App extends Component {
      render() {
        return (
          <MuiThemeProvider muiTheme={muiTheme}>
            ...
          </MuiThemeProvider>
        );
      }
    }
    ```
    
  * MyComponent.jsx
  
    ```js
    import RaisedButton from 'material-ui/RaisedButton';
    
    const MyComponent = () => (
      <RaisedButton label="Default" />
    );
    ```
    
