# ![GA LOGO](https://camo.githubusercontent.com/6ce15b81c1f06d716d753a61f5db22375fa684da/68747470733a2f2f67612d646173682e73332e616d617a6f6e6177732e636f6d2f70726f64756374696f6e2f6173736574732f6c6f676f2d39663838616536633963333837313639306533333238306663663535376633332e706e67) React ATM application

Let's make an ATM app! You will practice the dark art of manipulating components in real time.  You will create two components of the same class which will work independently of each other.  

<img width="992" alt="atm" src="https://cloud.githubusercontent.com/assets/4304660/24376818/18c39a82-12f2-11e7-81e7-af618c22b3ed.png">

Clone this repo, and run `npm install`. To launch the app, run `npm start`

### In `src/App.js`:
1. Pass a `name` property to each `Account` component, one for "Checking", the other for "Savings".  These will be used and accessed as `props`for our component. **Remember**: Props are immutable, that is, once they are declared, they cannot be changed while the application is running.

    <details>
    <summary>Hint:</summary>

    ```javascript
        <div>
          <Account name="Checking"/>
          <Account name="Savings"/>
        </div>
    ```

    </details


### In `src/Account.js`
2. Use the property you set in `App.js` and add it to the `<h2>`
    <details>
    <summary>Hint:</summary>

    ```javascript
        <div className="account">
          //this.props.name is referring to the name property we assigned the App component in App.js
          <h2>{this.props.name}</h2>
          <div className="balance">$0</div>
          <input type="text" placeholder="enter an amount" />
          <input type="button" value="Deposit" />
          <input type="button" value="Withdrawl" />
        </div>
    ```



    </details>

    Save your work. You should see two components named Checking and Savings.  You're getting there!


3. Add a `balance` property to `state` and set to 0 initially
    <details>
    <summary>Hint:</summary>

    ```javascript
        class Account extends Component {
            constructor(props){
              super(props)
              this.state = {
                balance: 0
              }
            }
        }
    ```

    </details>

<img src="https://media.giphy.com/media/26xBMuHu0ZFngH7Ta/giphy.gif">

4. Set a `ref` on the text field for targeting. This way we can access the data in the later when we want to know what values to add/subtract from our account.

    <details>
    <summary>Hint:</summary>

    ```html
      <input type="text" placeholder="enter an amount" ref="amount" />
    ```

    </details>

5. When the `Deposit` button is clicked, you should add the amount entered in the text field to the balance
    <details>
    <summary>Hint:</summary>
    a. Add a click handler in your input tags in our JSX return block:

    ```html
      <input type="button" value="Deposit" onClick={(e) => this.handleDepositClick(e)} />
    ```

    b. Define a click handler method within the `Account` class

    ```javascript
      handleDepositClick(e) {
        // It is good practice to still prevent default behavior
        e.preventDefault()
        // set a local variable to the amount entered in the text box.
        let amount = this.refs.amount.value
        // set a local variable to the new balance based off of the original balance + amount
        let newBalance = this.state.balance + amount;
        // set the balance to the newBalance using the setState method (necessary)
        this.setState({
          balance: newBalance
        })
        // empty out the text box in this component
        this.refs.amount.value = '';
      }
    ```

     PS - the amount entered in the text field will initially be a string, so you'll need to convert that to a number



    </details>



6. When the `Withdraw` button is clicked, you should deduct the amount entered in the text field to the balance.  **You should not be able to withdraw more than the current balance**

    <details>
    <summary>Hint:</summary>

      Try to mirror the functionality of the Deposit function above.

    </details>


7. If the current balance is 0, you should add a class of `zero` to the `<div className="balance">`. You can complete these computations in the render method, but before the JSX portion is returned.
    <details>
    <summary>Hint:</summary>
        In the Account.js render method:

    ```javascript
      // set the default class to `balance` for the balanceClass.
      let balanceClass = 'balance';
      // if the balance is 0, then add the class zero to balanceClass
      if (this.state.balance === 0) {
        balanceClass += ' zero';
      }
    ```  

    <p>Replace the hardcoded `balance` class with the balanceClass variable in your return jsx code block:</p>

    ```html
        <div className={balanceClass}>$0</div>
    ```

    </details>
