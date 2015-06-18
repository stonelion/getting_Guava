# Finer-grained subscribing
We have just seen examples on publishing and subscribing using the EventBus class.
If we recall, EventBus publishes events based on the type accepted by the subscribed
method.
EventBus投递事件是基于消费者接收方法的类型的。这让我们可以灵活的通过类型来发送事件给不同的订阅者。例如，我们想要分别审计买入和卖出的交易。首先，建立两个不同的事件类型。
```
    public class SellEvent extends TradeAccountEvent {
        public SellEvent(TradeAccount tradeAccount, double amount, Date tradExecutionTime) {
            super(tradeAccount, amount, tradExecutionTime,TradeType.SELL);
        }
    }

    public class BuyEvent extends TradeAccountEvent {
        public BuyEvent(TradeAccount tradeAccount, double amount, Date tradExecutionTime) {
            super(tradeAccount, amount, tradExecutionTime, TradeType.BUY);
    }
}
```
现在，我们建立了两个具体的事件类，SellEvent和BuyEvent。要分别地审计，我们先建立一个审计SellEvent实例的类：
```
    public class TradeSellAuditor {
        private List<SellEvent> sellEvents = Lists.newArrayList();
        public TradeSellAuditor(EventBus eventBus) {
            eventBus.register(this);
        }

        @Subscribe
        public void auditSell(SellEvent sellEvent){
            sellEvents.add(sellEvent);
            System.out.println("Received SellEvent "+sellEvent);
        }
        public List<SellEvent> getSellEvents() {
            return sellEvents;
        }
}
```

然后我们建立一个类，用于审计BuyEvent实例。
```
    public class TradeBuyAuditor {
        private List<BuyEvent> buyEvents = Lists.newArrayList();
        public TradeBuyAuditor(EventBus eventBus) {
            eventBus.register(this);
        }

        @Subscribe
        public void auditBuy(BuyEvent buyEvent){
          buyEvents.add(buyEvent);
          System.out.println("Received TradeBuyEvent "+buyEvent);
        }

     public List<BuyEvent> getBuyEvents() {
           return buyEvents;
        }
    }
```
现在，我们需要重构SimpleTradeExecutor类，根据是买或卖交易创建正确的TradeAccountEvent实例类。
```
public class BuySellTradeExecutor {
… deatails left out for clarity same as SimpleTradeExecutor
//The executeTrade() method is unchanged from SimpleTradeExecutor

    private TradeAccountEvent processTrade(TradeAccount tradeAccount, double amount, TradeType tradeType) {
        Date executionTime = new Date();
        String message = String.format("Processed trade for %s of amount %n type %s @ %s", tradeAccount, amount, tradeType,
executionTime);
        TradeAccountEvent tradeAccountEvent;
        if (tradeType.equals(TradeType.BUY)) {
            tradeAccountEvent = new BuyEvent(tradeAccount, amount,executionTime);
        } else {
            tradeAccountEvent = new SellEvent(tradeAccount,amount, executionTime);
        }
            System.out.println(message);
            return tradeAccountEvent;
    }
}
```
我们注册不同的消费者，投递不同的事件。但是，这些修改对于EventBus实例而言完全是透明的。如果我们想要根据时间的类型，分开处理，我们可以简单的添加对时间的类型检查。最后，如果需要，我们也可以定义有多个订阅方法的类：

```
    public class AllTradesAuditor {
        private List<BuyEvent> buyEvents = Lists.newArrayList();
        private List<SellEvent> sellEvents = Lists.newArrayList();

        public AllTradesAuditor(EventBus eventBus) {
            eventBus.register(this);
        }

        @Subscribe
        public void auditSell(SellEvent sellEvent){
            sellEvents.add(sellEvent);
            System.out.println("Received TradeSellEvent"+sellEvent);
        }

        @Subscribe
        public void auditBuy(BuyEvent buyEvent){
            buyEvents.add(buyEvent);
            System.out.println("Received TradeBuyEvent "+buyEvent);
        }
}
```
