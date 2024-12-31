> #### 作者主页：[舒克日记](https://blog.csdn.net/cativen)
>
>  简介：Java领域优质创作者、Java项目、学习资料、技术互助
>
> <b><font color=red>文中获取源码</font></b>

# 项目介绍

人事管理系统分为管理员和用户两部分操作角色

本次开发的人事管理系统实现了财务报销管理、字典管理、试卷表管理、试题表管理、考试记录表管理、答题详情表管理、错题表管理、公告管理、请假管理、员工管理、管理员管理等功能。

# 环境要求

1.运行环境：最好是java jdk1.8,我们在这个平台上运行的。其他版本理论上也可以。

2.IDE环境：IDEA,Eclipse,Myeclipse都可以。推荐IDEA;

3.tomcat环境：Tomcat7.x,8.X,9.x版本均可

4.硬件环境：windows7/8/10 4G内存以上；或者Mac OS;

5.是否Maven项目：是；查看源码目录中是否包含pom.xml;若包含，则为maven项目，否则为非maven.项目

6.数据库：MySql5.7/8.0等版本均可；

# 技术栈

运行环境：jdk8 + tomcat9 + mysql5.7 + windows10

服务端技术：Spring Boot+ Mybatis +VUE

# 使用说明

​

1.使用Navicati或者其它工具，在mysql中创建对应sq文件名称的数据库，并导入项目的sql文件；

2.使用IDEA/Eclipse/MyEclipse导入项目，修改配置，运行项目；

3.将项目中config-propertiesi配置文件中的数据库配置改为自己的配置，然后运行；

# 运行指导

idea导入源码空间站顶目教程说明(Vindows版)-ssm篇：

http://mtw.so/5MHvZq

源码地址：[http://www.codegym.top](http://www.codegym.top/)。


# 运行截图

## 文档截图

![img](https://img-blog.csdnimg.cn/img_convert/558c0be127165dc6f5fcc7a2207de2e5.png)

### 项目截图

![springboot247人事管理系统0](https://img-blog.csdnimg.cn/img_convert/d9265b43662e13bfd4875d0de182a6cb.png)

![springboot247人事管理系统1](https://img-blog.csdnimg.cn/img_convert/0909e7bfa6212af92f81841cb1e75fd9.png)

![springboot247人事管理系统2](https://img-blog.csdnimg.cn/img_convert/7edbb8e269975169fa1d20afbe38ac1e.png)

![springboot247人事管理系统3](https://img-blog.csdnimg.cn/img_convert/759b1c0cb296340d38caa5e8b8002bf4.png)

![springboot247人事管理系统4](https://img-blog.csdnimg.cn/img_convert/3a5d17f1c70f3810c5dbf431618b90d5.png)

![springboot247人事管理系统5](https://img-blog.csdnimg.cn/img_convert/8847da23fa7ded5ee378028bc736d95d.png)

![springboot247人事管理系统6](https://img-blog.csdnimg.cn/img_convert/b303380c1c199a0e2f48e3d3d82e01b3.png)

![springboot247人事管理系统7](https://img-blog.csdnimg.cn/img_convert/416e55fe52b4f56c3ed2d49bfb80f8c4.png)

### 代码

```
 private Map<String, UserOrganizationMapDTO> getOrganizationMap(List<String> ids){
        Map<String, UserOrganizationMapDTO> map = new HashMap<>();
        List<UserOrganizationMapDTO> userOrganizationMapDTOS = new ArrayList<>();
        if (RequestUtils.isAdministrator()) {
            userOrganizationMapDTOS = userOrganizationMapper.selectOrganizationListByUserIds(ids,null);
        }else {
            String currentTenantId = RequestUtils.getCurrentTenantId();
            userOrganizationMapDTOS = userOrganizationMapper.selectOrganizationListByUserIds(ids,currentTenantId);
        }
        if (!CollectionUtils.isEmpty(userOrganizationMapDTOS)) {
            for(UserOrganizationMapDTO organizationDO:userOrganizationMapDTOS){
                UserOrganizationMapDTO userOrganizationDTO = map.get(organizationDO.getUserId());
                if (userOrganizationDTO == null) {
                    UserOrganizationMapDTO newOrganizationDTO = new UserOrganizationMapDTO();
                    newOrganizationDTO.setName(organizationDO.getName());
                    ArrayList<String> newIds = new ArrayList<>();
                    newIds.add(organizationDO.getOrganizationId());
                    newOrganizationDTO.setIds(newIds);
                    map.put(organizationDO.getUserId(),newOrganizationDTO);
                }else {
                    String name = userOrganizationDTO.getName();
                    name = name +"," + organizationDO.getName();
                    userOrganizationDTO.setName(name);
                    List<String> oldIds = userOrganizationDTO.getIds();
                    oldIds.add(organizationDO.getOrganizationId());
                    map.put(organizationDO.getUserId(),userOrganizationDTO);
                }

            }
        }
        return map;
    }
```
