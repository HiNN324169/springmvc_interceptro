# springmvc_interceptro
springmvc 拦截器 入门案例

一、操作步骤简述：

    1、创建一个类 实现 HandlerInterceptor接口，并实现其方法
    
        方法简述：
        --> preHandle：拦截请求，客户端发送请求时，首先执行的方法，返回值：true 放行，false 拦截
        --> postHandle：拦截响应，controller执行完后，响应客户端前，执行该方法
        --> afterCompletion：视图jsp 被渲染完毕，客户端页面响应结束后执行该方法

    public class MyInterceptor implements HandlerInterceptor {
        @Override
        public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o) throws Exception {
        System.out.println("拦截 请求");
        /**
         *  返回 ：true 放行
         *          false 拦截
         */
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
        System.out.println("拦截 响应");

    }

    @Override
    public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
        System.out.println("视图 jsp 被渲染完毕");


    }
}


2、在 springmvc 配置文件中 配置拦截器

    全局配置，拦截全部请求

<!--配置拦截器：拦截全部请求-->
<!--<mvc:interceptors>-->
    <!--<bean class="com.nn.interceptor.MyInterceptor"></bean>-->
<!--</mvc:interceptors>-->


单个配置
<mvc:interceptors>
    <!-- 配置第一个拦截器-->
    <mvc:interceptor>
        <!-- 配置拦截的路径
            path 写法: 基于 ant 风格
        -->
        <mvc:mapping path="/**"/>

        <!-- 配置不拦截的路径
            注意：path 路径为 @RequestMapping 构成的路径，不要加入 项目名称Artfact
        -->
        <mvc:exclude-mapping path="/login"/>

        <!-- 配置拦截器-->
        <bean class="com.nn.interceptor.MyInterceptor"></bean>

    </mvc:interceptor>

</mvc:interceptors>


多个拦截器配置
<mvc:interceptors>
    <!-- 配置 第二个拦截器-->
    <mvc:interceptor>
        <!-- 配置拦截的路径
            path 写法: 基于 ant 风格
        -->
        <mvc:mapping path="/**"/>

        <!-- 配置不拦截的路径-->
        <mvc:exclude-mapping path="/login"/>

        <!-- 配置拦截器-->
        <bean class="com.nn.interceptor.MyInterceptor2"></bean>

    </mvc:interceptor>

    <!-- 配置第一个拦截器-->
    <mvc:interceptor>
        <!-- 配置拦截的路径
            path 写法: 基于 ant 风格
        -->
        <mvc:mapping path="/**"/>

        <!-- 配置不拦截的路径-->
        <mvc:exclude-mapping path="/login"/>

        <!-- 配置拦截器-->
        <bean class="com.nn.interceptor.MyInterceptor"></bean>

    </mvc:interceptor>

</mvc:interceptors>

