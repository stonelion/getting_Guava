# Event Publishing – An example
现在看看事件生产者的例子:
```
public class SimpleTradeExecutor {

    private EventBus eventBus;

    public SimpleTradeExecutor(EventBus eventBus) {
        this.eventBus = eventBus;
    }

    public void executeTrade(TradeAccount tradeAccount, double
amount, TradeType tradeType){
        TradeAccountEvent tradeAccountEvent = processTrade(tradeAccount, amount, tradeType);
        eventBus.post(tradeAccountEvent);
    }

    private TradeAccountEvent processTrade(TradeAccount tradeAccount, double amount, TradeType tradeType){
        Date executionTime = new Date();
        String message = String.format("Processed trade for %s of amount %n type %s @
%s",tradeAccount,amount,tradeType,executionTime);
        TradeAccountEvent tradeAccountEvent = new TradeAccountEvent(tradeAccount,amount,executionTime,tradeType);
        System.out.println(message);
        return tradeAccountEvent;
    }
}
```
和SimpleTradeAuditor类类似，我们在SimpleTradeExecutor构造器中使用EventBus类实例。不同的是，我们存储EventBus的引用。于之后使用。看起来很平常，但是还是要保证相同的实例传递到订阅和消费处。SimpleTradeExecutor类有一个public方法，executeTrade，接受所有处理交易的信息。当processTrade方法执行完毕，我们用返回的TradeAccountEvent实例调用EventBus.post。这样会通知所有TradeAccountEvent对象的订阅者。
