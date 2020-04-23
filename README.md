# redux installation

To add Redux into your react project follow below steps

install these 2 package 
    ```bash
    npm install redux react-redux
    ```
### step 1
now we need to create store
go  >> index.js 
    import 
    ```bash
       import { createStore } from 'redux';
       import { Provider } from 'react-redux';
    ```
 Now make store 

```base
const store = createStore()
```
wrape your App component with Provider(used for communicate react app with redux ) 
  ```
  ReactDOM.render(
                <React.StrictMode>
                    <Provider store = {store}>
                    <App />
                    </Provider>
                </React.StrictMode>,
                document.getElementById('root')
            );
  ```
  
### step 2
 create reducer (is simeple function and it has data which we want to change )
 make folder 
        ```
            <reducers> 
         ```
 make file reducer.js
   ``` 
    const istate = {
    name:'jemish',
    login:false
    }
    export const reducer = (state = istate, action) => {
    return state
    }
   ```
   import this file into index.js 
   we need to assign reduser in createStore() 
    ```base
        const store = createStore(reducer)
    ```
   ### step 3 
   access these data into the App component 
   
   ```import {connect} form 'react-redux'```
   
   wrap the App component with connect like
   ```export default connect()(App);```
so now we need to get the state data and convert into the props 
  ```
    const mapStateToProps = (state) =>{
        return{
        myname:state.name,
        islogin:state.login
        }
     }
  ```
and pass it into the connect()
```
export default connect(mapStateToProps)(App);
```
### step 4
update the state value 
make one functin in the app component 
```const mapDispatchToProps = (dispatch) => {
  return {
      changeData:(name) =>{dispatch({type:'CHANGE_NAME',data:name})}
  }
}
```
and export it like this
```
export default connect(mapStateToProps, mapDispatchToProps)(App);
```

now come to the reducer function where action perameter is set 
```
 const reducer = (state = istate, action) => {
    console.log('this is action ',action)
     if (action.type === 'CHANGE_NAME'){
        return{
            ...state,
            name:action.data
        }
    }
    else{
        return state
    }
}
```

# redux thunk 
it is one package or middelware used for performing async task like get/post/put.. etc 

## instalation 
``` 
npm install redux-thunk
```
index.js
```
import { createStore, applyMiddleware } from 'redux';
import thunk from 'redux-thunk';
```
```
const store = createStore(reducer,applyMiddleware(thunk));
```

or if you are useing google chrome extension redux then
```
  import { createStore, applyMiddleware, compose } from 'redux';
  const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
  const store = createStore(reducer, composeEnhancers(applyMiddleware(thunk)));
```
create myaction2.js in action folder

```
export const anotherChange = () => {
    return (dispatch)=>{
        fetch('https://jsonplaceholder.typicode.com/todos')
        .then(respo=>respo.json())
        .then(result=>{
            dispatch({type:'THUNKCHANGE',data:result[0].title})
        })
    }
  }
export default anotherChange
```
import it into app.js file 
get data 
```
const mapStateToProps = (state) =>{
  return{
    myname:state.name,
    islogin:state.login,
    title:state.title
  }
}
```

```
const mapDispatchToProps = (dispatch) => {
  return {
      changeData:(name) =>{dispatch(anotherName(name))},
      thunkChange:() =>{dispatch(anotherChange())},
  }
}
```

```
               <button onClick={()=>{props.thunkChange()}}>Thunk change</button>
```
make action on button clicked 
```
else if(action.type === 'THUNKCHANGE') {
        return {
            ...state,
            title: action.data
        }
    }
```



 



