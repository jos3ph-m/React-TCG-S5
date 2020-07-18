# Section 5 - Styling Components & Elements

## Setting Styles Dynamically

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
