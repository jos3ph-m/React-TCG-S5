# Section 5 - Styling Components & Elements

## Setting Styles Dynamically

Here we will change the background color from green to red depending on if the button has been clicked:

```javascript
const style = {
  backgroundColor: "green",
  color: "white",
  font: "inherit",
  border: "1px solid blue",
  padding: "8px",
  cursor: "pointer",
  outline: "none",
};

let persons = null;

if (this.state.showPersons) {
  persons = (
    <div>
      {this.state.persons.map((person, index) => {
        return (
          <Person
            click={() => this.deletePersonHandler(index)}
            name={person.name}
            age={person.age}
            key={person.id}
            changed={(e) => this.nameChangedHandler(e, person.id)}
          />
        );
      })}
    </div>
  );
  style.backgroundColor = "red";
}
```

---

## Settings Class Names Dynamically

Here we can set class names dynamically using a simple if check.

We've set the following classes in our App.css:

```css
.red {
  color: red;
}

.bold {
  font-weight: bold;
}
```

Inside of our app, we're using the following:

```javascript
const classes = [];

if (this.state.persons.length <= 2) {
  classes.push("red");
}

if (this.state.persons.length <= 1) {
  classes.push("bold");
}
```

```javascript
<p style={{ fontSize: "20px" }} className={classes.join(" ")}>
  And I was built for gaining a more developed grasp of React
</p>
```

---

## Adding and Using Radium

To install:

```console
npm install --save radium
```

Import in app:

```javascript
import Radium from "radium";
```

Wrap app with Radium:

```javascript
export default Radium(App);
```

We can then add our pseudo class to our style variable:

```javascript
":hover": {
        backgroundColor: "lightgreen",
        color: "black",
      },
```

To add media queries:

```javascript
const style = {
  "@media (min-width: 500px)": {
    width: "450px",
  },
};
```

---

## Adding and Using Styled Components

To install:

```console
npm install --save styled-components
```

To import:

```javascript
import styled from "styled-components";
```

Utilization - remember it's css syntax rather than javascript:

```javascript
const StyledDiv = styled.div`
  width: 60%;
  margin: 16px auto;
  border: 1px solid #eee;
  box-shadow: 0 2px 3px #ccc;
  padding: 16px;
  text-align: center;

  @media (min-width: 500px) {
    width: 450px;
  }
`;
```

```javascript
<StyledDiv>
  <p onClick={props.click}>
    I'm {name} and I'm {age}... I'm from the Person component and here I am
    generating a random number: {Math.floor(Math.random() * 100)}
  </p>
  <p>{children}</p>
  <input type="text" onChange={props.changed} value={props.name} />
</StyledDiv>
```

---

## CSS Modules

#### Getting set up.

Make sure to add and commit all changes first:

```console
git add .
git commit -m 'Your message here'
```

Now we can eject:

```console
npm run eject
```

Locate the file webpack.config.dev.js and ensure yours lists as follows:

```javascript
test: /\.css$/,
use: [
  require.resolve('style-loader'),
  {
    loader: require.resolve('css-loader'),
    options: {
      importLoaders: 1,
      modules: true,
      localIdentName: '[name]__[local]__[hash:base64:5]'
    },
```

We'll also want to add the following lines to the webpack.config.prod.js file:

```javascript
modules: true,
localIdentName: '[name]__[local]__[hash:base64:5]'
```

Now we'll import the classes from our App.css file:

```javascript
import classes from "./App.css";
```

Now we can assign those classes using the following syntax:

```javascript
<button className={classes.Button} onClick={this.togglePersonsHandler}>
  Toggle Persons
</button>
```

Alternatively we can do the following. Inside of App.css:

```css
.App {
  text-align: center;
}

.red {
  color: red;
}

.bold {
  font-weight: bold;
}

.App button {
  background-color: green;
  color: white;
  font: inherit;
  border: 1px solid blue;
  padding: 8px;
  cursor: pointer;
  outline: none;
}

.App button:hover {
  background-color: lightgreen;
  color: black;
}

.App button.Red {
  background-color: red;
}

.App button.Red:hover {
  background-color: salmon;
}
```

```javascript
let btnClass = [classes.Button];
if (this.state.showPersons) {
  persons = (
    <div>
      {this.state.persons.map((person, index) => {
        return (
          <Person
            click={() => this.deletePersonHandler(index)}
            name={person.name}
            age={person.age}
            key={person.id}
            changed={(e) => this.nameChangedHandler(e, person.id)}
          />
        );
      })}
    </div>
  );
  btnClass = classes.Red;
}
```

```javascript
<button className={btnClass} onClick={this.togglePersonsHandler}>
  Toggle Persons
</button>
```
