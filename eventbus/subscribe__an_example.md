# Subscribe – An example
假设我们有如下的事件处理类`TradeAccountEvent`：
```
    public class TradeAccountEvent {
        private double amount;
        private Date tradeExecutionTime;
        private TradeType tradeType;
        private TradeAccount tradeAccount;
        public TradeAccountEvent(TradeAccount account, double amount,
Date tradeExecutionTime, TradeType tradeType) {
            checkArgument(amount > 0.0, "Trade can't be less than
zero");
            this.amount = amount;
            this.tradeExecutionTime = checkNotNull(tradeExecutionTime,"ExecutionTime can't be null");
            this.tradeAccount = checkNotNull(account,"Account can't be null");
            this.tradeType = checkNotNull(tradeType,"TradeType can't be null");
        }
//Details left out for clarity
```
当购买后销售事务执行的时候，我们会建立一个TradeAccountEvent类实例。现在假设我们需要在交易执行的时候进行审计，所以，我们有了如下定义的SimpleTradeAuditor类:
```
public class SimpleTradeAuditor {
    private List<TradeAccountEvent> tradeEvents = Lists.newArrayList();
    public SimpleTradeAuditor(EventBus eventBus){
        eventBus.register(this);
    }
    @Subscribe
    public void auditTrade(TradeAccountEvent tradeAccountEvent){
        tradeEvents.add(tradeAccountEvent);
        System.out.println("Received trade "+tradeAccountEvent);
    }
}
```
类构造器上我们接受EventBus类实例，然后立即用收到TradeAccountEvents事件的EventBus实例注册SimpleTradeAuditor类。我们指定auditTrade
为事件处理方法。这个例子中，我们只是添加TradeAccountEvent对象到list上，并在console上打印我们收到的交易。
