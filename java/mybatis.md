## mybatis 约定俗称的规则  
1. resultType和parameterType都只能写一个值，不过需要很多参数的时候是可以用集合等来作为类型的
2. 如果是八个基本类型+String的简单类型，则在参数上可以用任意占位符#{x'x'x}，但如果是对象的话要用#{属性值}
3. 无论返回结果是一个还是多个，resultType都只能写对象类型，不可以是list什么的。直接用List接受就可以了 

```xml
<!-- 
	in 查询
	List<User> selectByIdSet(List idList);
-->

<select id="selectByIdSet" resultMap="BaseResultMap">
	SELECT
	<include refid="Base_Column_List" />
	from t_user
	WHERE id IN
	<foreach collection="list" item="id" index="index" open="(" close=")" separator=",">
	  #{id}
	</foreach>
</select>

<!-- 
	if 判断 
-->
<select id="selectUseIf" parameterType="com.soft.test.model.DynamicTestModel" resultMap="userMap">
        select * from t_user where 1=1
        <if test='id != null and id > 28'>
        	and id=#{id}
        </if>
</select>

<!-- 
	if else  批量插入用户 
	when 相当 if  
	otherwise 相当 else
-->
<insert id="insertBusinessUserList" parameterType="java.util.List">
    insert into `business_user` (`id` , `user_type` , `user_login` )
    values
    <foreach collection="list" index="index" item="item" separator=",">
        <trim prefix="(" suffix=")" suffixOverrides=",">
            <choose>
                <when test="item.id != null and item.id !=''">
                    #{item.id,jdbcType=CHAR},
                </when>
                <otherwise>
                    '',
                </otherwise>
            </choose>
            <choose>
                <when test="item.userType != null and item.userType !=''">
                    #{item.userType,jdbcType=VARCHAR},
                </when>
                <otherwise>
                    '',
                </otherwise>
            </choose>
        </trim>
    </foreach>
</insert>

<!--
list 映射 
-->
<resultMap id="QueryResultMap" type="com.kxdzc.push.domain.entity.vo.PushTemplateVo">
        <id column="id" property="id"/>
        <result column="channel" property="channel"/>
        <result column="key" property="key"/>
        <result column="title" property="title"/>
        <result column="desc" property="desc"/>
        <result column="content" property="content"/>
        <result column="params" property="params"/>
        <result column="hrefType" property="hrefType"/>
        <result column="href" property="href"/>
        <result column="template_id" property="templateId"/>
        <result column="used_count" property="usedCount"/>
        <result column="offline" property="offline"/>
        <result column="offline_expire_time" property="offlineExpireTime"/>
        <result column="ctime" property="ctime"/>
        <result column="utime" property="utime"/>
        <result column="status" property="status"/>
        <collection property="filters" javaType="ArrayList" ofType="com.kxdzc.push.domain.entity.PushTemplateFilter">
            <id column="filters.id" property="id"/>
            <result column="filters.push_template_id" property="pushTemplateId"/>
            <result column="filters.phone" property="phone"/>
            <result column="filters.status" property="status"/>
            <result column="filters.type" property="type"/>
            <result column="filters.ctime" property="ctime"/>
            <result column="filters.utime" property="utime"/>
        </collection>
    </resultMap>
```