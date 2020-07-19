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
