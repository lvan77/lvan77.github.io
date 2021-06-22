## lombok 插件  
注意问题：
@Data，而不使用@EqualsAndHashCode(callSuper=true)的话，
会默认是@EqualsAndHashCodecallSuper=false),
这时候生成的equals()方法只会比较子类的属性，
不会考虑从父类继承的属性，无论父类属性访问权限是否开放。