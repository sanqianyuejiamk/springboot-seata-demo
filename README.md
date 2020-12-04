# springboot-seata-demo

### Distributed Transaction Solution with SEATA

<img src="https://seata.io/img/solution.png"/>

### 启动seata
alibaba_seata/seata/bin

```
sh seata-server.sh --port 8091 -m file
```

### business-service
```java
    /**
     * 减库存，下订单
     *
     * @param userId
     * @param commodityCode
     * @param orderCount
     */
    @GlobalTransactional
    public void purchase(String userId, String commodityCode, int orderCount) {
        LOGGER.info("purchase begin ... xid: " + RootContext.getXID());
        storageClient.deduct(commodityCode, orderCount);
        orderClient.create(userId, commodityCode, orderCount);
    }
```
