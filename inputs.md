# The “problem” with getting user input in React is that we want our state to be our single source of truth - that is, any information about or generated in a component should be kept in its state.

# However, DOM elements such as input, text-area, and select have their own form of “state” where they keep the current value of their input inside the element (remember event.target.value?)

# To make sure that we only work with state, we will bind the value of the element to state, as well as update the state each time the value of the element changes. =>

# This is called two-way binding, and we’ll see it in code in a second.
the other way around

* //don't forget arrow syntax for correct `this` binding!

# Notice that we’re using the plain, vanilla-JS event - recall that onChange fires an event each time the input changes. We can capture that event* in whichever function we invoke once the change occurs.
*As with all parameter names, the name does not have to be event

* Now, because our state updates when the input changes, and the value of input is bound to the state, we have two-way binding.

# Catch-all Handler
You now understand the basics of handling input in React. And honestly, there’s not much more to it.
The only “issue” might arise when you have multiple inputs, and you need multiple methods to manage the state changes.
There’s nothing inherently wrong with having a method for each input element - you may very well want to do different things for each input.

# That said, it is silly to have several methods that do exactly the same thing: update one property of state

class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.type === 'checkbox' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}