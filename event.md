
# การจัดการ Event ของ Component 

เราสามารถใช้ method ของ Class ผูกเข้ากับ event attribute ของ HTML ได้โดยตรง

## ตัวอย่าง แบบใช้ Arrow Function

```html
<script type="text/babel">

        const Food = ({name}) => <h2>{name}</h2>;
    
        class App extends React.Component {
    
            state = {
                loggedIn: false
            }
    
            logIn = () => {
                this.setState({ loggedIn: true});
            }
    
            logOut = () => {
                this.setState({ loggedIn: false});
            }
    
            render() {
                return (
                    <div>
                        <button onClick={this.logIn}>Log In</button>
                        <button onClick={this.logOut}>Log Out</button>
                        <div>User is {this.state.loggedIn ? "logged in" : "not logged in"}</div>
                        <Food name="Tom Yam Goong"/>
                        <Food name ="Khao Pad Sapparod"/>
                    </div>
                )
            }
        }
    
        ReactDOM.render(
            <App />,
            document.getElementById("root")
        );
    
    </script>
```

### คำอธิบาย 

สังเกตว่าใน Component Class เราประกาศ method ขึ้นมา 2 method 

```js
logIn = () => {
    this.setState({ loggedIn: true});
}

logOut = () => {
    this.setState({ loggedIn: false});
}
```

คำสั่ง `this.setState({})` จะเป็นการกำหนดค่าให้กับ property `state` ใหม่ และทำให้ React ทำการ render component ตัวนั้นอีกครั้ง

### การผูก method กับ HTML Event (Event Binding)

เราสามารถกำหนด method ให้กับ event attribute ของ HTML ทั่วไปได้เลย

- สังเกตว่า `onClick={}` ไม่ใช่ `onClick="{}"`
- เรียกชื่อได้โดยตรง 

```html
<button onClick={this.logIn}>Log In</button>
```

## ตัวอย่างแบบใช้ Method ปกติ

ในกรณีที่เราไม่อยากประกาศ method แบบ Arrow function เช่น

```js
// ใช้แบบนี้
logIn() {
    this.setState({ loggedIn: true});
}

// แทนที่จะเป็นแบบนี้
logIn = () => {
    this.setState({ loggedIn: true});
} 
```

ตอน binding ใน JSX เราต้องใช้ Arrow function ร่วมกันด้วย เช่น 

```html
<button onClick={e => this.logIn()}>Log In</button>
```

ตัวอย่างแบบเต็ม

```html
<script type="text/babel">

        const Food = ({name}) => <h2>{name}</h2>;
    
        class App extends React.Component {
    
            state = {
                loggedIn: false
            }
    
            logIn() {
                this.setState({ loggedIn: true});
            }
    
            logOut() {
                this.setState({ loggedIn: false});
            }
    
            render() {
                return (
                    <div>
                        <button onClick={e => this.logIn()}>Log In</button>
                        <button onClick={e => this.logOut()}>Log Out</button>
                        <div>User is {this.state.loggedIn ? "logged in" : "not logged in"}</div>
                        <Food name="Tom Yam Goong"/>
                        <Food name ="Khao Pad Sapparod"/>
                    </div>
                )
            }
        }
    
        ReactDOM.render(
            <App />,
            document.getElementById("root")
        );
    
    </script>
```