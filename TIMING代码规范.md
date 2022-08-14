# 单体应用代码规范

1. 遵循阿里巴巴代码规范[Java开发手册（嵩山版）.pdf](https://faofvizbmz.feishu.cn/file/boxcncOEfIhhN4kwFhWGCesVcXg)，安装阿里巴巴编码规约插件
2. 对外接口路径命名，单词之间使用`-`连接
3. Controller层参数接收，Post请求大于3个参数时，必须定义对象接收，对象名称以DTO结尾
4. Controller层返回数据，出参字段大于3个时，需定义对象返回，对象名称以VO结尾
5. 代码中方法间数据传递，尽量避免使用JSONObject或者Map
6. 方法参数添加注释
7. 新增service接口需署名，存在多个实现类时，实现类中方法也需要署名（除非接口和所有实现类都是你写的）
8. 合理拆分和提取业务方法，减少代码冗余
9. 不要在Service层调用其他模块的Mapper操作sql
10. 开启事务的注解`@Transactional`按需使用
11. 状态、库存数量等重要数据修改时，需考虑并发问题，可通过加锁、CAS等进行修改
12. Bean之间转换使用Orika工具
13. 业务处理的代码各个步骤需配以一定量的注释
14. 代码提交，禁止提交`.idea`、`.iml`、`target`等文件
15. 注意代码整洁以及格式化，提高代码可读性
16. 前后端时间数据交互，统一用时间戳
17. 使用泛型类时，标明具体类型，如：`List<String>`、`Map<String,Object>`、`Result<XxxxVO>`等

## 方法注释模板

[(67条消息) IDEA类和方法注释模板设置（非常详细）_黑taoA的博客-CSDN博客_idea注释模板设置](https://blog.csdn.net/yy12345_6_/article/details/123830038)

IDEA：File -> Setting -> Editor -> Live Templates

**Template text(模板内容):**

```java
*
 * 方法说明
 $params$
 * @return $return$
 * @author huangyufeng
 * @date $date$ $time$
 */
```

**Edit variables(编辑变量):**

**params**

```
groovyScript("def result='';def tempStr=''; def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList(); for(i = 0; i < params.size(); i++) {if(i==0){result+='* @param ' + params[i] + ((i < params.size() - 1) ? '\\r\\n' : '')}else{result+='         * @param ' + params[i] + ((i < params.size() - 1) ? '\\r\\n' : '')}}; return result", methodParameters())
```

**return**

```
groovyScript("def result=\"${_1}\"; if(result == \"void\"){return \"\";}else{return \"{@link \"+result+\"}\";}", methodReturnType())
```

**date**

```
date("yyyy/MM/dd")
```

**time**

```
time()
```