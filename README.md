MyBatis CDI Extension
=====================

This CDI extension allows direct injection of Mybatis Mappers into CDI Beans.

Basic usage is:

Put the mybatis-cdi.jar it your .war applications.

Create a singleton or application scoped bean to provide your SqlSessionManager. You must maintain your instance in ApplicationScope or Singleton scoped bean. Just retrieve the reference in the producer methods to avoid re-creation of the manager at injection time.

	@ApplicationScoped
	public class SessionManagerProvider {
	
		private SqlSessionManager manager;
	
		@PostConstruct
		public void init() {
			manager = create the manager instance ....
		}

		@Produces
		public SqlSessionManager getManager() {
			// Important: Do not create the manager here. 
			// just retrieve a previously created instance.
			return manager;
		}
	
	}

Inject your mappers in your beans using the Mapper annotation

	@RequestScoped
	public class MyController {
	
		@Inject @Mapper
		MyMapperInterface mapper;
	
		public void doSomething() {
			mapper.myMethod(.....);
			.....
		}
	
	}

Each method call will use an isolated session. But if you want to enclose many method calls in a transaction, mark the method with @Transactional

    @Transactional
    public void doSomeTransaction() {
      ...
      mapper.insertMyBean(...);
      mapper.updateMyBean(...);
      ...  
    }

To support this kind of transactional behaviour, you need to activate the interceptor in beans.xml

    <beans
       xmlns="http://java.sun.com/xml/ns/javaee"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
          http://java.sun.com/xml/ns/javaee
          http://java.sun.com/xml/ns/javaee/beans_1_0.xsd">
       <interceptors>
          <class>org.mybatis.cdi.LocalTransactionInterceptor</class>
       </interceptors>
    </beans>

