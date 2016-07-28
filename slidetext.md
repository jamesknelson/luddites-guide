# The Luddite's guide to State

- **Q:** What is component state?

--

- **A:** I didn't take these from the dictionary, but:

    *State is one of two types of data which is attached to your component. Unlike props (the other type of data), the outside world cannot control your component's state. It **stays** the same until the component decides to change it*.

    Or:

    *State is data which your component owns.*


???

- # INTRODUCE YOURSELF

+ "Luddite": people who destroyed machines because they took their jobs. Also used to refer to people who don't like fancy new technology.

---

# But enough about state

Today, I don't want to talk about what state is. I want to discuss how to avoid it. And also how to use it, when necessary. 

(That's why it is the luddite's guide).

???

+ "Luddite": people who destroyed machines because they took their jobs. Also used to refer to people who don't like fancy new technology.

---

# Why do we want to avoid state?

???

# ASK

--

- It makes components less flexible

    + Have you ever installed a UI component from somewhere, only to wish you were able to have more control over it? That is because of internal state.

--

- It makes components harder to re-use
    + Have you ever run into two very similar components, where extracting common logic is difficult due to a fetch statement (or something similar) storing state?
    + What about wanting to be able to communicate between screens, and not being able to due to state?

--

- It makes your components less clear
    + Have you ever run into a component which is totally unclear what it does without reading through the entire code? Was state the cause?

---

## A React App Without Any Component State

Can we avoid state altogether? Let's try.

---

## A React App Without Any Component State

```javascript
class CommentForm extends React.Component {
    static propTypes = {
        value: React.PropTypes.object.isRequired,
        onChange: React.PropTypes.func.isRequired,
    }

    handleChange(field, e) {
        this.props.onChange({
            ...this.props.value,
            [field]: e.target.value,
        })
    }

    render() {
        return 
            <div>
                <input
                    placeholder="Name"
                    value={this.props.value.name}
                    onChange={this.handleChange.bind(this, 'name')}
                />
                <input
                    placeholder="Message"
                    value={this.props.value.message}
                    onChange={this.handleChange.bind(this, 'message')}
                />
            </div>
        )
    }
}
```

---

## A React App Without Any Component State

```javascript
function render(value) {
    ReactDOM.render(
        <CommentForm
            value={value}
            onChange={render}
        />,
        document.getElementById("react-app")
    )
}

render({
    name: "James",
    message: "",
})
```

--

The app has no component state.


--

But it does have state. *Where?*

--

**The DOM.**

--

And weren't we using React to avoid the DOM?

---

## The inevitability of state

- Any app which does basically anything has state.
- Stateless apps suck.

--

- But we've already discussed many problems of state.
- So what can we do?

---

# Managing state

- Instead of getting rid of state, we need to manage it.
- By keeping our state in a single location, we can avoid it *most* of the time.
- But are we keeping it in one place?

---

# Managing state - types of state

- **Q:** What types of state exist in our application?

--

- DOM state (uncontrolled components, things managed with `refs`)

--

- URL and History API state (which often masquerades as "routes")

--

- Data (stuff read from the server)

--

- Communications state (`fetch`, `jQuery.ajax`)

???

What is the difference between communcations and data?

--

- View state (selected items, pagination, sort/filter, etc.)

--

- Timers

---

# Managing state - methods for managing state

--

- react-router

--

- redux

--

- component state

--

- smart components / dumb components

---

# Managing state

But if an app uses all of these, then figuring out where the state is becomes difficult.

What if there was a way to manage location, communication, data, and view all from *one place*? And what if it was re-usable?

--

To be continued...
