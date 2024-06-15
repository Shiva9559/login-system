import React from 'react';
import Welcome from "./Welcome";
import Signup from "./Signup"

class LoginControl extends React.Component{
  constructor(props){
    super(props);
    this.state = {
      users: [
        { username:"code", password:"blogger" },
        { username:"true", password:"codes" },
        { username:"furkan", password:"gulsen" }
      ],
      welcomeConnect: false,
      trueUsername: "",
      isSign: false,
      isSignUp: false
    }
    this.new = this.props;
  }


  Control = () => {
    var newState = this.state.users.concat(this.new.newUser)
    if(this.new.newUser !== undefined){
      this.setState({
        users:  newState
      })
    }

    var username = document.getElementById("username");
    var password = document.getElementById("password");
    this.state.users.map( (user) => {
      if(user.username === username.value && user.password === password.value){
        return(
          this.setState({
            welcomeConnect: true,
            trueUsername: user.username,
          })
        )
      }
    })
  };

  SignUp = () => {this.setState({isSign: true})};


  render(){
    return(
      <div>
      {
        this.state.welcomeConnect 
        ? 
          <Welcome uName={this.state.trueUsername}/>
        :
          (
            this.state.isSign ?
            <Signup dataState={this.state} isClick={this.state.welcomeConnect} />
            : 
            <div className="main_box--main--login">
              <input type="text" id="username" 
              className="form-control"
              placeholder="username" 
              autoComplete="false"/>  
              <input type="password" 
              id="password" className="
              form-control" 
              placeholder="password"/>
              <button className="btn btn-success" onClick={this.Control}>LOGIN</button>
              <p onClick={this.SignUp}
                style={{textAlign:"center",color:"#262626",marginTop:"-5px",cursor:"pointer"}}>Sign Up</p>
            </div>
          ) 

      }
      </div>

    )
  }
}

export default LoginControl;
 34 changes: 34 additions & 0 deletions34  
React Login System/Components/Navbar.jsx
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,34 @@
import React from 'react';
import LoginControl from "./LoginControl";
import "./NavbarStyle.css";


class Navbar extends React.Component {
  constructor(props){
    super(props);
  }


  render() {
    const {header_h2__bold, header_title, header_info, main_title, main_info} = this.props;
    return (
      <div className="main_box">

        <div className="main_box--header">
          <h2><b>{header_h2__bold}</b> {header_title} </h2>
          <p>{header_info}</p>
        </div>

        <div className="main_box--main">
        <div className="main_box--main--title">
            <h4>{main_title}</h4>
            <p>{main_info}</p>
          </div>
          <LoginControl />
        </div>
      </div>
    )
  }
} 

export default Navbar;
 68 changes: 68 additions & 0 deletions68  
React Login System/Components/NavbarStyle.css
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,68 @@
.main_box{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}

/* Header */
.main_box--header{
  margin-top: -200px;
  margin-bottom: 50px;
  width: 700px;
  text-align: center;
}
.main_box--header h2{
  color: #fff;
  font-size: 32px;
}
.main_box--header p{
  color: #ccc;
  font-size: 20px;
}

/* Main */
.main_box--main{
  width: 500px;
  height: auto;
  position: relative;
  border-radius: 7.5px;
  box-shadow: 0px 0px 25px rgba(0,0,0,.35);
}
.main_box--main--title{
  width: 100%;
  height: 100px;
  background: rgb(250,250,250);
  padding: 20px;
  border-radius: 7.5px 7.5px 0px 0px  ;
}
.main_box--main--login{
  padding: 20px;
  width: 100%;
  height: 210px;
  background: rgb(200, 200, 200);
  box-shadow: inset 0px 5px 5px rgba(0,0,0,.15); 
  border-radius: 0px 0px 7.5px 7.5px;
}
.main_box--main--signUp{
  padding: 20px;
  width: 100%;
  height: 250px;
  background: rgb(200, 200, 200);
  box-shadow: inset 0px 5px 5px rgba(0,0,0,.15); 
  border-radius: 0px 0px 7.5px 7.5px;
}
.main_box--main--login input,
.main_box--main--signUp input{
  margin: 10px 0px ;
  box-shadow: 0px 0px 10px rgba(0,0,0,.25);
}
.main_box--main--login button,
.main_box--main--signUp button{
  margin: 10px 0px;
  box-shadow: 0px 0px 10px rgba(0,0,0,.25);
  padding: 7.5px;
  width: 100%;
  cursor: pointer;
}
 54 changes: 54 additions & 0 deletions54  
React Login System/Components/Signup.jsx
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,54 @@
import React, { Component } from 'react'
import LoginControl from "./LoginControl"


class Signup extends Component {
  constructor(props){
    super(props);
    this.state = {
      isSignUp: false,
      newUser: null
    }
  }


  NewUser = () => {
    var username = document.getElementById("signUpUsername").value;
    var password1 = document.getElementById("signUpPassword1").value;
    var password2 = document.getElementById("signUpPassword2").value;
    if(password1 === password2){
      if(username !== ""){
        this.setState({
          isSignUp: true,
          newUser: {username: username, password: password1}
        });
      }else{
        alert("User name cannot be blank.")
      }
    }
    else{
      alert("The passwords you entered do not match.");
    }
  }


  render() {
    return (
      <div>
      {
        this.state.isSignUp ?
        <LoginControl newUser={this.state.newUser}/>
        :
        <div className="main_box--main--signUp">
          <input type="text" id="signUpUsername" className="form-control" placeholder="username" autoComplete="false"></input>
          <input type="password" id="signUpPassword1" className="form-control" placeholder="password" ></input>
          <input type="password" id="signUpPassword2" className="form-control" placeholder="re-enter password" ></input>
          <button className="btn btn-success" onClick={this.NewUser}>SIGN UP</button>
        </div>  
      }
      </div>
    )
  }
}

export default Signup;
 22 changes: 22 additions & 0 deletions22  
React Login System/Components/Welcome.jsx
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,22 @@
import React from 'react'

const boxStyle = {
  width: "500px",
  height: "200px",
  background:"rgb(245,245,245)",
  textAlign:"center",
  position:"absolute",
  color:"#262626",
  top: 0,
  left: 0,
  lineHeight:"190px",
  borderRadius:"10px"
}

const Welcome = (props) => {
  return(
    <h2 style={boxStyle}>WELCOME {props.uName}</h2>
  )
}

export default Welcome;
 Binary file addedBIN +520 KB 
React Login System/Components/loginWallpaper.jpg

 6 changes: 6 additions & 0 deletions6  
React Login System/Containers/App.css
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,6 @@
body{
  background-image: url('../Components/LoginSystem/loginWallpaper.jpg');
  background-size: cover;
  background-repeat: no-repeat;
  overflow: hidden;
}
 33 changes: 33 additions & 0 deletions33  
React Login System/Containers/App.js
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,33 @@
import React from 'react';
import './App.css';
import Navbar from "../Components/Navbar";

class App extends React.Component{
  state = {
    // header 
    header_h2__bold: "React",
    header_title: "Login System",
    header_info: "Lorem Ipsum dolar...",

    // main
    main_title: "Login to our site",
    main_info: "Enter your username and password to log on",
  }

  render(){
    const state = this.state;
    return(
      <div className="container mt-5" >
        <Navbar
          header_h2__bold = {state.header_h2__bold}
          header_title = {state.header_title}
          header_info = {state.header_info}
          main_title = {state.main_title}
          main_info = {state.main_info}
        />  
      </div>
    )
  }
}

export default App;
 21 changes: 21 additions & 0 deletions21  
React Login System/License.md
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,21 @@
MIT License

Copyright (c) 2019 Codeblogger

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
 25 changes: 25 additions & 0 deletions25  
React Login System/index.html
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,25 @@
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <!-- <link rel="stylesheet" href="../node_modules/animate.css/animate.min.css"> -->
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.8.2/css/all.css">
    <title>React App 3</title>

  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>

    <div id="root"></div> 


<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
<script src="https://code.jquery.com/jquery-3.3.1.slim.min.js" integrity="sha384-q8i/X+965DzO0rT7abK41JStQIAqVgRVzpbzo5smXKp4YfRvH+8abtTE1Pi6jizo" crossorigin="anonymous"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js" integrity="sha384-UO2eT0CpHqdSJQ6hJty5KVphtPhzWj9WO1clHTMGa3JDZwrnQq4sF86dIHNDz0W1" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js" integrity="sha384-JjSmVgyd0p3pXB1rRibZUAYoIIy6OrQ6VrjIEaFf/nJGzIxFDsf4x0xIM+B07jRM" crossorigin="anonymous"></script>
  </body>
</html>
 9 changes: 9 additions & 0 deletions9  
React Login System/index.js
Original file line number	Diff line number	Diff line change
@@ -0,0 +1,9 @@
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './Containers/App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

serviceWorker.unregister();
