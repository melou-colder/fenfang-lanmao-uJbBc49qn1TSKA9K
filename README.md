
在AngularJS中，控制器是用于控制视图行为的重要组件。当定义控制器时，有两种主要的方式注入依赖项：


**1\. 显式依赖注入，即使用字符串数组形式来注入依赖项：**



[?](https://github.com)

| 123 | `myapp.controller(``'myCtrl'``, [``'$scope'``, function($scope) {``$scope.navs = [];``}]);` |
| --- | --- |



 


　　在这种方式中，依赖项（这里是\`$scope\`）是以字符串的形式明确列出的。这种方法被称为“显式依赖注入”，它使得依赖关系更加明显，并且有助于测试，因为可以更容易地为依赖项提供mock对象。这是AngularJS官方推荐的做法，因为它能够避免由于作用域链导致的问题，并且有助于提高代码的可维护性。这种写法中function($scope)的参数名`$scope`可以在函数内部更改而不影响代码的执行，因为AngularJS会根据字符串数组中的名字来查找对应的依赖项。例如，您可以将函数参数改为任何其他名称，如下所示：




[?](https://github.com):[wgetCloud机场](https://tabijibiyori.org)

| 123 | `myapp.controller(``'myCtrl'``, [``'$scope'``, function(myCustomScopeName) {``myCustomScopeName.navs = [];``}]);` |
| --- | --- |



　　



只要第一个数组元素`'$scope'`保持不变，AngularJS就能正确地将`$scope`实例注入到名为`myCustomScopeName`的参数中。


**2\. 隐匿依赖注入，即直接传递依赖项名称的形式：**



[?](https://github.com)

| 123 | `myapp.controller(``'myCtrl'``, function($scope) {``$scope.navs = [];``});` |
| --- | --- |



　　这种方式中，依赖项（如\`$scope\`）直接作为参数传递给构造函数。虽然这种方式简洁，但它依赖于解析器能够正确解析出函数参数名并将其与服务名称匹配。这在开发阶段可能会导致一些问题，尤其是在某些JavaScript优化工具（如闭包编译器）压缩代码时，可能会改变变量名，从而导致注入失败。这种写法中，function($scope)的$scope这个函数参数就不能更改名称了。否则AngularJS将无法识别并注入正确的服务，从而导致错误。


总的来说，第一种方法（显式依赖注入）更安全，更易于调试和测试，而第二种方法虽然简单，但在大型项目中可能会带来一些问题。因此，建议使用第一种方法来定义你的控制器。


