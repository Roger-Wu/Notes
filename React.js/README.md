# React.js Notes

## 學習資源

* [Official Tutorial (ES5)](https://facebook.github.io/react/docs/tutorial.html)
* [kdchang's 從零開始學 ReactJS](https://github.com/kdchang/reactjs101)



# React Router

## location

* [how to get current location](http://stackoverflow.com/questions/35031911/how-to-get-current-route-in-react-router-2-0-0-rc5)
  
  ```js
  // App.jsx
  var currentLocation = this.props.location.pathname
  ```


# Material UI

## working with React Router

1. pass props.location to MyAppBar

  ```jsx
  <MyAppBar location={this.props.location} />
  ```

2. set ```<Tab/>```'s containerElement to ```<Link/>```

  ```jsx
  <Tabs>
    <Tab label="Home" containerElement={<Link to="/"/>}></Tab>
    <Tab label="Learn" containerElement={<Link to="/learn"/>}></Tab>
    <Tab label="Train" containerElement={<Link to="/train"/>}></Tab>
  </Tabs>
  ```

3. set value of ```<Tab>``` and ```<Tabs>``` so the active ```<Tab>``` is synchronous with routing

  ```jsx
  <Tabs value={this.props.location.pathname}>
    <Tab label="Home" value="/" containerElement={<Link to="/"/>}></Tab>
    <Tab label="Learn" value="/learn" containerElement={<Link to="/learn"/>}></Tab>
    <Tab label="Train" value="/train" containerElement={<Link to="/train"/>}></Tab>
  </Tabs>
  ```

