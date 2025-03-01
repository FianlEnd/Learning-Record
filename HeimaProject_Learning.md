# **java后端学习**

## Maven
### &emsp;&emsp;依赖管理
&emsp;&emsp;在maven的pom.xml文件中添加配置 
### &emsp;&emsp;项目构建 
&emsp;&emsp;maven提供了一套简单命令进行项目构建，能很容易完成 编译(compile),测试(test),打包(package),发布(deploy) 的操作，并且支持跨平台。
### &emsp;&emsp;统一项目结构
&emsp;&emsp;提供了标准java项目目录
```
maven-project01
        |---  src  (源代码目录和测试代码目录)
               |---  main (源代码目录)
                        |--- java (源代码java文件目录)
                        |--- resources (源代码配置文件目录)
              |---  test (测试代码目录)
                        |--- java (测试代码java目录)
                        |--- resources (测试代码配置文件目录)
        |--- target (编译、打包生成文件存放目录)
```
### &emsp;&emsp;生命周期
- clean：清理工作。
- default：核心工作。如：编译、测试、打包、安装、部署等。
- site：生成报告、发布站点等。
- 生命周期的顺序：clean --> validate --> compile --> test --> package --> verify --> install --> site --> deploy
- 比较关注的：clean -->  compile --> test --> package  --> install

### &emsp;&emsp;使用JUnit进行单元测试
&emsp;&emsp;(Get的请求参数在请求行中，Post的请求参数在请求体中，Post请求安全性相对较高

&emsp;&emsp;请求行，请求头，请求体，响应头，响应行，响应体  

&emsp;&emsp;响应码：

&emsp;&emsp;1xx	响应中 --- 临时状态码。表示请求已经接受，告诉客户端应该继续请求或者如果已经完成则忽略

&emsp;&emsp;2xx	成功 --- 表示请求已经被成功接收，处理已完成

&emsp;&emsp;3xx	重定向 --- 重定向到其它地方，让客户端再发起一个请求以完成整个处理

&emsp;&emsp;4xx	客户端错误 --- 处理发生错误，责任在客户端，如：客户端的请求一个不存在的资源，客户端未被授权，禁止访问等

&emsp;&emsp;5xx	服务器端错误 --- 处理发生错误，责任在服务端，如：服务端抛出异常，路由出错，HTTP版本不支持等)


## 三层架构

Controller: 接受请求，响应数据  
Service: 逻辑处理   
Dao: 数据访问


## 软件设计原则：高内聚低耦合

- 控制反转： Inversion Of Control，简称IOC。对象的创建控制权由程序自身转移到外部（容器），这种思想称为控制反转。
  - 对象的创建权由程序员主动创建转移到容器(由容器创建、管理对象)。这个容器称为：IOC容器或Spring容器。
  
- 依赖注入： Dependency Injection，简称DI。容器为应用程序提供运行时，所依赖的资源，称之为依赖注入。
  - 程序运行时需要某个资源，此时容器就为其提供这个资源。
  - 例：EmpController程序运行时需要EmpService对象，Spring容器就为其提供并注入EmpService对象。

- bean对象：IOC容器中创建、管理的对象，称之为：bean对象。


在实现类加上 @Component(衍生注解@Controller，@Service，@Repository)，把当前类产生的对象交给IOC容器管理。    
依赖注入方式    
```
@RestController
public class UserController {

    //方式一: 属性注入
    @Autowired
    private UserService userService;
    
  }
  
@RestController
public class UserController {

    //方式二: 构造器注入
    private final UserService userService;
    
    @Autowired //如果当前类中只存在一个构造函数, @Autowired可以省略
    public UserController(UserService userService) {
        this.userService = userService;
    }
    
 }   

@RestController
public class UserController {
    
    //方式三: setter注入
    private UserService userService;
    
    @Autowired
    public void setUserService(UserService userService) {
        this.userService = userService;
    }
    
}    
``` 

防止同类型bean出现两个方法:

方案一：使用@Primary注解
当存在多个相同类型的Bean注入时，加上@Primary注解，来确定默认的实现。  
```
@Primary
@Service
public class UserServiceImpl implements UserService {
}
```

方案二：使用@Qualifier注解
指定当前要注入的bean对象。 在@Qualifier的value属性中，指定注入的bean的名称。 @Qualifier注解不能单独使用，必须配合@Autowired使用。
```
@RestController
public class UserController {
    @Qualifier("userServiceImpl")
    @Autowired
    private UserService userService;}
```

方案三：使用@Resource注解
是按照bean的名称进行注入。通过name属性指定要注入的bean的名称
```
@RestController
public class UserController { 
    @Resource(name = "userServiceImpl")
    private UserService userService;}
```


