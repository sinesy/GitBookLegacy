In case of a **Custom Java grid component,** a java programmer has to create externally a java plain class, using a Java IDE, such as Eclipse.
This java bean should be created as a Stateless EJB 3.0 bean and must have as a mandatory attribute the attribute &#8220;em&#8221; as in the following scriptlet:

```js
@
```

 **Stateless** 

```js
public class YourList
```

 **Bean** 

```js
 implements YourList
```

 **Local** 

```js
 {
  


```

 ** @PersistenceContext(unitName=&#8221;DB4WS&#8221;) private EntityManager em; public void setEm(EntityManager em) { this.em = em; }** 

```js
  @Resource(mappedName="java:/DB4WS")
  private DataSource ds;

  public void setDataSource(DataSource ds) {
    this.ds = ds;
  }

  private HashMap&lt;Long,DataSource&gt; ads;

  /**
   * If present any additional datastores these are injected as a Datasource map from DirectCallServerProxy
   * @param ads
   */
  public void setAdditionalDataSources(HashMap&lt;Long,DataSource&gt; ads) {
    this.ads = ads;
  }

```

Optionally, you can also include additional attributes: ds and ads.The latter is used to access any additional datastore defined at application level.
Within that bean, you can define a java method which will be invoked by the grid as a business component.
Suppose that you define as component name in the b.c. definition: &#8220; **YourListBean.getList** &#8220;, in that case, you have to define a java method named &#8220;getList&#8221; inside your &#8220;YourListBean&#8221; class.
You can name your method as you wish, but the signature of that method must be as follows:

```js
public void getList(

```

 ** it.tinet.warp.common.datamanagement.java.ListCommandlc,  org.wag.renderer.java.JSONListRenderer listRenderer** 

```js
);
```

Thanks to the &#8220;ListCommand&#8221; argument you can access to filtering and ordering conditions coming from the grid, as well as pagination settings.
You can use the Warp framework to use the utility methods (for SQL or JPA) to make it easy the enquery process.
The second argument must be used to compose, record by record, the response in JSON format.
See the JSONListRenderer structure for more details.


In case of a **Custom Java detailcomponent,** a java programmer has to create externally a java plain class, using a Java IDE, such as Eclipse.
This java bean should be created as a Stateless EJB 3.0 bean and must have as a mandatory attribute the attribute &#8220;em&#8221; as in the following scriptlet:

```js
@
```

 **Stateless** 

```js
public class YourDetail
```

 **Bean** 

```js
 implements YourDetail
```

 **Local** 

```js
 {
  


```

 ** @PersistenceContext(unitName=&#8221;DB4WS&#8221;) private EntityManager em; public void setEm(EntityManager em) { this.em = em; }** 

```js
  @Resource(mappedName="java:/DB4WS")
  private DataSource ds;

  public void setDataSource(DataSource ds) {
    this.ds = ds;
  }

  private HashMap&lt;Long,DataSource&gt; ads;

  /**
   * If present any additional datastores these are injected as a Datasource map from DirectCallServerProxy
   * @param ads
   */
  public void setAdditionalDataSources(HashMap&lt;Long,DataSource&gt; ads) {
    this.ads = ads;
  }

```

Optionally, you can also include additional attributes: ds and ads.The latter is used to access any additional datastore defined at application level.
Within that bean, you can define a java method which will be invoked by the formas a business component.
Suppose that you define as component name in the b.c. definition: &#8220; **YourDetailBean.getDetail** &#8220;, in that case, you have to define a java method named &#8220;getDetail&#8221; inside your &#8220;YourDetailBean&#8221; class.
You can name your method as you wish, but the signature of that method must be as follows:

```js
public void getDetail(

```

 ** it.tinet.warp.common.datamanagement.java.ServerCommandsc, HashMap pk,  org.wag.renderer.java.JSONVORenderer renderer** 

```js
);
```

Thanks to the &#8220;ServerCommand&#8221; argument you can access toadditional info, such as the username, language and so forth.
You can use the Warp framework to use the utility methods (for SQL or JPA) to make it easy the enquery process.
Through the second argument you can access to the primary key values (attributes/values) that you can add to your WHERE condition.
The lastargument must be used to compose the response in JSON format.
See the JSONVORenderer structure for more details.


                

---


