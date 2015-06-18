# Dependency injection
为了保证我们使用相同的EventBus类进行消费和生产，使用依赖注入框架(Spring 或 Guice)可以让这件事更容易。下面的例子，我们展示如何使用Spring框架配置SimpleTradeAuditor和SimpleTradeExecutor类。

```
    @Component
    public class SimpleTradeExecutor {
        private EventBus eventBus;
        @Autowired
        public SimpleTradeExecutor(EventBus eventBus) {
            this.eventBus = checkNotNull(eventBus, "EventBus can't be null");
        }
        @Component
        public class SimpleTradeAuditor {
            private List<TradeAccountEvent> tradeEvents = Lists.newArrayList();

        @Autowired
        public SimpleTradeAuditor(EventBus eventBus){
            checkNotNull(eventBus,"EventBus can't be null");
            eventBus.register(this);
        }
    }
```

```
    @Configuration
    @ComponentScan(basePackages = {"bbejeck.guava.chapter7.publisher","bbejeck.guava.chapter7.subscriber"})
    public class EventBusConfig {
        @Bean
        public EventBus eventBus() {
            return new EventBus();
        }
    }
```

