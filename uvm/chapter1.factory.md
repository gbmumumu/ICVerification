# Factory
## 意义
- 工厂的存在在于更方便的替换验证环境中的实例或已注册的类型，工厂的注册机制也带来配置的灵活性。


“替换”即**override**, 被替换的对象或者类型应满足：1.注册(registration)；2.多态(polymorphism)的要求。


                / class uvm_component 环境的层次 extends uvm_object
    UVM验证环境   
                \ class uvm_object    环境的属性/数据传输

这两种class即工厂的主要**模具**<通过注册可以利用工厂完成对象的创建>和**生产对象**<工厂生产模具灵活好替代>，这使得可以在不修改原有代码层次和验证包的同时完成环境内部组件类型或对象的覆盖。
### 便利
将大象装进冰箱需要三步，打开Factory也一样：


    step 1. 将class注册到工厂；ie. `uvm_component_utils(cls_name)/`uvm_object_utils(cls_name)
    step 2. 在例化前设置覆盖对象和类型(可选)；
    step 3. 对象创建；ie. tmp_obj = cls_name::type_id::create("tmp_obj")


