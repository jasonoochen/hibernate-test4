# hibernate-test4  
ppt132  
  
1. HQL 查询  
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
5. left join fetch  
6. left join  
7. QBC 查询  
  criteria  
    //1. 创建一个 Criteria 对象  
		Criteria criteria = session.createCriteria(Employee.class);  
		
		//2. 添加查询条件: 在 QBC 中查询条件使用 Criterion 来表示  
		//Criterion 可以通过 Restrictions 的静态方法得到  
		criteria.add(Restrictions.eq("email", "SKUMAR"));  
		criteria.add(Restrictions.gt("salary", 5000F));  
		
		//3. 执行查询  
		Employee employee = (Employee) criteria.uniqueResult();  
8. 本地sql查询  
9. 二级缓存 second-level cache ppt145  
