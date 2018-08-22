## BeanFactory 继承体系

---

BeanFactory是Spring框架最核心的接口，它提供了高级IOC的配置机制。BeanFactory使用管理不同类型的java对象成为可能，应用上下文ApplicationContext建立在BeanFactory基础之上，提供了更多面向应用功能，它提供了国际化支持及框架事件体系，更易于创建实际的应用。一般称BeanFactory为Ioc容器，而ApplicationContext为应用上下文。

- **BeanFactory的继承体系如下图所示：**
![BeanFactory](../images/core/BeanFactory.jpg)


- **BeanFactory继承体系中重要的Bean说明**

   - **BeanFactory**
   
     > 定义：
   
         * The root interface for accessing a Spring bean container.
         * This is the basic client view of a bean container;
         * further interfaces such as {@link ListableBeanFactory} and
         * {@link org.springframework.beans.factory.config.ConfigurableBeanFactory}
         * are available for specific purposes.
         
     > 主要方法：
     
      - Object getBean(String name) throws BeansException
      - ...
      - \<T> ObjectProvider\<T> getBeanProvider(Class\<T> requiredType)
      - ...
      - boolean containsBean(String name);
      - boolean isSingleton(String name) throws NoSuchBeanDefinitionException
      - boolean isPrototype(String name) throws NoSuchBeanDefinitionException
      - boolean isTypeMatch(String name, ResolvableType typeToMatch) throws NoSuchBeanDefinitionException
      - boolean isTypeMatch(String name, Class\<?> typeToMatch) throws NoSuchBeanDefinitionException
      - Class\<?> getType(String name) throws NoSuchBeanDefinitionException
      - String[] getAliases(String name)
     
   - **HierarchicalBeanFactory**
     > 定义
    
          * Sub-interface implemented by bean factories that can be part
          * of a hierarchy.
          *
          * <p>The corresponding {@code setParentBeanFactory} method for bean
          * factories that allow setting the parent in a configurable
          * fashion can be found in the ConfigurableBeanFactory interface. 
     > 主要方法：
     - BeanFactory getParentBeanFactory()
     - boolean containsLocalBean(String name)          
   
   - AutowireCapableBeanFactory
     >定义：
     
         * Extension of the {@link org.springframework.beans.factory.BeanFactory}
         * interface to be implemented by bean factories that are capable of
         * autowiring, provided that they want to expose this functionality for
         * existing bean instances.  
         
     >主要方法：
     - \<T> T createBean(Class\<T> beanClass) throws BeansException
     - void autowireBean(Object existingBean) throws BeansException
     - Object createBean(Class\<?> beanClass, int autowireMode, boolean dependencyCheck) throws BeansException    
     - Object autowire(Class\<?> beanClass, int autowireMode, boolean dependencyCheck) throws BeansException
     -  void autowireBeanProperties(Object existingBean, int autowireMode, boolean dependencyCheck) throws BeansException
     - void applyBeanPropertyValues(Object existingBean, String beanName) throws BeansException
     - Object initializeBean(Object existingBean, String beanName) throws BeansException
     - Object applyBeanPostProcessorsBeforeInitialization(Object existingBean, String beanName) throws BeansException
     - Object applyBeanPostProcessorsAfterInitialization(Object existingBean, String beanName) throws BeansException
     - void destroyBean(Object existingBean)
     - \<T> NamedBeanHolder\<T> resolveNamedBean(Class\<T> requiredType) throws BeansException
     - Object resolveDependency(DependencyDescriptor descriptor, @Nullable String requestingBeanName) throws BeansException
     - Object resolveDependency(DependencyDescriptor descriptor, @Nullable String requestingBeanName,
      			@Nullable Set\<String> autowiredBeanNames, @Nullable TypeConverter typeConverter) throws BeansException 
      			
   - **ListableBeanFactory**
     >定义:
     
         * Extension of the {@link BeanFactory} interface to be implemented by bean factories
         * that can enumerate all their bean instances, rather than attempting bean lookup
         * by name one by one as requested by clients. BeanFactory implementations that
         * preload all their bean definitions (such as XML-based factories) may implement
         * this interface.
     
     > 主要方法：
     - boolean containsBeanDefinition(String beanName)
     - int getBeanDefinitionCount()
     - String[] getBeanDefinitionNames()
     - String[] getBeanNamesForType(ResolvableType type)
     - String[] getBeanNamesForType(@Nullable Class\<?> type)
     - String[] getBeanNamesForType(@Nullable Class\<?> type, boolean includeNonSingletons, boolean allowEagerInit)
     - \<T> Map<String, T> getBeansOfType(@Nullable Class\<T> type) throws BeansException
     - \<T> Map<String, T> getBeansOfType(@Nullable Class\<T> type, boolean includeNonSingletons, boolean allowEagerInit)
       			throws BeansException
     - String[] getBeanNamesForAnnotation(Class<? extends Annotation> annotationType)
     - Map\<String, Object> getBeansWithAnnotation(Class<? extends Annotation> annotationType) throws BeansException
     - \<A extends Annotation> A findAnnotationOnBean(String beanName, Class\<A> annotationType)
       			throws NoSuchBeanDefinitionException
       			
   - **SingletonBeanRegistry**
     >定义：
       
         * Interface that defines a registry for shared bean instances.
         * Can be implemented by {@link org.springframework.beans.factory.BeanFactory}
         * implementations in order to expose their singleton management facility
         * in a uniform manner.
         
     > 主要方法：
     
     - void registerSingleton(String beanName, Object singletonObject)
     - Object getSingleton(String beanName)
     - boolean containsSingleton(String beanName)
     - String[] getSingletonNames()
     - int getSingletonCount()
     - Object getSingletonMutex()
   
   - **AliasRegistry**
   - **SimpleAliasRegistry**  
   - **DefaultSingletonBeanRegistry**