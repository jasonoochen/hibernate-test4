# hibernate-test4  
ppt132  
  
1. HQL  
  a. 创建 Query 对象  
    - 基于命名参数.   
    - 基于位置的参数.   
  b. 绑定参数  
    - Query 对象调用 setXxx 方法支持方法链的编程风格.  
  c. 执行查询  
2. 分页查询  
  a. setFirstResult(int firstResult)  
  b. setMaxResults(int maxResults)  
3. 在映射文件中定义命名查询语句  
  Hibernate 允许在映射文件中定义字符串形式的查询语句.  
  \<query name="salaryEmps">\<![CDATA[FROM Employee e WHERE e.salary > :minSal AND e.salary < :maxSal]]>\</query>  
  <query> 元素用于定义一个 HQL 查询语句, 它和 <class> 元素并列.    
  在程序中通过 Session 的 getNamedQuery() 方法获取查询语句对应的 Query 对象.   
4. 投影查询  
  
