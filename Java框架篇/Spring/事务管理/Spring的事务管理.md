保存点savepoint

```java
/*
需求：AB（必须），CD（可选） 
*/
Connection conn = null;
Savepoint savepoint = null;  //保存点，记录操作的当前位置，之后可以回滚到指定的位置。（可以回滚一部分）
try{
  //1 获得连接
  conn = ...;
  //2 开启事务
  conn.setAutoCommit(false);

  A
  B
  savepoint = conn.setSavepoint(); // 设置保存点
  C
  D
  //3 提交事务
  conn.commit();
} catch(e) {
  if(savepoint != null){   //savepoint!=null 说明AB正常 CD异常  
    // 回滚到CD之前
    conn.rollback(savepoint);
    // 提交AB
    conn.commit();
  } else{   
    // 否则 AB异常
    // 回滚AB
    conn.rollback();
  }
}

```







#### Spring事务管理介绍

 

Spring提供的事务jar包.   spring-tx-3.2.0.RELEASE.jar



 