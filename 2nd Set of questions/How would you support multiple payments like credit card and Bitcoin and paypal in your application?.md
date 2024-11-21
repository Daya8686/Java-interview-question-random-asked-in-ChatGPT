# How would you support multiple payments like credit card and Bitcoin and paypal in your application?
# Supporting Multiple Payment Methods (Credit Card, Bitcoin, PayPal)

To support multiple payment methods in an application (Credit Card, Bitcoin, PayPal), you can use the Strategy Design Pattern. This pattern allows you to encapsulate different payment methods as individual classes, making it easy to add or remove a payment method without changing the code structure significantly.

## Example Design:
1. Create a `PaymentStrategy` interface to define a common method for payment processing.
2. Implement concrete classes for each payment type (Credit Card, Bitcoin, PayPal).
3. A context class can then use the `PaymentStrategy` to process the payment based on user choice.

### PaymentStrategy Interface
```java
// PaymentStrategy Interface
public interface PaymentStrategy {
    void pay(double amount);
}

// CreditCard Payment Strategy
public class CreditCardPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("Payment of $" + amount + " made using Credit Card.");
    }
}

// Bitcoin Payment Strategy
public class BitcoinPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("Payment of $" + amount + " made using Bitcoin.");
    }
}

// PayPal Payment Strategy
public class PayPalPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("Payment of $" + amount + " made using PayPal.");
    }
}

// Payment Context
public class PaymentContext {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void executePayment(double amount) {
        paymentStrategy.pay(amount);
    }
}

// Usage
public class PaymentDemo {
    public static void main(String[] args) {
        PaymentContext context = new PaymentContext();

        // Pay with Credit Card
        context.setPaymentStrategy(new CreditCardPayment());
        context.executePayment(100.0);

        // Pay with Bitcoin
        context.setPaymentStrategy(new BitcoinPayment());
        context.executePayment(200.0);

        // Pay with PayPal
        context.setPaymentStrategy(new PayPalPayment());
        context.executePayment(300.0);
    }
}
```

