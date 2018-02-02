_因为spring中的bean\(即普通类）默认是单例的_

所以如果类中存在私有变量，例如

```java
public class TestManagerImpl implements TestManager{  
    private User user;    
  
    public void deleteUser(User e) throws Exception {  
        user = e ;           //1  
        prepareData(e);  
    }  
  
    public void prepareData(User e) throws Exception {  
        user = getUserByID(e.getId());            //2  
        .....  
        //使用user.getId();                       //3  
        .....  
        .....  
    }     
}  
```

对如上的user进行操作，那么user因为是单例，如果两个线程同时访问，修改user,那么user变量可能会存在值不统一的问题。





