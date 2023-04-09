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


