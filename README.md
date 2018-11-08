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
1. 使用 Hibernate 二级缓存的步骤:  

1). 加入二级缓存插件的 jar 包及配置文件:  

I. 复制 \hibernate-release-4.2.4.Final\lib\optional\ehcache\*.jar 到当前 Hibrenate 应用的类路径下.  
II. 复制 hibernate-release-4.2.4.Final\project\etc\ehcachexml 到当前 WEB 应用的类路径下  

2). 配置 hibernate.cfg.xml   

I.   配置启用 hibernate 的二级缓存  
\<property name="cache.use_second_level_cache">true\</property>  

II.  配置hibernate二级缓存使用的产品  
\<property name="hibernate.cache.region.factory_class">org.hibernate.cache.ehcache.EhCacheRegionFactory\</property>  

III. 配置对哪些类使用 hibernate 的二级缓存  
\<class-cache usage="read-write" class="com.atguigu.hibernate.entities.Employee"/>  
		
实际上也可以在 .hbm.xml 文件中配置对哪些类使用二级缓存, 及二级缓存的策略是什么.   

2). 集合级别的二级缓存的配置  

I. 配置对集合使用二级缓存  

\<collection-cache usage="read-write" collection="com.atguigu.hibernate.entities.Department.emps"/>  

也可以在 .hbm.xml 文件中进行配置  

\<set name="emps" table="GG_EMPLOYEE" inverse="true" lazy="true">  
	\<cache usage="read-write"/>  
    \<key>  
        \<column name="DEPT_ID" />  
    \</key>  
    \<one-to-many class="com.atguigu.hibernate.entities.Employee" />  
\</set>  

II. 注意: 还需要配置集合中的元素对应的持久化类也使用二级缓存! 否则将会多出 n 条 SQL 语句.   

3). ehcache 的 配置文件: ehcache.xml  

4).  查询缓存: 默认情况下, 设置的缓存对 HQL 及 QBC 查询时无效的, 但可以通过以下方式使其是有效的  

I.  在 hibernate 配置文件中声明开启查询缓存  

\<property name="cache.use_query_cache">true\</property>  

II. 调用 Query 或 Criteria 的 setCacheable(true) 方法  

III. 查询缓存依赖于二级缓存  
