# redux installation

To add Redux into your react project follow below steps

install these 2 package 
```bash
npm install redux react-redux
```
step 1
now we need to create store 
    go  >> index.js 
    import 
    ```bash
       import { createStore } from 'redux';
       import { Provider } from 'react-redux';
    ```
Now make store >>

```base
const store = createStore()
```
wrape your App component with Provider(used for communicate react app with redux ) >>
            ```ReactDOM.render(
                <React.StrictMode>
                    <Provider store = {store}>
                    <App />
                    </Provider>
                </React.StrictMode>,
                document.getElementById('root')
            );
           ```
step 2
create reducer (is simeple function and it has data which we want to change )
    make folder 
        ```<reducers> ```
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
   step 3 
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
