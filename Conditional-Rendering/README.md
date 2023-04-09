# Conditional Rendering

&emsp;It is an essential feature of React that allows you to display different content based on certain conditions. 
This can include things like user input, server responses, or the state of your application.

&emsp; Here's an example of how you could use an `if statement` to conditionally render a component 
based on whether a shipment of finished products has been delivered to the customer:
```javascript
// this component takes a prop called isDelivered, which is a boolean value
function ShipmentStatus(props) {
  const isDelivered = props.isDelivered;
  // component returns different message depending on whether shipment has been delivered or not
  if (isDelivered) {
    return <h1>Your shipment has been delivered!</h1>;
  } else {
    return <h1>Your shipment is on its way.</h1>;
  }
}

// in parent component
function App() {
  //we define an object with a property of isDelivered
  const shipmentStatus = { isDelivered: true };
  // we render ShipmentStatus component and pass in isDelivered prop
  return (
    <div>
      <h1>Shipment Status</h1>
      <ShipmentStatus isDelivered={shipmentStatus.isDelivered} />
    </div>
  );
}
```

&emsp; Example - component to detect if prepayment on an order is greater than 70% of total value so that factory can start manufacturing
```javascript
import React from 'react';

function PaymentStatus(props) {
  const { isPaymentComplete, prepaymentAmount, totalAmount } = props;
  const prepaymentPercentage = (prepaymentAmount / totalAmount) * 100;
  
  return (
    <div>
      {isPaymentComplete ? (
        <h1>Your payment has been received. Thank you!</h1>
      ) : prepaymentPercentage >= 70 ? (
        <h1>Your prepayment is greater than 70%. Manufacturing will begin soon.</h1>
      ) : (
        <h1>Please complete your payment to begin production.</h1>
      )}
    </div>
  );
}
// main component
function App() {
  const paymentStatus = {
    isPaymentComplete: false,
    prepaymentAmount: 750,
    totalAmount: 1000,
  };

  return (
    <div>
      <h1>Production Payment</h1>
      <PaymentStatus
        isPaymentComplete={paymentStatus.isPaymentComplete}
        prepaymentAmount={paymentStatus.prepaymentAmount}
        totalAmount={paymentStatus.totalAmount}
      />
    </div>
  );
}

export default App;
```

&emsp; Here's an example of how you could **render a list** of customers who confirmed the drawings for their requests and **map the data** to individual Customer components:

> **Customer.js** component:
```javascript
import React from 'react';

function Customer(props) {
  const { name, dateConfirmed } = props;
  return (
    <div>
      <h2>{name}</h2>
      <p>Confirmed on: {dateConfirmed}</p>
    </div>
  );
}

export default Customer;
```

> **CustomerList.js** component:
```javascript
import React from 'react';
import Customer from './Customer';

function CustomerList(props) {
  const customers = props.customers;
  const customerItems = customers.map((customer) =>
    <li key={customer.id}>
      <Customer name={customer.name} dateConfirmed={customer.dateConfirmed} />
    </li>
  );
  
  return (
    <div>
      <h1>Confirmed Customers</h1>
      <ul>{customerItems}</ul>
    </div>
  );
}

export default CustomerList;
```


> **App.js** component:
```javascript
import React from 'react';
import CustomerList from './CustomerList';

function App() {
  const confirmedCustomers = [
    { id: 1, name: 'John Doe', dateConfirmed: '2022-03-01' },
    { id: 2, name: 'Jane Smith', dateConfirmed: '2022-03-02' },
    { id: 3, name: 'Bob Johnson', dateConfirmed: '2022-03-03' },
  ];

  return (
    <div>
      <CustomerList customers={confirmedCustomers} />
    </div>
  );
}

export default App;
```

> > _When the App component is rendered, it will render the CustomerList component, which in turn will render a list of Customer components, each displaying the customer's name and the date they confirmed the drawings for their request._
